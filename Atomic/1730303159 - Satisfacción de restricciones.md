---
aliases:
  - Satisfacción de restricciones
tags:
  - review
"References":
cssclasses:
---
# Satisfacción de restricciones

Una **red de restricciones** (una tarea de satisfacibilidad de restricciones) es $X_iD_iC$ donde:
- $X = \{x_i\}_{i=1}^n$ son sus variables
- $D = \{D_i\}_{i=1}^n$ con el dominio de $x_i \in X$
- $C = \{R\}_{j=1}^m$ son las restricciones

Una restricción $R_{ij}$ es una relación binaria entre $x_1 \text{ y } x_j$ que nombra las combinaciones $(a_i, a_j)$ que son permitidas $a_i \in D_i \space \space a_j \in D_j$

Una **instanciación** es una asignación de valores a $S \subset X$ :
- $S \subset X$: instanciación parcial
- $S = X$: instanciación total

**Objetivo**: dada $(X_iD_iC)$ encontrar una instanciación total que sea compatible con todas las restricciones.




***