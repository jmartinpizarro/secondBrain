---
aliases:
  - Curvas Elípticas
tags:
  - review
"References":
cssclasses:
---
# Curvas Elípticas

Parte $E$ de un cuerpo $K$. Es cúbica, irreducible y no degenerada, definida sobre el plano proyectivo $P²(K)$, sobre el cuerpo $K$, junto con el punto $O \in E(K)$

 Basada en funciones matemáticas fáciles de calcular y revertir.
 >[!CAUTION]
 >Es muy complicado calcular el logaritmo discreto de una curva elíptica
 
 ![[CurvaEliptica.png]]

Hay varios algoritmos que se basan en esta imposibilidad de calcular el logaritmo discreto para sus operaciones:
- ECC acuerdo de clave - ECDH (Elliptic Curve Diffie - Hellman)
- ECC cifrado - ECIES (Elliptic Curve Integrated Encryption Scheme)
- ECC firma digital - ECDSA (Elliptic Curve Digital Signature Algorithm)

*Clave pública*: un punto en la curva
*Clave privada*: la derivada de un número aleatorio $d$ muy grande

Hay una **menor longitud de clave**, además de tener  la misma seguridad y la misma rapidez que otros algoritmos. Sin embargo, **es más complicado de implementar**; requiere un mayor manejo de errores.
***