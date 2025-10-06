---
aliases:
  - Reducción de penalización de fallos
tags:
"References":
cssclasses:
---
# Reducción de penalización de fallos

A lo largo del tiempo, ha incrementado la distancia entre el rendimiento de la DRAM y la CPU -> coste de penalización de fallo creciente.

- Hacemos la caché **más rápida**.
- Hacemos la caché **más grande**.

## Cachés multinivel

### Tasa de fallos local

Fallos en un nivel de la caché con respecto a accesos a ese nivel de caché.
$$L1 \rightarrow m(L1)$$
$$L2 \rightarrow m(L2)$$
### Tasa de fallos global

Fallos en un nivel de caché con respecto a todos los accesos de memoria.
$$L1 \rightarrow m(L1)$$
$$L2 \rightarrow m(L1) \cdot m(L2)$$

### Tiempo medio de acceso

$$t_a(L1) + m(L1) \cdot t_f(L1) =$$
$$t_a(L1) + m(L1) \cdot (t_a(L2) + m(L2) \cdot t_f(L2))$$

## Prioridad de fallos de lectura sobre escritura

Reduce la penalización de fallos; evitando que un fallo de lectura tenga que esperar a que una escritura termine.

- **Cachés de escritura inmediata**: bufer de escritura contiene una modificación del dato que se lee.
- **Cachés con post-escritura**: fallo de lectura podría reemplazar a un bloque modificado.