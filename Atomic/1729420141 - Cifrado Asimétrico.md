---
aliases:
  - Cifrado Asimétrico
tags:
  - review
  - matemáticaDiscreta
References: 
cssclasses:
---
# Cifrado Asimétrico

## Aritmética modular: exponenciación y logaritmo discreto

### Restos potenciales y gaussiano

#### Restos potenciales

Dada $a \in \mathbb{Z}$ se llaman **restos potenciales** de $a$ respecto al módulo $n$ a los restos de las potencias sucesivas de $a$ respecto a ese mismo módulo:
$$a⁰ \space \text{mod n}$$
$$a¹ \space \text{mod n}$$
$$a² \space \text{mod n}$$
$$...$$
$$a^g \space \text{mod n}$$
![[RestosPotenciales.png]]
#### Restos Gaussianos

Si $\text{m.c.d(a, n)} = 1$ por Euler, entonces:

Existe al menos un exponente $m$ tal que $a^m = 1 \space \text{mod n}$
$$a^{\phi(n)} = 1 \space \text{mod n} \rightarrow m = \phi(n)$$
El menos exponente $w$ que cumple $a^{w} = 1 \space \text{mod n}$, se denomina **gaussiano de $a$** respecto del módulo $n$. 

El **gaussiano de $a$** respecto a $n$ divide al número de elemento de $\mathbb{Z}_n^*$.
- Si $w = orden(a, n) \rightarrow w \space | \space \phi(n)$  
Por tanto, *solo pueden ser gaussianos de $a$  respecto a $n$, los divisores de $\phi(n)$*.

### Raíces primitivas o generador

Cuando el gaussiano de $a$ respecto de $n$ es igual indicador de Euler ($\phi(n)$), se dice que $a$ es una raíz primitiva o generador de $n$.

Los restos potenciales de las raíces primitivas generan todo el conjunto reducido de restos $Z_n^*$ (elementos con inverso multiplicativo de $Z_n$).

![[RaicesPrimitivas.png]]

### Logaritmos discretos

El cálculo inverso a la exponenciación en la aritmética modular se denomina *logaritmo discreto*. 
$$x = log_a b \space \text{mod n}$$

## Criptosistemas asimétricos de cifrado

Se emplean *pares de claves*:
- Clave pública: conocida por todos, el emisor usa la clave pública del receptor para cifrar mensajes a este
- Clave privada: conocida solamente por el propietario. El receptor la usa para descifrar.

>[!NOTE]
>Tiene que ser **inviable** determinar la clave privada a partir de la pública.

Ofrecen una **gran seguridad computacional**:
- Búsqueda exhaustiva es posible en teoría
- Claves usadas han de ser suficientemente grandees
- Los problemas matemáticos en los que se basan son difíciles (factorización números grandes y logaritmo discreto)

Sin embargo, son muy **lentos en comparación con criptosistemas simétricos**.

## Algoritmo RSA

Se basa en la dificultad de factorizar un número producto de dos grandes primos de similar longitud.

$B$ elige $p_B, q_B \space \text{primos muy grandes, no públicos}$
$B$ obtiene $n_B = p_B \cdot q_B$
$B$ calcula $\phi(n_B) = \phi(p_B) \cdot \phi(q_B)$
$B$ escoge $e_B \in \mathbb(Z)+ / \operatorname{mcd}(e_B, \phi(n_B)) = 1$ 
$B$ calcula $d_B / e_B \cdot d_B = 1 \space \text{mod} \space \phi(n_B)$  

**Clave pública de B**: $K_{\text{U, B}} = (e_B, n_B)$
**Clave privada de B**: $K_{\text{V, B}} = (d_B, n_B)$

### Ataques a RSA

El RSA puede ser maleable, para ello usamos *RSA-OAEP*

Se añade un relleno (padding), y algo de redundancia para que no sean válidos todos los mensajes. Tras el rellenado, se cifra el mensaje codificado:
$$C = (EM)^e \space \text{mod n}$$
***