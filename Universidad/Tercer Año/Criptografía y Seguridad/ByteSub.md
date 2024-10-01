---
tags:
  - AES
---
# ByteSub

Dada una tabla $S-Box$ (siempre es la misma), somos capaces de cambiar la matriz por un número hexadecimal equivalente.

![[SBox.png]]

El nuevo valor del vector columna puede ser calculado tal que:

![[OperatingByteSub.png]]

Donde el inverso del valor de entrada es un campo de Galois (en este caso esta columna corresponde al inversor de $\{63\}_{16}$). La otra matriz corresponde con una matriz probada matemáticamente por ser la más óptima.

![[OperatingByteSumEj.png]]