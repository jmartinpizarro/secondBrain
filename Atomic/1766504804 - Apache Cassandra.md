---
aliases:
  - Apache Cassandra
tags:
"References":
cssclasses:
---
# Apache Cassandra

## Introducción, características y estructura

Tolerante a fallos sin nodo maestro, **combina el modelo de almacenamiento de clave-valor con un diseño orientado a columna**.

### Modelo clave-valor vs orientado a columna

**Modelo clave-valor**:
- Cada elemento de datos tiene una clave única y un valor asociado
**Modelo orientado a columnas**:
- Almacena datos de la misma columna juntos
- Rápida agregación y operaciones sobre columnas completas
- Optimizada para lecturas por columna, no por filas. *Ideal para analítica*.

Cassandra combina lo mejor de ambos tipos:
- **Eficiencia de almacenamiento** clave-valor para accesos rápidos y directos a los datos
- **Optimización de operaciones en columnas** para consultas analíticas a gran escala.

Cassandra es altamente escalable y manejable con grandes volúmenes de datos distribuidos.

### Características

- **Alta disponibilidad**: diseñada para estar siempre operativa.Si un nodo falla, el resto continúa funcionando sin interrupción (arquitectura sin nodo maestro)
- **Consistencia configurable**: desde eventual hasta fuerte, según los requisitos de cada operación de lectura o escritura.
- **Alta escalabilidad**: casi lineal. Agregar más nodos incrementa el rendimiento de forma proporcional.
- **Rapidez**: tiempos de respuesta rápidos en consultas de lectura e **inmediatos en escrituras**. Idónea para entornos que requieren de procesamiento rápido de datos.
- **Sencillez en la replicación y distribución de datos**: es automática, mejorando la tolerancia a fallos y la disponibilidad.
- **Operaciones transaccionales**: soporta transacciones ACID, aunque con algunas limitaciones frente a bases de datos tradicionales

Su estructura se basa en:
- **Cluster**: unidad de infraestructura más grande. Es la agrupación de uno o más Data Centers. Los nodos forman un anillo lógico, y se les asigna los datos acordes con las directrices predefinidas. La replicación se realiza automáticamente.
- **Data Center**: conjunto de nodos relaciones
- **Rack**: grupo de nodos físicamente cercanos dentro del mismo armario o módulo. Un fallo de rack implica riesgo de caída conjunta.
- **Nodo**: cualquier miembro de la red (almacena datos y proporciona servicios)
- **Nodo virtual (vNode)**: cubo de datos
- ***Factor de replicación***: cantidad de copias que se hacen de los datos, siguiendo una estrategia de replicación:
	- *Simple Strategy*: las copias se realizan en los nodos siguientes del anillo, no se consideran racks ni datacenters
	- *Network Topology Strategy*: controla en qué racks y data centers replicar.

## Diseño

### Claves de diseño

**Redundancia lógica**: puede ser necesaria para mejorar la eficiencia de acceso a los datos. Optimizado para cargas OLTP distribuidas. Se diseñan tablas para cada consulta, mejorando notable el rendimiento.

**Procesos batch**: permiten actualizaciones atómicas en varios registros relacionados. No están pensados para optimizar le rendimiento. 

>[!DANGER]
>Los procesos batch solo se deben de usar cuando las operaciones tengan una dependencia lógica, sino se degradará el rendimiento.

**Clave primaria**: es más una cuestión de garantizar la unicidad que de optimizar recursos. No se usa para identificar filas, **sino que determina la distribución física del dato**.

>[!WARNING]
>Si tenemos `PRIMARY KEY (country)` y 10 millones de usuarios en España, toda la partición "ES" va al mismo nodo -> hotspot -> cluster muerto.

#### Elección de clave primaria

- Si la clave primaria se define **a nivel de columna**, sólo consta de ese único atributo
- Si se define **a nivel de tabla**, puede tener varios atributos.

Si se inserta una fila con un valor de clave primaria ya existente, se sobreescribe dicha fila con la nueva información. No existe *rollback*.


**Clave de partición**: el **primer atributo de la PK**; es el que definirá la ubicación de los datos (en qué nodo se almacenan, mediante *hash*).
- Puede contener varios atributos (pero no es habitual)

*Ejemplo para modelos tipo geolocalización*: `PRIMARY KEY ((country, city), user_id)`.

