# Algoritmos de Transposición
## Transposición por grupos

- Escítala: al enrollar en el papel y escribir, a la hora de descifrar el bastón debía de ser del *mismo diámetro* para que funcionase.


## Transposición por series

Ordenar mensaje como cadena de submensajes transpuestos.
$$Message\text{\scriptsize main} = Message\text{\scriptsize 1} + Message2\text{\scriptsize proc} + ... + Message\text{\scriptsize 3}$$


## Transposición por columnas/filas

Rizar el rizo de la transposición de series. Dada una serie de columnas (donde el mensaje está escrito), permutarlas para cambiar el mensaje

# Algoritmos de Sustitución
## Sustitución mono-alfabeto monográfica

Dado un único alfabeto inicial, generar un algoritmo donde una letra sea el equivalente a otra (el algoritmo de César). Hay varios tipos de algoritmos:

- Cifrados de desplazamiento puro (tipo César, ROT 13...):
$$E(m\text {\scriptsize i}) = (m\text {\scriptsize i} + b) \space mod \space n $$
- Cifrado por decimación pura (ROT 13):
$$E(m_i) = (m_i * a) \space mod \space n$$
- Cifrado por sustitución afín:
$$E(m_i) = (a * m_i + b) \space mod \space n$$

>[!warning]
>Para este tipo de cifrados, un carácter solamente puede equivaler a otro.

Las frecuencias de aparición de los caracteres siempre van a aparecer. Entonces, matemáticamente, el algoritmo no es seguro.

## Sustitución mono-alfabeto poligráfica

Algoritmos como el *PlayFair*, basado en un algoritmo de sustitución por columnas. Usaremos una matriz para distribuir todas las letras del abecedario y usando una palabra base (una clave), podemos sustituir el mensaje.

Otros algoritmos, como el *Hill*, cifran `n` caracteres al mismo tiempo. Utiliza ecuaciones lineales y transformaciones matriciales, donde la propia clave es la matriz.


## Sustitución poli-alfabética

Estos son los casos **periódicos**. Permiten distintos desplazamientos por carácter. Sin embargo, **sigue habiendo una sola clave por carácter**. 

Por ejemplo, a la letra `A` la movemos 3 posiciones, y a la letra `A` (en otro alfabeto distinto) la movemos 5 posiciones. De esta manera, usamos dos alfabetos distintos donde la misma clave puede tener distintos resultados.

El más conocido es el de Vigenère, donde había 27 alfabetos cifrados y 27 cambios siguiendo le método César. La clave tenía una longitud `m`.	
$$E(m_i) = (m_j \space + \space k{\scriptsize (j \space mod \space m)}) \space mod \space 27 $$
donde:
- $k_i = \text{desplazamiento del alfabeto i}$ 
- $m_j = \text{letra texto en claro en posición j}$
- $E(m_j) = \text{letra cifrada}$
### Sustitución poli-alfabética progresiva

El mayor exponente es la máquina Enigma. Máquina eléctrico-mecánica, formado por varios rotores. Cada vez que se introducía una letra, la posición del rotor cambiaba. Cuando el primer rotor daba una vuelta entera, el de su izquierda rotaba una vez.


Este tipo de algoritmos son usados especialmente en los [[Cifradores de bloques]].
