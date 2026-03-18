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

De tipo LR.
Vale la recursividad a izquierdas.
Se aplican reducciones: si tenemos un conjunto de terminales que equivalen a un terminal, este conjunto se convierte en un no terminal.

No se puede reducir todo, solo el **pivote de reducción**, una subcadena que encaja por la parte derecha.

Se basa en acciones **shift-reduce**. Dado el elemento de la pila, y el símbolo de la entrada:
- **Shift**: el siguiente símbolo de la entrada se desplaza a la cima de la pila.
- **Reduce**: elimina los símbolos de la pila cuando encajen con la parte derecha de una producción y los sustituye por el No Terminal de la parte izquierda.
- **Accept**: el parser consigue reducir la cadena de entrada completa
- **Error**: el parser detecta un error y llama a la función de tratamiento.

Estos pasos se repiten hasta lograr el **Accept**, donde la pila contendrá $\{\$, S\}$ y la entrada $\{\$\}$ o hasta que se detecta un error.

Puede generar dos tipos de conflictos:
- shift-reduce: estado en el que el parser no puede determinar si realizar un shift o un reduce
- reduce-reduce: estado en el que el parser no puede determinar qué producción aplicar para realizar un reduce

**Operaciones del parser (de las tablas)**:
- Action: define si se hace un *shift* (y a qué estado) o un *reduce* (reduce una predicción)
- Goto: a qué estado tras una acción

### Analizador LR(0)

No tiene *lookahead*. No sirve para nada, salvo para basarnos en él, podemos construir el SLR(1). Nos basamos en un en un **Autómata Finito Determinista** para poder desarrollarlo.
1. Hay que crear el conjunto canónica $LR(0)$.
2. Asociar acciones a los items de los estados.

#### Item LR(0)

Asuma:
$$S \rightarrow var = num$$
Un item es cada una de las posiciones que puede tener esta regla. Es decir:
$$S \rightarrow \cdot var = num$$
$$S \rightarrow var \cdot = num$$
$$S \rightarrow var = \cdot num$$
$$S \rightarrow var = num \cdot$$
Ese punto indica lo que se encuentra procesado (metido en la pila). Solo cuando el puntero esté al final (todo está procesado) se podrá hacer la reducción (sustituimos la parte derecha por la izquierda).


>[!DANGER]
>Si existe una producción que fuese $A \rightarrow \lambda$, la producción que le corresponde es $A \rightarrow .$

---

- A los estados del AFD se les denomina **conjunto canónico $LR(0)$.
- Un estado del conjunto canónico $LR(0)$ está formado por un conjunto de items.
- El estado inicial del autómata es el que contenga el item del axioma.

>[!DANGER] Superaxioma
>Si **el axioma tiene varias producciones**, no se puede elegir. Para ello se crea un superaxioma, ampliando la gramática tal que:
>$$S' \rightarrow S$$

- La creación de los estados del conjunto canónico $LR(0)$ se apoya en dos funciones
	- Cierre(cerradura, *close*): determina los items que pertenecen a un estado
	- Ir_a(*goto*): genera un nuevo estado a partir de los items de un estado y símbolos gramaticales

Asuma una gramática tal que:
$$S \rightarrow T \mid S \space op \space T$$
$$T \rightarrow num \mid ( \space S \space )$$
Un posible estado de cierre (inicial, del superaxioma) sería:
$$S' \rightarrow \cdot S$$
$$S \rightarrow \cdot T$$
$$S \rightarrow \cdot S \space op \space T$$
$$T \rightarrow \cdot num$$
$$T \rightarrow \cdot ( \space S \space )$$

