---
tags:
  - AES
---
# MixColumns

Opera sobre columnas, consideradas como un polinomio del tipo $CG(2⁸)$, multiplicando por cada columna por el polinomio fijo:
$$a(x) = x⁴+1, \text{donde los valores \{\} están en hexadecimal}$$
$a(x)$ es primo relativo de $x⁴+1$, asegurando el inverso.
$$a(x) = \{03\}x^3 + \{01\}x^2 + \{01\}x + \{02\}$$
Recuerde que $\{03\} = x + 1$, $\{02\} = x$  

![[OperatingMixColumnsEj.png]]
