# Introducción

Sea $Z$ un conjunto de números enteros con $a, b, c \in Z$, con las siguientes propiedades:
$$a + b \in Z$$
$$a + (b+c) = (a+b) +c$$
$$a+0 = a$$
$$a + (-a) = 0$$

$Z$ forma una estructura de **Grupo Conmutativo** o **Abeliano** si :
$$a+b = b+a$$
$Z$ forma una estructura de **Anillo** $Z,+, \space .$ si $Z$ es un grupo abeliano y se cumplen las anteriores propiedades.

$Z$ es un **anillo de división** si:
$$a * a^{-1} = 1$$

# Congruencias

Sean $a, b, n \in Z$ donde $n \neq 0$ y $a, b$ son congruentes módulo n tal que:
$$a = b (mód \space n)$$ solo si:
$$a = b (mód \space n) \Leftrightarrow a - b = k * n$$

El **conjunto de posibles restos mód n** es un anillo, un subset donde:
$$Z^* \in [0, n-1]$$
## Cálculo de inversos

Si $a \in Z_n / m.c.d. (a,n) = 1 \text(coprimos)$ ; existe un único $x \in Z_n - \left\{0 \right\}$ tal que: 
$$a*x = 1 (mód \space n)$$ Este valor se representa por:
$$x = a^{-1} (mód n)$$

## Indicador de Euler

- Si $n$ es un número primo $p$:
$$\phi(p) = p - 1$$
- Si $p$ es un número primo y $k \in Z⁺$:
$$\phi(p^k) = p^k - p^{k - 1} = p^{k - 1} (p - 1)$$
- Si $p$ y $q$ son números primos entonces:
$$\phi(p * q) = \phi(p) * \phi(q)$$
- Si $n = \prod_{i} p_i^{k_i} \quad \forall i \, (p_i \text{ es primo}, \, k_i \in \mathbb{Z}^+)$
$$\Phi(n) = \prod_{i} p_i^{k_i - 1} (p_i - 1)$$

Sabiendo esto, podemos aplicar Euler para calcular un inverso:
$$a^{-1} = a^{\phi(n)-1} (mód \space n)$$ cuando se nos pide calcular el inverso de un número (ejemplo):
$$1 = 3x (mód \space 10)$$
$donde a = 3, n = 10$ 