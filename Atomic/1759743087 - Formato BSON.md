---
aliases:
  - Formato BSON
tags:
"References":
cssclasses:
---
# Formato BSON

Conocido como **Binary JSON**. Se basa en el formato JSON (JavaScript Object Notation):
- Ligero, simple y eficiente para grandes volúmenes de datos
- Subconjunto del lenguaje JavaScript.

Un fichero BSON puede contener la definición de **uno o más objetos o documentos**.

Un objeto BSON es una lista ordenada de elementos agrupados por llaves y separados por comas.

Cada elemento sigue una tripleta `<nombre, tipo, valor>`.
- Nombre es una *string*
- El tipo es implícito: asociado al valor y no a la variable

## Tipos

- Simples: entero, real, string, bool, null, date
- Especiales: expresiones regulares, JS code
- Compuestos
	- Otro objeto: definición de otro documento distinto referenciándolo por su nombre
	- Array de objetos

>[!NOTE]
>MongoDB distingue de mayúsculas y minúsculas incluso cuando el SO no lo hace.

