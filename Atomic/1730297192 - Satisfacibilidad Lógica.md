---
aliases:
  - Satisfacibilidad Lógica
tags:
  - review
  - "#lógica"
References: 
cssclasses:
---
# Satisfacibilidad Lógica

Las *proposiciones* que usaban los antiguos filósofos griegos se llaman ahora *variables*, tal que $x_1 = \text{True} = 1$ es una variable. Las variables pueden ser de negación tal que $\overline{x_1} = \text{False} = 0$.

En lógica proposicional se tiende a usar $p \rightarrow q = p \lor q$, **disyunción de literales**.

Una fórmula normal está en **forma normal conjuntiva** si: $\land_{i=1}^N \lor_{j=1}^N l_{ij}$

Se denomina **modelo** $M$ a la definición de variables de una fórmula para que dicha fórmula se cumpla. Por ejemplo:
$$M = x_1 = \perp, x_2 = T, ..., x_n = \perp/T$$
$$donde \perp = False \space \text{y T = True}$$
>[!NOTE]
>Un literal es puro si su negación no pertenece a la fórmula (si tenemos $x_1$, no podemos tener $\overline{x_1} \space \text{en el resto de la fórmula}$)

**Tautología**: fórmula proposicional siempre cierta en cualquier asignación de sus expresiones atómicas tal que: $F = x_1 \lor \overline{x_1}$

**Contradicción**: algo que no puede ser cierto, que no tiene sentido tal que: $F = x_1 \land \overline{x_1}$. Entonces $Res(F, x_1) = \emptyset \lor \emptyset = \{\emptyset\}$    


$$Res(F, l) = \begin{cases}  F &  l \notin F \\ F \backslash l & l \in F \space \text{y l es puro} \\ (C_1 \lor C_2) & l \in F, \text{l no es puro}\end{cases}$$
$$\text{F = Formula y l = Literal}$$

Si $F = (x_1 \lor \overline{x_2} \land (\overline{x_1} \lor \overline{x_2} \lor x_3))$, entonces $Res(F, \overline{x_2}) = \emptyset$.     

**1-SAT**: problema que se resuelve en tiempo lineal $O(n)$. Este problema tiene la forma de:
$$x_1 \land \overline{x_2} \land \overline{x_1} \space ... \space \land x_n$$
**2-SAT**: problema que se resuelve en tiempo cuadrático $O(n²)$
$$(\overline{x_1} \lor x_2) \land (x_1 \lor \overline{x_3}) \space ...$$
Para resolver problemas del tipo *exponencialmente difíciles* usaremos el [[1730301854 - Algoritmo de Davis-Putnam|Algoritmo de Davis-Putnam]]

Una modificación de este algoritmo mucho más efectiva es la del [[1730301910 - Algoritmo de Davis-Putnam-Logemann-Loveland|Algoritmo de Davis-Putnam-Logemann-Loveland]].
Estos algoritmos tienen una complejidad $O(2^n)$, ya que la propia naturaleza de un problema booleano es de complejidad exponencial.

***