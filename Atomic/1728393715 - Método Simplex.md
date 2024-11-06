---
aliases:
  - Método Simplex
tags:
  - review
  - "#simplex"
  - programacionLineal
References: 
cssclasses: 
sr-due: 2024-10-18
sr-interval: 4
sr-ease: 270
---
# Método Simplex

## Introducción

Una tarea de programación lineal está en **FORMA ESTÁNDAR** cuando:
1. $z$ es una función de maximización
2. Las restricciones son del tipo $=$ y no del tipo >= o <=
3. El vector de recursos $\vec{b}$ es no negativo
4. $\vec{x}$ es no negativo

## Transformaciones

### De minimización a maximización

Dado $\min z = C^T*x$ -> negamos el signo tal que:
$$\max z' = -C^T*X$$
### Transformar el vector de recursos $\vec{b}$ 

$$\sum_{j=1}^{n} a_{ij} x_j \leq b_i \overset{\text{T}}{=} -\sum_{j=1}^{n} a_{ij} x_j \geq b_i$$

### Variables de holgura

Si un recurso se acota:
- *superiormente*: $+$ $$\sum_{j=1}^{n} a_{ij} * x_j \leq b_i \rightarrow \sum_{j=1}^{n} a_{ij} * x_j + S_i = b_i $$
- *inferiormente*: $-$ $$\sum_{j=1}^{n} a_{ij} * x_j \geq b_i \rightarrow \sum_{j=1}^{n} a_{ij} * x_j - S_i = b_i $$

## Definiciones Formales

**Vector solución**: un vector $\vec{x} = (x_1, x_2, \ldots, x_n)^T$ que resuelve $A*\vec{x} = b$ 

**Solución factible**: un vector $\vec{x} \geq 0$ que resuelve $A*\vec{x} = b$ 

>[!NOTE]
>Si tenemos una matriz $n \geq m$, degeneraremos ciertos elementos de $\vec{x}$ para facilitar la implementación del algoritmo.

**Solución factible *básica***: un vector $\vec{x_b} \geq 0$ que resuelve $B_{m*m} * x_b = b$

>[!CAUTION]
>Para que haya solución, la base debe de ser invertible

>[!Teorema]
>Dada $\max z = C^T * x$ la solución se encontrará sí o sí en uno de los puntos factibles de $F$
***

