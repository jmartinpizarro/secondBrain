---
aliases:
  - Sobre condiciones binarias en programación lineal
tags:
  - review
"References":
cssclasses:
---
# Sobre condiciones binarias en programación lineal

Dada una restricción del tipo:
$$x_2 \geq 20 \Leftrightarrow \text{compramos el aparato}$$
Es decir, que existe una variable $b$ que puede ser:
$$x_2 \geq 20 \Leftrightarrow b = 1$$
$$b = 1 \space \text{si compramos el aparato}$$
$$b = 1 \space \text{si no compramos el aparato}$$

Lo que hacemos es crear una contante $M$ que tienda a $\infty$ tal que:
$$b_{ij} - M$$

Si hacemos que $20 \leq x_2 + M *(1-b)$, estaríamos perdiendo algunas condiciones. Por ello, lo que debemos hacer es restar ese posible valor de $b$ al valor restringido de $x_2$:
$$x_2 \leq 19 + M*b$$
***
