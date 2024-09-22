# Métodos de cifra moderna

Podemos distinguir dos grupos principales de algoritmos:
- Clave simétrica: una sola clave. Aquí están los algoritmos de flujo y de bloque
- Clave asimétrica: con una clave pública y otra privada.

# Características de los algoritmos de flujo

1. Descomponen el mensaje en bits tal que:
$$M = m_1, m_2, ..., m_n$$
2. Cifran cada $m_i$ con el correspondiente $k_i$ de la serie cifrante, idealmente infinita y aleatoria
$$K = k_1, k_2, ..., k_n, k_{n+1},...$$
3. El resultado sería el siguiente:
$$E_k(M) = E_{k_1}(m_1) E_{k_2}(m_2)... E_{kn}(m_n)$$

# Tipos de cifradores de flujo

Podemos encontrar dos tipos:
- Síncronos: emisor y receptor se sincronizan externamente (no son dependientes o se usan en el algoritmo)
- Asíncronos: emisor y receptor se sincronizan automáticamente (son dependientes de ellos mismos en el algoritmo)

## Ventajas de los cifradores de flujo

- Ventajas:
	- Transformación byte a byte -> altas velocidades de cifrado
	- Los errores de transmisión no se propagan
- Desventajas:
	- Escasa difusión de información (cada símbolo $M$ corresponde con uno $C$)
	- Series cifrantes no son realmente aleatorias #pseudoaleatorio, #generación-determinista
	- [[Problemas de reutilización de clave]] 

# Vernam

Cifrado de Vernam, es un tipo de cifrado de flujo arcaico y teórico. Se demostró que es **incondicionalmente seguro** si la clave k:
- Es realmente aleatoria
- Se usa solo una vez
- Es de longitud igual o mayor que M

Consiste en combinar el mensaje y un flujo constante totalmente aleatorio del mismo tamaño que la clave mediante la operación XOR para cifrar el mensaje. 
El cifrado sigue la siguiente fórmula:
$$E(M) = M \oplus K = m_1 + k_1,\space m_2 + k_2, \space ... \space, \space m_n + k_n$$
Mientras que el descifrado sigue esta otra:
$$M = E(M) \oplus K$$
Es computacionalmente imposible, no somos capaces de generar alfabetos **aleatorios**, solamente **pseudo-aleatorios**. Al ser pseudo-aleatorios, la #entropía no es máxima y por ende no es incondicionalmente seguro.

**Otro problema** de este algoritmo (y de aquellos puramente aleatorios) es que no somos capaces de replicar una clave aleatoria. Entonces, es imposible descifrar el mensaje.
#vernam 

# Postulados de Golomb

Condiciones necesarias pero no suficientes para las secuencias pseudoaleatorias parezcan aleatorias.

Hay dos formas para generar una *serie cifrante* de manera pseudoaleatoria:
- Mediante un generador de números pseudoaleatorios (generación determinista)
- A partir de una clave base (secreta y aleatoria) de centenas de bits para evitar ataques de fuerza bruta.

Sobre las propiedades de Golomb:
- G1: Debe de existir el mismo número de 0 que de 1. Se acepta como máximo una diferencia de un 0.
- G2: La mitad de las rachas (sucesión de dígitos iguales) tiene longitud 1, la
cuarta parte tiene longitud 2, la octava longitud 3, etc
- G3: Para todo k, la Auto-correlación fuera de fase AC(k) es igual a una constante.

**Auto-correlación**: desplazamiento de la secuencia $S$ de período $S$ de $k$ bits hacia la izquierda.
$$AC(k) = \frac{(A - F)}{T}$$
donde $A = Aciertos$ y $F = Fallos$

En la teoría, una serie cifrante debería tener ciertas propiedades deseables:
- Período muy grande
- Aleatoriedad
- Impredecibilidad:
	- Se puede calcular su complejidad lineal $LC$. Se calculan $L$ bits, si se conoce $2L$ bits se puede predecir el resto de la serie.

# LFSR

Es conocido como **Registro de desplazamiento con realimentación lineal** (Linear Feedback Shift Register). 

![[Pasted image 20240918071533.png]] 

donde:
$$n = \text{número de celdas del registro}$$
$$f(x) = a_4x⁴+a_3x³+a_2x²+a_1x+1$$
Es un polinomio donde cada término con incógnita corresponde a una celda del registro. El coeficiente $A$ solo puede ser 0 o 1. La elige el usuario.
$$\text{Función única}: XOR \space \oplus$$
$$\text{Período máximo} = T_{max} = 2^n -1$$
$$Semilla: \text{valores iniciales de cada celda}$$

![[Pasted image 20240918072236.png]]

El **LFSR** tiene períodos muy altos, pero una *complejidad lineal muy baja*. ¿Solución? Aumentar la complejidad usando varios LFSR:
- Operaciones lineales de secuencias pseudoaleatorias
- Operaciones no lineales de secuencias pseudoaleatorias
- Filtrado no lineal de los estados del LFSR

# Entropía

No sabemos probar que algo es aleatorio (computacionalmente), pero *sí podemos probar que algo no es aleatorio* -> rechazamos las series aleatorias, pero aceptamos aquellas que no nos den motivos para pensar que no son aleatorias



