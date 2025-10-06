---
aliases:
  - Modelos de agregación
tags:
"References":
cssclasses:
---
# Modelos de agregación

Un agregado es un solo conjunto de datos que se gestiona como una sola unidad.
- Se identifican por una clave única
- Unidad mínima de almacenamiento y consulta
- Los cambios aplican al agregado completo

## Diseño del agregado

Se guía por los patrones de caso de uso de la aplicación, que son las consultas más frecuentes. 

El perímetro del agregado es una decisión de diseño: define qué datos viajan siempre juntos.

Bien diseñados, los agregados **reducen accesos y evitan JOINS forzosos**.

Útiles cuando:
- La funcionalidad está definida de antemano y no se esperan cambios frecuentes
- No existen relaciones complejas entre entidades.