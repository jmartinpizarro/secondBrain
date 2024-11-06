---
aliases:
  - Integridad y autenticación con criptografía simétrica
tags:
  - review
  - hash
  - mac
References: 
cssclasses:
sr-due: 2024-10-29
sr-interval: 15
sr-ease: 294
---
# Integridad y autenticación con criptografía simétrica

## Funciones Resumen

También conocidas como *funciones hash*. Es una función que acepta un bloque de datos $M$ de longitud variable y genera un resumen (hash) de longitud fija.

$$H(M) = Hash$$

El resumen, de tamaño limitado, *identifica de manera única* dicho mensaje.

>[!CAUTION]
>Estamos hablando de resumen -> *integridad*. Esto no tiene nada que ver con confidencialidad.
>

### Colisión

Espacio de resúmenes $h$ para una función resumen dada:
$$|h| = 2^n$$
Entonces, es posible *que un mensaje $M$ y $M'$ tal que sean iguales, y por lo tanto haya una colisión*.

$$H(M) = H'(M) = colisión$$

### Funciones resumen criptográficas

Funciones resumen que deben de cumplir ciertos requisitos:
- **Difusión**: si se modifica un solo bit del mensaje $M$, el resumen debería cambiar la mitad de sus bits aproximadamente.
- **Determinista**: la aplicación de la misma función resumen sobre los mismos datos debe de producir el mismo resumen
- **Eficiente**: tanto en implementaciones hardware y software.

### Resistencia de una función resumen

Una función resumen debe de ser resistente a:
- **Resistente a preimágenes**: dado un resumen $h$, debe de ser computacionalmente imposible encontrar un mensaje $M'$ tal que:
$$M'/ H(M') = h$$
- **Resistente a segunda preimagen (resistencia débil a colisiones)**: dado un mensaje $M$, es computacionalmente imposible encontrar un $M'$ tal que el resumen de ambos coincidan:
$$M' \neq M / H(M) = H(M')$$
- **Resistente a colisiones (resistencia fuerte a colisiones):** es computacionalmente imposible encontrar dos mensajes M y M’ tales que sus resúmenes coincidan:
$$M \neq M' / H(M) = H(M')$$

La fortaleza de una función resumen radica en que *su diseño sólo permita ataques por fuerza bruta (no criptoanalizable)*. Además, *n (longitud del resumen) debe de ser lo suficientemente grande*.

### Probabilidades de encontrar una colisión (posibles ataques)

- Ataque de preimagen: $$\frac{1}{2^n}$$
- Ataque de segunda preimagen: $$\frac{1}{2^n}$$
- Ataque de colisión:$$\frac{1}{2^{n/2}}$$

### Ejemplos de Hashing

Tenemos varios ejemplos de funciones hash. Los más relevantes son:
- [[1728313596 - Estructura Merkle-Damgärd|Estructura Merkle-Damgärd]]
- [[1728313662 - MD5|MD5]]
- [[1728313719 - Familia SHA|Familia SHA]]

## Códigos de autenticación de mensajes

### Generalidades MAC

Algoritmo que emplea una clave secreta sobre un mensaje de longitud variable para generar un valor de longitud fija.

Cualquier entidad con la clave puede *verificar* la integridad del mensaje.

### Requisitos seguridad MAC

- Dado un mensaje $M$ y el valor $MAC(K, M)$, es computacionalmente imposible encontrar un mensaje $M'$ cuyo valor $MAC(K, M')$ coincida.
- $MAC(K, M)$ debe estar uniformemente distribuido, de forma que la probabilidad de encontrar dos mensajes $M$ y $M’$ cuyos valores $MAC$ coincidan es $\frac{1}{2^n}$
- Sea $M'$ un mensaje resultante de aplicar una transformación $M [M' = f(M)]$. En tal caso, se debe de cumplir que: $$Pr[MAC(K, M) = MAC(K, M')] = \frac{1}{2^n}$$
- Ataques de fuerza bruta:
	- Ataques al espacio de claves
	- Ataques al valor MAC
- Ataques de criptoanálisis:
	- Require la existencia de vulnerabilidades en el diseño o en el algoritmo.

Nos podemos encontrar **dos tipos de MAC**:

- [[1728313824 - MAC basados en funciones resumen|MAC basados en funciones resumen]]
- [[1728313907 - MAC basados en cifradores de bloque|MAC basados en cifradores de bloque]]

## Cifrado Autenticado

Proporcionar tanto confidencialidad, integridad y autenticidad en las comunicaciones. Usamos tanto *cifrado simétrico* como *MAC*

Tenemos tres tipos distintos:
- Encrypt-then-MAC: alta seguridad si la MAC es la adecuada
- Encrypt-and-MAC: existe *un problema*: el mismo texto genera la misma MAC
- MAC-then-encrypt: verificar la integridad require que se descifre primero

## Modos de operación de cifrado autenticado

### Cifrado autenticado y modos de operación

Proporcionar al mismo tiempo **confidencialidad, integridad y autenticidad**. Son similares a los cifradores simétricos, pero introduciendo elementos de autenticación:

- GCM Gaulois Counter MODE (AES con GCM)
- Poly1305 (CHACHA20 con Poly1305)

### GCM

Extensión del modo de operación [[1729418366 - CTR - Counter Mode Encryption|CTR - Counter Mode Encryption]] , incluyendo autenticación. El cifrado se realiza como un CTR. Se añade una función MAC con operaciones en cuerpos de Galois.

En paralelo al CTR se realiza la autenticación, que es una multiplicación en $CG(2^{128})$. 

![[GCM Galois Counter Mode.png]]

## Poly1305

Es un MAC con funciones resumen. Muy rápido, ya que usa [[1729418856 - ChaCha20|ChaCha20]] (algoritmo de flujo). 

El cifrado ocurre a partir del bloque 1 usando un contador.

El *Auth Tag* se genera a partir de:
1. Se combina el texto cifrado con ChaCha20 y Auth Data.
2. Se aplica Poly1305 sobre el resultado
3. La clave que usa Poly1305 para genera el Auth Tag se obtiene en el bloque 0.

## Comunicaciones seguras - TLS

Hereda del protocolo de redes [[1728882855 - TCP|TCP]], habilitando el cifrado de datos. Cualquier comunicación HTTPS se realiza con TLS, que se encarga de crear un canal seguro para la transmisión.

Aporta:
- Confidencialidad
- Autenticación
- Integridad

Para negociar el canal seguro TLS permite negociar al cliente y al servidor unas condiciones de seguridad, llamadas [[1729419322 - Suites de Cifrado|Suites de Cifrado]]






***