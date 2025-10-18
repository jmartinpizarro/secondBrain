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

### Validación de esquemas