**Clave de clusterización**: el resto de los atributos de la PK definen la posición de los datos dentro del nodo (ordenación).

*En el caso anterior, user_id es una clave de clusterización*

## Distribución de los datos y arquitectura de almacenamiento

### Dispersión

**Clave de partición**: toda la fila lleva una clave privilegiada que determina su ubicación.

La ubicación se basa en $n$ (número de nodos) y en la transformación numérica (token) del valor de la fila en la clave de partición.

**Hash consistente**: $x // n$. Reduce migración de datos si cambia $n$ (comparado con el hash módulo simple $x \space \% \space n$.

Al añadir un nodo nuevo, solo los tokens comprendidos entre el nodo nuevo y su predecesor deben moverse.

### Replicación

Independiente del particionamiento: primero se determina el nodo primario y después las réplicas se colocan en los siguientes nodos del anillo según la estrategia de replicación.

La replicación de los datos depende del **factor de replicación** definido para el *keyspace*.

Con $RF=1$, no hay tolerancia a fallos. Con $RF = 2$, se tolera la caída de un nodo. Con $RF = 3$, se toleran múltiples fallos de *racks*.

**Simple Strategy**: réplicas dentro del mismo Data Center (solo para entornos de *testing*).
**Network Topology Strategy**: réplicas distribuidas entre racks y múltiples Data Centers. Permite elegir cuántas replicas van en cada Data Center.

### **Distribución de los datos**

$\exists$ la posibilidad que hubiera nodos saturados y otros vacíos. Los *vNodes* existen para evitar *hotspots* y permitir sustituir nodos fácilmente. 

### Arquitectura de almacenamiento

- **Keyspace**: contenedor de información en el ámbito lógico (base de datos).
	- Define el factor de replicación de sus datos
	- Almacena una o más familias de columnas
- **Mem-table**: estructura de datos en RAM (*buffer*). Al confirmar (commit), los datos se escriben en una *mem-table*. Puede haber varias para cada columna. La *mem-table* se vuelca cuando tenga 128MB.
- **SSTable**: estructura en soporte secundario (fichero en disco) en el que se vuelcan los datos desde una *mem-table* cuando su contenido sobrepasa cierto umbral o tras un periodo de tiempo. 
- **Compactación**: es el proceso de fusionar **SSTables** para mejorar la eficiencia de las operaciones de lectura y reclamar espacio en disco.
	- Combina varias SSTables en una más grande, descartando las versiones obsoletas de los datos.
	- Puede afectar al rendimiento si no está bien dimensionado, por lo que debe ser programada y monitoreada cuidadosamente para mantener el equilibrio entre rendimiento y uso de recursos.

## Cassandra Query Language - CQL

### Keyspace

Contenedor para almacenar familias de columnas.
- Factor de replicación: número de nodos que almacenan cada dato
- Estrategia de replicación: ubica cada réplica de los datos (la primera está en su partición)
	- Simple Strategy: no debe usarse en producción.
	- Network Topology Strategy: adecuada para implementaciones con varios DC, permite dar más información para cada data center

```cql
# simple strategy
CREATE KEYSPACE [ IF NOT EXISTS ] myKeyspace
WITH repication = {
	'class' : 'SimpleStrategy',
	'replication_factor' : 2
}

# network topology strategy
CREATE KEYSPACE bigKeyspace
WITH replication = {
	'class’: ´NetworkTopologyStrategy´,
	'DC1': 2, 
	'Spain': 3, 
	'UK’: 2
	}
```


### Table

```cql
CREATE TABLE [ IF NOT EXISTS] employees (
	email text PRIMARY KEY,
	first_name text,
	last_name text,
	department text,
	hire_date date
);
```

### Tipos de datos

- Numéricos: int (32b), bigint (64b), smallint (8b), varint, float (32b), double (64b)
- Alfanuméricos: text (codificación UTF-8), varchar (UTF-8), ascii (cod.ascii)
- Tiempo: timestamp (64b), date (16b), time (8b)
- Identificadores: uuid, timeuuid
- Otros: Boolean, Blob, Counter, inet (IP address)

También existen los tipos compuestos:
- tuple `<tipo1, tipo2>`
- map `<text, text>`
- set `<tipo> / list <tipo>`

