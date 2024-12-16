---
aliases:
  - Problema de las n reinas
tags:
  - review
"References":
cssclasses:
---
# Problema de las n reinas

**Problema de las n-reinas:** Dado un tablero de ajedrez de _n_ × _n_, ¿es posible colocar _n_ reinas en el tablero de modo que ninguna de ellas esté en la misma fila, columna o diagonal que otra? Si es posible, encontrar una configuración válida de las _n_ reinas; si no, indicar que no existe tal configuración.

Aunque podemos definirlo de muchas formas, una forma curiosa (y la más óptima) es la siguiente. Asumimos que el tablero tiene un tamaño $n \cdot n$, donde $n = 4$. 

- $x_i \triangleq \text{fila de la reina de la columna i-ésima}$; ya que sabemos que por definición nunca podrá haber dos reinas en una misma columna
- $R = \{1 \leq a_i \leq 4\}$; donde $a_i$ es una constante del dominio genérica
- $R_{1, 2} = \{(1,3), (1,4), (2,4), (3,1), (4,1), (4,2)\}$

Tenemos que hacer las restricciones para $R_{1,3}, R_{1,4}, R_{2,3}, R_{2,4}, R_{3,4}$


***