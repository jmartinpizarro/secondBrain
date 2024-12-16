---
aliases:
  - Búsqueda y espacio de estados
tags:
  - review
"References":
cssclasses:
---
# Búsqueda y espacio de estados

**Espacio de estados**: 
- *Estados*: configuraciones posibles del problema
- *Operadores*: permiten transitar entre estados (funciones, métodos...)
- *Restricciones*: encargadas de limitar el problema

En este tipo de problemas, siempre tendremos que implementar la función *descendants*:
```C++
vector <state_t> descendants(const state_t node){}
	"Function that given a state (node), it returns all its adjacent states in a     vector of states"
	if <condition>
		then <efectos>
```

**Espacio de problemas**:
- *Un espacio de estados*: lo modelizamos como un $G(V, E)$
- *Un estado inicial $S$*: modelizado como un estado `state`
- *Al menos un estado final $t$ (target)*: modelizado como un estado `state`. Este estado se puede definir:
	- Explícitamente: queremos resolver un problema de optimización
	- Implícitamente:: querer resolver un problema de decibilidad.

1. Resolver problemas -> $G_p(V, E)$ -> $T_G(s, t)$, donde $T_G$ es un árbol
2. Los árboles tienen dos características principales:
	1. $b$: factor de ramificación.
	2. $d$: profundidad. Distancia hasta la meta más cercana.
3. Algoritmos de búsqueda: dado un grafo $G(V, E)$, desarrolla $T_G(s, t)$.
	- Completitud: garantiza que encontrará una solución dado que exista alguna
	- Admisibilidad: garantiza que encontrará una solución óptima, dado que exista alguna

>[!NOTE]
>Un vértice es la ocurrencia de un estado en un grafo. En los árboles, estos vértices se llamarán nodos.


***