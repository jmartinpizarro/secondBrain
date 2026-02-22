---
aliases:
  - Análisis Léxico
tags:
"References":
cssclasses:
---
# Análisis Léxico

**Frontend**: depende del lenguaje
**Backend**: depende de la máquina.

![[Pasted image 20260209151811.png]]

Es posible tener el:
- Analizador Léxico
- Analizador Sintáctico
- Analizador Semántico
dentro del frontend.

El optimizador se basa en heurísticas.

---

El analizador léxico pide leer un *token*. El léxico le devuelve un *token*. Se comprueba que esté en la tabla de símbolos y luego se continua. 

Para leer el léxico se usa:
- Expresiones Regulares: `id: [a-zA-Z][a-zA-Z0-0]*`
- Gramáticas de Tipo 3

## Definiciones

**Tokens**: permite que el traductor/compilador/intérprete trabaje con agrupaciones de caracteres como una unidad, considerando estas agrupaciones como terminales de la gramática.
- Palabras reservadas
- Identificadores
- Números
- Cadenas de caracteres
- Comentarios: NO son tokens

**Lexema**: secuencia de caracteres del código fuente que se identificada como una unidad con significado léxico.
$$<num, 345.2>$$

**Análisis Lineal**: la cadena de entrada de lee de izquierda a derecha, y se agrupa en componentes léxicos (tokens). 

## Funciones

- Manejar el fichero fuente
- Leer los caracteres de la entrada
- Eliminar los comentarios/delimitadores
- Generar una secuencia de componentes léxicos (tokens)
- Relacionar los mensajes de error con las líneas del programa fuente
- Introducir identificadores en la tabla de símbolos
- Controla si es de formato libre o no (sigue indexación o no)

### Reconocimiento de palabras reservadas

Se guardan en la tabla de símbolos, donde dicho componente léxico equivale a un lexema y una descripción es única.

Por ejemplo:
*While (pal. res.)* -> while -> "while"
Numero -> 3.141, 0 -> `[0-9]⁺\.[0-9]⁺`

## Construcción

Se definen los diagramas de transición, AFDs generalizados con las siguientes características:
- Las transiciones pueden estar etiquetadas por un símbolo, un conjunto de ellos o una ER
- Algunas estados de aceptación pueden devolver el último símbolo dado que no pertenece al token requerido.
- Los estados de aceptación realizan la acción de devolver el token

A la hora de convertir un AFD en un analizador léxico, solo nos interesan las transiciones útiles, no las sumidero!

**Obtención de un DT**:

1. Toda expresión regular tiene un AFND asociado
2. Conversión de AFND a AFD
3. Minimización del AFD
4. Adaptación a un DT
5. Generación de un programa/simulador de DT

En caso de error (el analizador léxico detecta un error):
1. Anotar el error
2. Recuperarse:
	1. Ignorar
	2. Borrar
	3. Insertar
3. Seguir

Un programa con $K$ errores: hacen falta $K$ cambios para poder ser correcto.