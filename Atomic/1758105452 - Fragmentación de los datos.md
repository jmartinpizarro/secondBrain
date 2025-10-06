---
aliases:
  - Fragmentación de los datos
tags:
"References":
cssclasses:
---
# Fragmentación de los datos

Los datos se organizan para **optimizar el acceso y los tiempos de respuesta**, asegurando que los datos a los que se acceden se ubiquen en el mismo nodo.

>[!NOTE]
>El agregado se convierte en la unidad de fragmentación

Criterios:
- Proximidad geográfica
- Temporalidad
- Secuencialidad
- Distribución uniforme

La **localización física** de los datos se determina a partir de **claves de fragmentación**, usualmente *hashes* a partir de atributos del dato.

Los datos **pueden cambiar de valor** a lo largo de su ciclo de vida, es necesaria una **re-fragmentación**. 

**Ventajas**:
- Escalabilidad en lecturas y escrituras
- No consume muchos recursos la gestión del cluster
- Consistencia mejora al repartir responsabilidad de los datos entre los nodos
**Desventajas**:
- Paso de una DB única a una fragmentada es complicado.
- Menor fiabilidad
- Consultas a la totalidad son costosas.
