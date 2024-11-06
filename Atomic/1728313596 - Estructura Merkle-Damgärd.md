---
aliases:
  - Estructura Merkle-Damgärd
tags:
  - review
  - hash
References: 
cssclasses:
sr-due: 2024-11-02
sr-interval: 15
sr-ease: 290
---
# Estructura Merkle-Damgärd

Usada en la mayoría de funciones resumen actuales.

La idea es ejecutar funciones sobre un bloque y sus anteriores, de manera que siempre obtendremos un resultado con el mismo tamaño.

Para finalizar, añadimos la longitud del texto original, de manera que obtenemos otra autentificación.

![[HashingFunction.png]]
***