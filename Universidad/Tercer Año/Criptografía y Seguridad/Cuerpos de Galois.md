# Cuerpos de Galois

Sea $Z_p = \{0, 1, 2, \dots, p - 1\}$ siendo $p$ un número primo y $\forall x \neq 0 \in Z_p$ $x$ es un primo relativo respecto a $p$ (coprimo), entonces:

**Existe $x^{-1}$ respecto al módulo $p$**. Hay $p$ elementos dentro de $CG(p)$.  

$Z_p$ es un *cuerpo finito* denominado *Cuerpo de Galois ($CG(p)$)*

## Operaciones con cuerpos de Galois $CG(q^n)$ 

(A, +, $\cdot$) con A = $Z_p$:
- $+$ : AxA -> A
	a, b -> $(a+b) (mód \space p)$

- $\cdot$ : AxA -> A
	a, b -> $(a \cdot b)(mód \space p)$

## Cuerpos de Galois $CP(2^n)$

Estos serán los cuerpos con los que principalmente trabajaremos.
Cada elemento $a(x) \in CG(2^n)$ se representa mediante coeficientes $a_i = {0, 1}$ 

El número de elementos de este cuerpo es $2^n$, donde usaremos $n$ bits para representar un elemento.

Esto significa, matemáticamente, que seremos más óptimos al usar $CG(2^n)$ que al usar $CG(p)$.
- Mientras que usamos $2^n$ bits, con el polinomio usamos $n+1$ bits (más números, menos óptimo)
- Aprovecha toda la capacidad de la representación electrónica
- Cálculos inversos más rápidos
- 

