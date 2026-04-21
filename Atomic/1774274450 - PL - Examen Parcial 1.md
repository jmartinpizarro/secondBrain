---
aliases:
  - PL - Examen Parcial 1 
tags:
"References":
cssclasses:
---
# PL - Examen Parcial 1 

**Problema 1.**
**Apartado a**

```
1. S -> ACBSC
2. S -> lambda
3. A -> nM
4. A -> a
5. M -> zA
6. M -> t
7. B -> zB
8. B -> lambda
9. c -> nC
10. c -> n
```

FIRST(C): n
FIRST(B): lambda, z
FIRST(M): z, t
FIRST(A): n, a
FIRST(S): lambda, n, a

---

SIG(S): $, n
SIG(A): n $\cup$ SIG(M)
SIG(M): SIG(A)
SIG(B): n, a
SIG(C): z, n, a $\cup$ SIG(S)

R1. 
SIG(A): FIRST(CBSC) - lambda: n
SIG(C): FIRST(BSC) - lambda: z - lambda $\cup$ FIRST(SC) $\cup$ FIRST(C): z, n, a
SIG(B): FIRST(SC) - lambda: n, a - lambda $\cup$ FIRST(C): n, a
SIG(S):  FIRST(C) - lambda: n
SIG(C): SIG(S)

R3.
SIG(M): SIG(A)

R5.
SIG(A): SIG(M)


Por lo que:

SIG(S): $, n
SIG(A): n
SIG(M): n
SIG(B): n, a
SIG(C): z, n, a, $

**Apartado b**

```
1. A -> bB
2. A -> Aa - RI
3. B -> cB - ambiguedad
4. B -> c - ambiguedad
```

Para quitar la RI de A:

A -> bBA'
A' -> aA' | lambda

Para quitar la ambigüedad de B:
B -> cB'
B' -> B | lambda

---


**Problema 3.**

```
0. S' -> S
1. S -> E
2. E -> [ L ]
3. L -> E Q
4. L -> Q
5. Q -> , E
```

