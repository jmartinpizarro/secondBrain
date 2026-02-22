---
aliases:
  - Análisis Sintáctico
tags:
"References":
cssclasses:
---
# Análisis Sintáctico

El compilador está conformado por:
- Léxico
- Sintáctico
- Semántico

El sintáctico se basa en, usando los tokens que le proporciona el léxico, los parsea y genera el árbol sintáctico.

Para todo el proceso en el que el parser le pide al analizados léxico un token, se usa el **Análisis Descendente** o  el **Análisis Ascendente**

## Introducción

1. El analizador sintáctico llama al analizador léxico y demás componentes del compilador
2. Tanto para el análisis descendente y ascendente: **la entrada se lee de izquierda a derecha**.
3. Las gramáticas usadas serán LL y LR (cómo se deriva)
	1. $LL(k) \in LR(k)$ ($k$ es el número de tokens, leídos anticipadamente)
	2. En la práctica solo se usa $k=1$

**Funciones**:
- Comprobar que la secuencia de componentes léxicos es una sentencia válida de un lenguaje.
- Generar el árbol sintáctico

>[!DANGER]
>Los diagramas de sintaxis son muy útiles. Y a Webber le gustan mucho :)

**Notación BNF - Backus Naur Form**

### Formalismos

Ventajas de usar una gramática vs hand-coded parser.
- Especificaciones sintácticas precisas de un lenguaje
- Mantenible

**Derivación**: aplicación de una producción a una forma sentencial. Tras cada derivación se obtiene una forma sentencial

**Orden de derivación**:
- Derivación más a la izquierda: en la forma sentencial, se sustituye primero el símbolo No Terminal más a la izquierda.
- Derivación más a la derecha: en la forma sentencial, se sustituye primero el símbolo No Terminal más a la derecha.

**Regla Compresora $A \rightarrow \lambda$**: se emplea para elementos que son opcionales. Puede aparecer al factorizar una gramática.

$S := aB \space | \space a$
---
$S := aX$
$X := \lambda \space | B$

**Analizador Sintáctico**: toma una sentencia $w$ (secuencia de tokens) y produce una derivación representable con forma de árbol.

>[!NOTE]
>Cuestiones clave:
>- Como se reconoce que $w \in L(G)$
>- Error si no existe un árbol para $w$
>- ¿Existe ambigüedad?


**Se debe de evitar siempre la ambigüedad**:
1. No hay técnicas generales
2. Es imposible convertir automáticamente una gramática ambigua en una no ambigua
3. Algunos parsers proporcionan facilidades para tratar la ambigüedad.
4. Se permite una gramática ambigua si (según Araceli esto es mentira):
	1. Simplifica la gramática para representar un lenguaje
	2. Permite definiciones más naturales
	3. Pero exigen mecanismos para resolver ambigüedades (otra mentira)

**El analizador sintáctico**:
1. Controla las llamadas al Analizador Léxico
2. Comprueba la corrección estructural de la entrada
3. Inserta las acciones semánticas y la traducción

**Criterios de diferenciación**:
1. Derivación del NT
	1. más a la izquierda vs derecha en la forma sentencial (LL vs LR)
2. Generación del árbol de derivación: Derivación del NT
	1. De forma descendente vs Ascendente (Top Down vs Bottom Up)
3. Recursivo vs Tabla
4. Predictivos de $k$ elementos: se leen de forma anticipada $k$ elementos léxicos de la secuencia de la entrada para predecir la derivación adecuada.


## Análisis Sintáctico Descendente

Se aplican derivaciones.
No vale la recursividad a izquierdas.

Sea $x$ una secuencia de tokens.
Pertenece al lenguaje definido por la gramática $G$ si genera una sentencia del lenguaje.
1. Iniciar la forma sentencial con el axioma
2. Tomar un token de izquierda a derecha
3. Seleccionar una regla de producción
4. Si coinciden token y símbolo de la forma sentencial, leer siguiente token
5. Sustituir el símbolo no-terminal más a la izquierda (Left Most Derivation) por la parte derecha
6. Repetir el proceso hasta que la entrada ha sido procesada

**Descenso Recursivo**: consiste en una serie de funciones pequeñas
Cada función:
- Representa a un No Terminal que aparece en la parte izquierda de las producciones
- Realiza el proceso de Análisis que definen las producciones
- Llama a las funciones delos NT que aparecen a la derecha de las producciones
- Hace llamadas recursivas cuando hay recursividad en las producciones -> **backtracking**
## Análisis Sintáctico Ascendente

Se aplican reducciones.
Vale la recursividad a izquierdas.
