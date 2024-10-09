---
aliases:
  - Modelización
tags:
  - review
"References":
cssclasses:
---
# Modelización

## Transporte

Dados $m$ orígenes y $n$ destinos donde:
$$a_i \rightarrow \text{capacidad origen i}, \space 1 \leq j \leq n $$
$$b_i \rightarrow \text{demanda destino j}, \space 1 \leq j \leq n$$
$$c_{ij} \rightarrow \text{coste unitario} \space i \rightarrow j$$
Si hacemos una relación directa entre orígenes y destinos, veremos que deberíamos generar un grafo bipartito.

Es decir, sabiendo que queremos mover $x_{ij} \triangleq cantidad \space i \rightarrow j$ , tendremos varios requisitos genéricos:
1. No agotar ninguna base de suministros (si tenemos 10.000 palets, no entregar 10.001) $$\sum_{j=1}^n x_{ij} \leq a_i \space \forall i$$
2.  Todos los destinos tienen que ser mayor o igual a la demanda $$\sum_{j=1}^m x_{ij} \geq b_j \space \forall j$$
## Asignación

Dados $m$ individuos y $m$ tareas conocido un valor $C_{ij} \triangleq coste \space i \rightarrow j$

Si hacemos una relación directa entre individuos y tareas, veremos que deberíamos generar un grafo bipartito.

Las variables de decisión serán binarias: $x_{ij} \triangleq  \begin{cases}  1 & \text{si i} \rightarrow j \\ 0 & \text{en caso contrario} \end{cases}$

Tendremos tantas restricciones como individuos.

## Condicionales

Aplicado a relaciones del tipo *causa y efecto*. Para ello usaremos el *Método de la M*. A efectos prácticos, es aplicar [[1727968348 - Sobre condiciones binarias en programación lineal|Sobre condiciones binarias en programación lineal]]. 

***