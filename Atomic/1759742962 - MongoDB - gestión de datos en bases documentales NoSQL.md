---
aliases:
  - MongoDB - gestión de datos en bases documentales NoSQL
tags:
"References":
cssclasses:
---
# MongoDB - gestión de datos en bases documentales NoSQL

## Introducción

Almacén NoSQL de tipo documental. Almacenamiento no estructurado:
- Cada objeto se almacena en un documento
- Los grupos de objetos se almacenan en **colecciones** no estructuradas.
- La colección y la base de datos **no se definen**.

Se basa en el [[1759743087 - Formato BSON|Formato BSON]]

### Estructura de un documento

Lista de pares `<nombre : valor>` ordenados, separados por comas y agrupados por llaves. El campo valor puede ser cualquiera de los tipos de BSON incluyendo los compuestos.

Utiliza $.$ para referenciar a los elementos:
$$mydoc.name.first$$
Genera flexibilidad, pero **puede complicar las operaciones de consulta**.

### Colecciones

Proporcionan localidad a los datos; relacionándolos semánticamente entre sí.
- Esquema libre
- Los documentos no tienen por qué seguir un formato común
- Se pueden dividir en sub-colecciones dependiendo del criterio del dominio del problema
- Si los datos están mal estructurados, **los mecanismos de indexado son más eficientes**.

### Identificadores

Todos los documentos tienen una clave denominada $\_id$ (tipo ObjectId, 12 bytes en hexadecimal) que actúa como clave primaria.

Tres campos:
- *Timestamp* de 4 bytes que representa la fecha de creación del objeto en segundos
- Campo de 5 bytes basado en la máquina y PID de la instancia
- Contador de 3 bytes.

Se pueden generar manual o automáticamente.

## Modelado de datos

**Equilibrar las necesidades de la aplicación, características del motor y patrones de consulta**.

