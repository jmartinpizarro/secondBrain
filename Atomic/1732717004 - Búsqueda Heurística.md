---
aliases:
  - Búsqueda Heurística
tags:
  - review
"References":
cssclasses:
---
# Búsqueda Heurística

```c++
int h (const state_t n){
	...
	return
}
```

**Admisibilidad**: $h(n) \leq h^*(n)$
**Consistencia**: $h(n) \leq h(n_i) + C(n, n_i)$ (específica para grafos teledirigidos)

La función heurística debe de devolver 0 cuando está en la meta.

Si una heurística es consistente, entonces es admisible. 

No todos los problemas tienen funciones heurísticas.

## Relajación de restricciones

Método usado para generar heurísticas

1. Dado un problema real
2. Dadas sus restricciones
3. Relajamos las restricciones (una combinación de ellas)
4. Resolver óptimamente el problema relajado

Entonces, $h(n) = h_r^*(n) \leq h^*(n)$

Las mejores heurísticas son obtenidas con una relajación de restricciones mínima.

## Algoritmo de Escalada (Hill-Climbing)

Elegimos de todos los sucesores el nodo que sea más prometedor, heurísticamente hablando, y eliminamos el resto de memoria.

Memoria: $O(d)$

No es un algoritmo completo, ya que juzgamos a los nodos dependiendo del valor heurístico (que puede no ser correcto realmente).

No es un algoritmo admisible.

Este algoritmo es usado cuando tenemos problemas con un alto factor de ramificación.

## Búsqueda en haz (Beam Search)

Parámetro $k$: número de nodos simultáneamente expandidos.

El parámetro $k$ define el número de nodos máximos posiblemente óptimos a expandir y los expande. Pero todavía no se evalúan heurísticamente (los recién generados). Una vez que tiene todos los sucesores, se queda otra vez con los $k$ mejores de dicho nivel de profundidad. 

Memoria: $O(k \cdot d)$

No es un algoritmo completo, ya que juzgamos a los nodos dependiendo del valor heurístico (que puede no ser correcto realmente).

¿Es admisible? Con $k = 1$, tenemos el algoritmo de escalada. Si $k = \infty$, tenemos el algoritmo de amplitud. Es altamente modificable, dependiendo de la $k$.  Aun así, siempre existe la posibilidad que juzguemos a un nodo mal y lo perdamos. No, no es admisible.

## El Mejor Primero

Es completo y admisible.

Consumo de memoria y consumo temporal $2^n$.

Especialmente bueno a mayor número de transposiciones.

>[!DANGER] Ha caído siempre en los exámenes finales

1. $\exists$ OPEN: lista de nodos generados esperando a ser expandidos ordenados ascendentemente $f(n)$.
2. $\exists$ CLOSED: lista de nodos ya expandidos.
3. *Terminación*: la terminación ocurre cuando $t$ va a ser expandido. 

$f$ puede ser:
1. $f = h$, lo que en español conocemos como Heurística Pura (Greedy BFS).
2. $f = g$, donde $g = \text{Algoritmo de Dijkstra}$. ¡Dijkstra es un algoritmo de fuerza bruta!
3. Sabemos que tardamos $g$ (unidades del coste que pretendemos minimizar). Cuando llegamos a un nodo $n$ genérico, sabemos su coste desde el nodo $S$. Entonces, estimamos del nodo $n$ al nodo $t$ (con un valor de $h$). Entonces obtenemos el algoritmo $A^*$ que usa la función: 
$$f = g + h; \space h \leq h^*$$

## Iterative-deepening-A* (IDA*)

Algoritmo que combina Profundización iterativa con el $A^*$. Algoritmo sin memoria.
$$\eta_0 = h(s); \space h \leq h^*$$
$$\eta_{i+1} = \min_{n, f(n) > \eta}\{f(n)\}$$
A mayor número de transposiciones, mayor tiempo en completarse.

***