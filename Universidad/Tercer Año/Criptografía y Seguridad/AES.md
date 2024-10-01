---
aliases: 
cssclasses: 
tags:
  - AES
---
# AES: el algoritmo

Implementa criptografía simétrica. Usa la tecnología de los [[Cifradores de bloques]]. 
- Opera sobre bloques de 16 bytes (128 bytes)

Acepta tres longitudes de clave: 128, 192 (menos usado) y 256 bits. Se generar siempre subclaves o claves internas de 128 bits.

>[!WARNING]
>Es una red de sustitución-permutación, no una red Feistel.
>

Rápido tanto en software como en hardware, fácil de implementar y requiren poca memoria.

Se basa en *cuatro funciones invertibles*, aplicadas en un número determinado de rondas, a los bytes de una matriz llamada *Estado*.

La *Matriz Estado* se carga inicialmente con los bytes del bloque de entrada de las subclaves.

## Esquema de propagación

Hay un total de 10 rondas, sin contar la inicial. En ellas se ejecutan hasta cuatro funciones para cifrar. A la hora de descifrar, se usan las inversas de dichas funciones:
- [[AddRoundKey]]: añadimos una clave de vuelta al estado
- [[ByteSub]]: sustitución de un byte usando una *tabla S-Box*
- [[ShiftRow]]: desplazamiento de filas de un estado
- [[MixColumns]]: mezcla de datos dentro de cada columna

![[PropagacionAEs.png]]

## Operaciones con bytes

La unidad mínima con la que operar es el **byte**. La suma y la multiplicación se calculan usando [[Cuerpos de Galois]]. 

Para la reducción de polinomios usaremos:
$$p(x) = x⁸+ x⁴+x³+x+1$$
Nótese que este polinomio (al igual que todas las funciones usadas para cifrar), están demostradas matemáticamente que son las más óptimas.

## Expansión de la clave

La clave no es suficientemente larga para usarse las rondas necesarias, ergo necesita ser expandida para poder ser usada.
- 10 rondas para AES128
- 12 rondas para AES192
- 14 rondas para AES256

Usando S-Box y una constante de ronda (que incluye la no linealidad), somos capaces de modificar la clave original. Añadiendo sustitución y varias iteraciones, somos capaces de expandir la clave.

