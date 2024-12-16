---
aliases:
  - Búsqueda de Fuerza Bruta
tags:
  - review
"References":
cssclasses:
---
# Búsqueda de Fuerza Bruta

## Pseudo-código de los algoritmos de fuerza bruta

1. Generar el nodo inicial $S$.
2. Expandir el primer nodo de la LISTA y añadir sus SUCESORES a LISTA.
3. Si la META $t \in \text{SUCESORES}$, HALT. En otro caso, volvemos al paso 2. 

>[!DANGER] Transposiciones
>Existen varias maneras de ir de un nodo a otro.

## Primero en Amplitud

Nunca expande un nodo a profundidad $d$ hasta que no ha expandido todos a la profundidad $d - 1$. 

LISTA es una COLA o QUEUE.

Es un *algoritmo completo*: garantiza por construcción que va a encontrar una solución al problema. 

Es un *algoritmo admisible*: por definición, el algoritmo descarta todos los nodos con profundidad $d - 1$ cuando está expandiendo nodos en $d$. Entonces, de encontrar una solución, siempre será la más óptima.

$b$ es el número de nodos generados.

 Complejidad temporal: $O(b^d)$
 Complejidad en memoria: $O(b^d)$

## Primero en Profundidad

Expande el primero de los nodos recién generados hasta que se encuentra la meta o se alcanza una profundidad máxima $d_{max}$.

LISTA es una PILA.

*No es un algoritmo completo*: si un nodo solución existe más allá de la profundidad máxima no lo encontraremos.

**Como no es completo, no es admisible.**

Complejidad temporal: $O(b^d)$
Complejidad en memoria: $O(d)$

## Profundización iterativa (Iterative Deepening)

Dado el algoritmo Primero en Profundidad, si no encontramos la solución, aumentamos $d_{max}$ en $k$ y repetimos el algoritmo desde cero. 

*Es completo*.
*Es admisible* solo y solo sí $d_{max} = 1$ y $k = 1$, ya que así no perdemos ningún nodo entre profundidades. 

Complejidad temporal: $O(b^d)$
Complejidad en memoria: $O(d)$

## Ramificación y acotación en profundidad (DFBnB)

Usado cuando el problema tiene diversos costes, ya no existe una relación inequívoca entre la profundidad en la que nos encontramos y el coste.

$g(\pi)$, donde $\pi$ es un camino $\rightarrow$ secuencia ordenada de estados; donde cada estado es alcanzable mediante el uso de un operador. El siguiente ejemplo se corresponde a un *modelo aditivo*.
$$g(\pi) = \sum_{i=0}^{k=!} C(n_i, n_{i+1})$$
$$\pi = <S = n_0, n_1, ..., n_k = t>$$

Al encontrar una primera solución $B$, vamos comprobando el coste de los siguientes nodos. Si encontramos que el valor actual es mayor que $B$, podemos podar esa parte del árbol, ya que la posible solución no será la más óptima.


***