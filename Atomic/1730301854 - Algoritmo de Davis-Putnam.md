---
aliases:
  - Algoritmo de Davis-Putnam
tags:
  - review
"References":
cssclasses:
---
# Algoritmo de Davis-Putnam

1. Elegir un *literal* $l \in F$
2. Aplicar $Res(F, l)$ y anotar la variable usada y las cláusulas involucradas
3. Si resulta la cláusula vacía, nos detenemos. **Problema No Satisfacible**
4. Si resulta $F = \emptyset$ ir al paso 5. En otro caso, volvemos al paso 1.
5. **Problema Satisfacible**. Considerar la lista de variables y cláusulas en orden inverso, calculando $T \space o \perp$ para todas las variables involucradas.
***