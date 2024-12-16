---
aliases:
  - Programación Dinámica
tags:
  - review
"References":
cssclasses:
---
# Programación Dinámica

Existen cuatro técnicas de programación
- Recursividad: recursividad simple, recursividad por la cola, por la cabeza, recursividad arbitrariamente grande...
- Divide and Conquer
- Programación Voraz
- Programación Dinámica

*Asuma que queremos calcular una forma de obtener el número binomial de $\binom{n}{k}$*. Sabemos que:

$$\binom{n}{k} = \frac{n!}{k! \cdot (n-k)!}$$
```c++
unsigned long long int bc(int n, int k){
	return fact(n) / (fact(k) + fact(n-k))
}
```

Pero este código NO funciona (no óptimamente). Estamos trabajando con factoriales de número exageradamente grandes; por lo que no somos capaces de terminar de ejecutar estos.

Pero también sabemos que:

$$\binom{n}{k} = \binom{n-1}{l} + \binom{n-1}{k-1}$$
```c++
unsigned long long int bc2(int n, int k){
if (n == k) || (k==0){
	return 1;
	} 
	return bc2(n-1, k) + bc2(n-1, k-1)
}
```

Aunque es óptima, es una técnica de programación recursiva. Si usamos programación dinámica, la idea es cachear los valores previamente calculados en una tabla bidimensional de tamaño $i x j$ tal que podemos representar los coeficientes binomiales en la tabla:

| ---  | pos0 | pos2 | pos3               | pos4             | pos5 |
| ---- | ---- | ---- | ------------------ | ---------------- | ---- |
| col0 |      |      |                    |                  |      |
| col1 |      |      |                    |                  |      |
| col2 |      |      | $\binom{i-1}{j-1}$ | $\binom{i-1}{j}$ |      |
| col3 |      |      |                    | $\binom{i}{j}$   |      |
| col4 |      |      |                    |                  |      |
| col5 |      |      |                    |                  |      |

Tal que para un valor en la fila $i$ y la columna $j$, solamente tenemos que sumar el valor de la fila anterior (misma columna) y de la fila y columna anterior.

## Problema de la mochila

Suponga que queremos meter una serie de objetos en un maleta con un volumen máximo:
$$V(x) = \min\{c(x, a) + V(T(x, a))\}$$
$$C, w(0), \delta(0) \rightarrow \text{objeto con un peso y una importancia}$$
Entonces, podemos hacer:
$$V_{i, j} = max\{V_{i, j-1}, V_{i-w(j)}, \delta(j)\}$$

## Algoritmo de Bellman-Ford-Moore

Dado un grafo $G(V, E)$ y $C: e \in E \rightarrow \mathbb{Z}$; calcular el coste de la solución óptima desde $s \in V$ hasta todos los demás.

```python
def bellmanFordMoore(s, V, E):
	d = [M] * len(V)
	d[s] = 0
	for v in len(V) - 1:
		for e in E:
			d[e.V] = min(d[e.v], d[e.u] + e.e)
	if d[e.v] + e.e < d[e.u]:
		raise Error
```

## Algoritmo de Floyd-Warshall

Dado un grafo $G(V, E)$ y $C: e \in E \rightarrow \mathbb{Z}$; calcular el coste óptimo entre cualquier par de vértices.

```python
def floydWarshall(V, E):
	for i in V:
		for j in V:
			d[i][j] = M if i != j else 0
	for e in E:
		d[e.u][e.v] = e.e
	for k in len(V) - 1:
		for i in V:
			for j in V:
				d[i][j] = min(d[i][j], d[i][k] + d[k][j])
```

***