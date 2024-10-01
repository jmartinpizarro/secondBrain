---
tags:
  - AES
---
# ShiftRow

Consiste en ir desplazando bloques de **1 byte** hacia la izquierda módulo columna por cada fila.

Suponiendo una matrix $4x4$:
- La fila 0 no se desplaza
- La fila 1 se desplaza 1 bloque
- La fila 2 se desplaza 2 bloques
- La fila 3 se desplaza 3 bloques

