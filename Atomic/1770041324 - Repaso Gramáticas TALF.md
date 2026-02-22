---
aliases:
  - Repaso Gramáticas TALF
tags:
"References":
cssclasses:
---
# Repaso Gramáticas TALF

Un alfabeto se representa tal que $\sum = \{0, 1\}$, donde $0, 1$ son los valores que el alfabeto tiene.
- Un alfabeto cerrado incluye $\sum^* = \{\lambda, 0, 1, 00, 11, 10, ...\}$
- Un alfabeto cerrado estricto incluye $\sum⁺ = \{0, 1, 00, 11, 10, ...\}$

Por lo tanto $\sum^* = \sum^+ \cup \{\lambda\}$

**AFD/DFA -> Autómatas Finitos de Estado**

![[Pasted image 20260202153439.png]]

El autómata anterior es determinista, pero si fuese no determinista (un mismo input puede dirigir a dos estados distintos), existiría un problema - se vuelve un problema exponencial.

Existe un algoritmo para convertir un autómata no determinista en uno determinista. Usualmente los autómatas deterministas son lenguajes de tipo 3.

Para hacer lenguajes de programación se requieren lenguajes de tipo 2.

Para ello **AP/PDA -> Autómatas de Pila**. Estos autómatas son, casi siempre, no deterministas y no existe un algoritmo para convertirlos en no deterministas: $O(B^n)$

## Gramáticas ##

$G = \{\sum_T, \sum_N, S, P\}$

donde:
- $\sum_T$ es el alfabeto de terminales
- $\sum_N$ es el alfabeto de no terminales
- $S$ es el axioma
- $P$ son las reglas (producciones)

---

**Representación de una gramática tipo 3**

$N \rightarrow w$ 
donde:
- $N \in \sum_N$
- $w \in (\sum_T \cup \sum_N)^*$
- $w$ es un terminal, un terminal seguido de un no terminal o de un no terminal seguido de un terminal o $\lambda$

Forma sentencial: contiene no terminales
Palabra: no contiene terminales

>[!DANGER]
Recursividad por la izquierda y doble recursividad siempre prohibidas!

