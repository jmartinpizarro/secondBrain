---
aliases:
  - Ejercicio - Introducción a la creación de un Compilador
tags:
"References":
cssclasses:
---
# Ejercicio - Introducción a la creación de un Compilador

![[Pasted image 20260202200122.png]]

**Palabra Reservada**: palabras que pueden colisionar con la definición de otras palabras, pero que tienen prioridad. En este caso, *main*, es una palabra reservada.

Axioma: Programa -> *main*  Código  .
Código -> Sentencia; Código | Sentencia 
Sentencia -> Lectura | Escritura | Asignación
Lectura -> leer  VAR
Escritura -> imprimir VAR
Asignación -> VAR := EXPRESIÓN
EXPRESIÓN -> VAR | NUMERO | EXPRESIÓN OPERADOR EXPRESIÓN \ (EXPRESIÓN) (doble recursividad no permitida, aquí lo permitimos *for the sake of complexity*)
OPERADOR -> + | -  | * | /
VAR -> Letra | Letra RestoVAR
RestoVAR -> Letra | Dígito | Letra RestoVAR | Dígito RestoVAR
Dígito -> 0 | 1 | ... | 9