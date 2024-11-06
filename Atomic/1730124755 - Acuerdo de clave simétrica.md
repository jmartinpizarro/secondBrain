---
aliases:
  - Acuerdo de clave simétrica
tags:
  - review
  - "#diffieHellman"
References: 
cssclasses:
---
# Acuerdo de clave simétrica

## Establecimiento de clave simétrica con criptografía de clave pública

Dados dos entidades $A$ y $B$, queremos **intercambiar una clave**.
1. $A$ elige un $p$ número primo muy grande, un $g$ número generador de $G(p)$ y una $x_A \in G(p)$
2. $A$ calcula $y_A$, un parámetro público de $A$ ($y_A = g^{x_A} \space \text{mod p}$)
3. Similarmente, $B$  elige un $p$ número primo muy grande, un $g$ número generador de $G(p)$ y una $x_B \in G(p)$
4. $B$ calcula $y_B$, un parámetro público de $B$ ($y_B = g^{x_B} \space \text{mod p}$) y además tiene $y_A$
5. Ambos son capaces de calcular una clave $k = y_B^{x_A} \space \text{mod p} = y_A^{x_B} \space \text{mod p}$. Esto se puede resumir en $$k = g^{x_B^{x_A}} = g^{x_A^{x_B}}$$
La seguridad del algoritmo de establecimiento (o intercambio) de clave de Diffie-Hellman se basa en:
- Calcular $x$ conociendo solo $y$ es un problema computacionalmente difícil.
- Calcular $K$ solo conociendo $y_A$ e $y_B$ es un problema computacionalmente difícil.

También tiene ciertas **vulnerabilidades**:
- No es resistente frente  a los ataques activos, pues *no se incorpora ningún mecanismo de autenticación de las claves compartidas.* Esto permite ataques del tipo **Man in the Middle**. Esto se soluciona con [[1730132002 - Diffie Hellman Autenticado|Diffie Hellman Autenticado]]
- **Forward Secrecy**. Si se compromete la clave privada estática, un atacante sería capaz de generar de nuevo todas las claves de sesión anteriores. Esto se soluciona con DH Efímero autenticado. Esto se soluciona con [[1730132101 - Diffie Hellman Efímero - DHE|Diffie Hellman Efímero - DHE]]
## Diffie Hellman Efímero sobre Curvas Elípticas - ECDHE

El problema de Diffie Hellman se puede resolver también usando [[1730132320 - Curvas Elípticas|Curvas Elípticas]], permitiendo definir el algoritmo de acuerdo de clave secreta sobre curvas elípticas.

De la misma manera que sus otras variantes, este algoritmo debe de ser *efímero* y *autenticado*.



***