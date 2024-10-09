Tenemos dos problemas principales:
- Ataque con texto original conocido: se puede obtener $K$ si tenemos $M$ y $C$
$$M \oplus C = M \oplus M \oplus K = K $$
- Ataque solo al criptograma: $M_i$ a partir de $C_i$ y $C_j$ escogidos si $M_j$ predecible.
$$C_i \oplus C_j = M_i \oplus K \oplus M_j \oplus K = M_i \oplus M_j$$
