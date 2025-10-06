---
aliases:
  - Reducción de tasa de fallos
tags:
"References":
cssclasses:
---
# Reducción de tasa de fallos

## Aumento de tamaño de bloque

- Mayor tamaño de bloque -> menor la tasa de fallos, pero **mayor la penalización por fallos**
	- Mayor aprovechamiento de localidad espacial
Se requiere una necesidad de equilibrio:
- Memoria de alta latencia y alto ancho de banda: incrementa el tamaño de bloque
- Memoria de baja latencia con bajo ancho de banda: tamaño de bloque reducido

## Aumento tamaño de caché

Mayor tamaño de caché -> menor tasa de fallos, pero **puede incrementar el tiempo de acierto**.

Mayor coste -> mayor consumo de energía.

## Incremento de asociatividad

Mayor asociatividad -> menor tasa de fallos pero **puede incrementar tiempo de acierto**.