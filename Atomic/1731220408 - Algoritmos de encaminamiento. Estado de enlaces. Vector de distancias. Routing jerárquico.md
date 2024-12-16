---
aliases:
  - Algoritmos de encaminamiento. Estado de enlaces. Vector de distancias. Routing jerárquico
tags:
  - review
"References":
cssclasses:
---
# Algoritmos de encaminamiento. Estado de enlaces. Vector de distancias. Routing jerárquico

**Forwarding**: direcciona los paquetes a la siguiente salida del router
**Routing**: se encarga de seleccionar la ruta a un destino más óptima 

Hay dos formas de estructurar el plano de control de una red:
- Control Pre-Router (tradicional): cada router debe interactuar con todos los routers del plano para poder ejecutar el algoritmo.
- Control lógico centralizado (definido por software): se instalan tablas de salida en los routers

## Protocolos de enrutamiento

Dada una heurística denominada coste, podemos definir un algoritmo que nos seleccione la ruta más óptima entre dos puntos para no saturar la red.

Dependiendo del tipo de algoritmo que usemos, podrá tener una serie de características:
- Global: todos los nodos tienen información de los restantes, computacionalmente costoso. *Algoritmo Dijkstra*.
- Descentralizado: los nodos solo tienen información de sí mismos y sus vecinos, por lo que deben intercambiarse la información constantemente. *Algoritmo del vector distancia*.
- Estático: la red cambia muy poco/lentamente a lo largo del tiempo.
- Dinámico: la red se encuentra constantemente en cambios, saturando al algoritmo.

### Algoritmo de Dijkstra 

Algoritmo centralizado e iterativo. Implementamos el algoritmo de Dijkstra modificado, donde calculamos el menor coste de un nodo hasta todos los posibles.

*Complejidad del algoritmo*: $O(n) \space \text{nodos}$, con una complejidad de $O(n²)$, aunque hay algoritmos más eficientes del tipo $O(n \cdot log(n))$

*Complejidad del mensaje*: cada router debe de hacer un broadcast al resto para que obtengan su estado, complejidad $O(n)$.

### Algoritmo del Vector Distancia

Se basa en la ecuación de Bellman-Ford, relacionada con la programación dinámica.
$$D_x(y)=min_v \{c_{\text{x,v}} + D_v(y)\}$$
La idea es conocer la información del propio nodo y que sus vecinos adyacentes le trasladen la información del resto de manera iterativa. Es un algoritmo que debe de ejecutarse constantemente, y asíncrono (ya que toma valores de la iteración anterior).




***