Existen dos mecanismos:
- **Embeber documentos**: incluir sub-documentos dentro de un documento, simplificando las consultas pero con documentos extensos
- **Referenciar documentos**: permite guardar el $\_id$ de otro documento, forzando a realizar múltiples consultas.
$$\text{\{"\$ref": "<value>, "\$id": <value>, "\$db": <value>\}}$$

### Patrones de modelado - Relaciones 1 a N

Las relaciones de $1$ a $N$ se pueden modelar de diversas formas:
- [[1759744109 - Embeber la tabla de referencia - embebiendo toda la relación|Embeber la tabla de referencia - embebiendo toda la relación]]
- [[1759744123 - Embeber todas las entidades referenciadas|Embeber todas las entidades referenciadas]]
- [[1759744144 - Embeber la referencia y el resumen|Embeber la referencia y el resumen]]

![[Pasted image 20251006114940.png]]

### Patrones de modelado - Relaciones 1 a 1

**Candidatas para opción de embeber los documentos**.

Cuidado con el tamaño final del documento

Posibilidad de repartir información usando patrón de [[1759744144 - Embeber la referencia y el resumen|Embeber la referencia y el resumen]].

### Patrones de modelado - Relaciones N a M

Siempre deben manejarse mediante referencias.

El valor de $N$ es importante:
- $N$ -> muchos -> puede ser recomendable usar referencias.
### Modelo de agregados

**Agregado**: conjunto de entidades que tratamos como una unidad para los cambios de datos.

**Raíz**: es el punto de entrada que garantiza la integridad del grafo de asociaciones dentro del agregado.

**Consistencia transaccional**: los agregados aseguran que los datos relaciones se mantengan coherentes.

**Perímetro**:
- Define los límites del agregado, especificando qué entidades forman parte de él
- El perímetro delimita las entidades que deben mantenerse coherentes dentro de una transacción.

## Validación de esquemas

A medida que se establece un esquema en tu aplicación, es recomendable usar validación de esquemas para asegurar que no haya cambios no intencionados en el esquema o datos incorrectos. Es un **mecanismo de consistencia**.

Se implementa a través de un JSON Schema, formato que permite anotar y validar documentos JSON.

Se define un esquema de validación para los documentos de una colección. Las reglas definidas en el esquema se aplican cada vez que se  inserta o se actualiza un documento de dicha colección.

```json
db.createCollection("students", {
	validator: {
		bsonType: "object",
		title: "Student Object Validation",
		required: ["address", "major", "name", "year"],
		properties: {
			name: {
				bsonType: "string",
				description: "'name' must be a string and is required"
			},
			year: {
				bsonType: "int",
				minimum: 2017,
				maximum: 3017,
				description: "..."
			},
			gpa {
				bsonType: ["double", "null"],
				description: "..."
			}
		}
	}
})
```

A la hora de insertar, si no se cumple el esquema MongoDB, el contenido no se insertará y se generará un error. Es posible cambiar este comportamiento por defecto.

También es posible usar operadores de consulta para añadir mayor definición a dichos esquemas. 

*Ejemplo: el precio final de descuento debe de ser menor que el precio final*

```json
db.createCollection("sales", {
	validator: {
		"$and": [
			{"$expr": {"$lt": ["$lineItems.discountedPrice", "$lineItems.price"]}},
			{"$jsonSchema": { 
				"properties": {"bsonType": "array"} 
				}
			}
		]
	}
})
```

## Operaciones CRUD

- `db.nombre_col.insert(var_name)`: inserta un documento en una determinada colección de la BD en uso utilizando una variable
- `db.nombre_col.insertOne(doc)`: inserta un documento en una determina colección de la BD definiendo el documento directamente en la invocación
- `db.nombre_col.insertMany([doc1, doc2,..., docn])`: inserta un array de documentos en una determinada colección de la BD
- `db.nombre_col.find(filter, projection)`: lectura de un conjunto de campos (projection) utilizando un filtro con condiciones.
- `db.nombre_col.deleteOne(filter)`
- `db.nombre_col.deleteMany(filter)`
- `db.nombre_col.deleteMany({})`: eliminar todos los elementos de la colección, dejándola vacía
- `db.col.drop()`: elimina la colección "col"

## Consultas y filtrado de datos

### Búsqueda. Filtro

La función *find()* admite dos parámetros: filtro y proyección.

El **filtro** es una expresión condicional compuesta de restricciones que se basan a su vez en operadores que se definen sobre los campos del documento y que tienen la forma `campo: {op: valor}`. La expresión vacía `{}` utilizada como filtro indica una selección completa. 

`{precio: {$ft: 100, $lt: 200}}`: indica que $100 < precio < 200$

Una **proyección** es una secuencia de inclusiones (campo: 1) o de exclusiones (campo: 0).

`db.libros.find( {Apellido:“Asimov"}, {Apellido:0, Título:0} )`: indica que se busque todos los libros con el apellido Asimov, pero en la query final no aparecerán ni el Apellido ni el Título del auto/libro respectivamente.

Las restricciones se pueden agrupar mediante **conectores** para constituir una expresión condicional compleja. **Conectores**: cuatro operadores lógicos para construir restricciones: AND, OR, NOR, NOT.

## Índices B+

Creación automática de un índice sobre el campo \_id  (PK). Se crean índices automáticos creados por el usuario para mejores el rendimiento. Índices secundarios para los diferentes elementos de un array.

- **Sparse index**: algo menos rápidos que los índices densos pero con consumo mucho menor. Solo incluye los documentos que poseen el campo indexado.

**Búsquedas textuales**: solo pueden ejecutarse sobre campos que tenga un índice del tipo *text*. Utiliza una string con las palabras a localizar.

## Procesamiento de Datos: Aggregation Pipeline

**Agregación**: permite agrupar y procesar los documentos de una colección o de un filtrado aplicado a una colección.
**Pipeline**: *framework* que bajo el modelo de un pipeline de varias fases puede transformar los documentos y calcular funciones agregadas.

### Aggregation Pipeline

Se invoca con el método `aggregate()` de las colecciones indicando como parámetro la lista de fases a ejecutar:
1. Transforma o selecciona la colección proporcionando otra intermedia sobre la que trabajar
2. Cada fase de pipeline toma de entrada la colección anterior, y proporciona otra nueva
3. Terminadas todas las fases, devuelve un cursos con la última colección.

```json
db.coffee.aggregate([
	{$match: {Coffea: {$ne: "Arabica"}}}
])
```

## Clusters de replicación

La replicación permite mantener varias copias sincronizadas de los mismos datos en diferentes servidores -> garantiza la disponibilidad, tolerancia a fallos y recuperación ante desastres.

MongoDB organiza la replicación mediante un conjunto de réplicas:
1. Uno actúa como nodo primario (líder): procesa ordenes de escritura, escribe en `oplog` el cambio y luego se sirve como fuente de verdad del cluster
2. Los demás como nodos secundarios: copian el contenido de `oplog`. Atiendes de lectura.

**Limitaciones**:
- Mayor consumo de recursos
- Latencia de replicación
- Carga centralizada en el primario
- Complejidad operativa

### Algoritmo RAFT

Si el nodo primario deja de responder, el cluster inicia un proceso de recuperación de consenso distribuido.
1. Los nodos vivos intercambias señales de vida
2. Los nodos votan siguiendo el protocolo basado en RAFT.
3. El nodo que tiene la mayoría de votos se convierte en primario.
4. Durante el proceso, el nodo principal acepta lecturas, pero nunca escrituras.

Además, MongoDB permite roles adicionales para optimizar el cluster:
- Secundario de prioridad 0: nunca puede ser elegido como líder, ideal para réplicas de respaldo.
- Secundario oculto: no atiende lecturas y se usa para tareas internas como backups o análisis.
- Árbitro: no almacena datos, pero participa en las votaciones para mantener un número impar de votos.

## Clusters de fragmentación - *sharding*

*Sharding* permite distribuir los datos entre varios servidores para conseguir escalabilidad horizontal. MongoDB divide las colecciones en *chunks* que se reparten automáticamente, manteniendo una visión unificada del sistema.

El **balanceo** y **enrutamiento** de consultas se gestionan de forma automática por el motor.

La fragmentación introduce complejidad y sobrecarga en la arquitectura, solo merece la pena usarla cuando **el sistema alcanza sus límites de**:
- Memoria disponible
- Capacidad de disco
- Rendimiento computacional

>[!DANGER]
>¡Es una técnica difícilmente reversible!

- Fragmentar demasiado poco: complica innecesariamente el sistema
- Fragmentar demasiado tarde: fuerza una migración en caliente sobre un sistema ya saturado.

Se puede hacer *sharding* por varias estrategias:
- Por rango: divide el dominio de la clave en intervalos ordenados. Ideal para consultas por rangos (fechas.)
- Por hash: función de hash sobre la clave, reparte los *chunks* uniformemente. Menos eficiente, pero evita *hotspots*.
- Combinada por rango y hash.
- Por zonas: asigna rangos o valores a *shards* específicos.

El **balancer** es un proceso del cluster que mantiene una distribución equilibrada de los datos de los shards. Por defecto es 128MB. Cuando detecta desigualdades en este número, comienza migraciones automáticas.