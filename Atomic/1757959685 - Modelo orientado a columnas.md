---
aliases:
  - Modelo orientado a columnas
tags:
"References":
cssclasses:
---
# Modelo orientado a columnas

Ven los datos como una matriz bidimensional:
- Filas: agregaciones de datos accedidas por clave
- Columnas: los atributos de las agregaciones se representan mediante una tripleta
$$(\text{nombre, valor, timestamp})$$
Atomicidad a nivel de fila.

Adecuados para accesos a sistemas distribuidos. Más lentas que clave-valor (menos escalables). 

Mucho más eficientes cuando:
- Inserción de múltiples registros al mismo tiempo (se actualizan en bloques de columnas).
- Cuando solo se quiere acceder a una serie de columnas.

