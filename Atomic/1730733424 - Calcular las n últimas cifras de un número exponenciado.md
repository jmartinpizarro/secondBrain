---
aliases:
  - Calcular las n últimas cifras de un número exponenciado
tags:
  - review
  - matemáticaDiscreta
References: 
cssclasses:
---
# Calcular las n últimas cifras de un número exponenciado

A efectos prácticos, es dividir entre 10, 100, 1000... Obtendremos una expresión tal que
$$a^b \space \text{mod n}$$
Como $n$ no será primo, tenemos que usar una variación de Fermat que usa Euler tal que:
$$\phi(n) = m \rightarrow a^m \space \text{mod n}$$
Pero no hemos acabado. Hacemos la división de $b / m$ y hacemos que:
$$a^{b \cdot m} *a^r \space \text{mod n}$$
donde $r = \text{resto de la división de b/m}$. De nuevo, hemos simplificado la operación.  
***