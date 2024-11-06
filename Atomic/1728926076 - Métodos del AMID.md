---
aliases:
  - Métodos del AMID
tags:
  - review
"References":
cssclasses:
sr-due: 2024-10-19
sr-interval: 4
sr-ease: 270
---
# Métodos del AMID

## Inicio lento

Cuando se inicia la conexión, iniciaremos una ventana de congestión (cwnd) de 1 ms. La aumentaremos exponencialmente hasta llegar a cierto umbral (ssthresh), donde cambiaremos el método para *evitar la congestión*.

Si se finaliza un timeout antes de llegar al ssthresh, el emisor TCP establece $ssthresh = cwnd / 2$ y $cwnd = 1 ms$ comenzando el *inicio lento* nuevamente.

Si ocurre un triple ACK duplicado:
- TCP Tahoe: lo mismo que para un timeout
- TCP Reno: $ssthresh = cwnd / 2$ y $cwnd = sshthresh + 3$. Tras esto entra en modo *recuperación rápida*.

## Evitar la congestion

No podemos aumentar el $cwnd$ exponencialmente todo el rato. A partir del $ssthresh$, lo haremos **linealmente**.

Si no ocurre ningún fallo, por cada RTT aumentaremos el $cwnd$ en 1.

Si encontramos un timeout o un triple ACK duplicado, replicamos lo que ocurre en el *inicio lento*.

## Recuperación rápida

Recomendado pero no obligatorio (TCP Reno los usa, pero TCP Tahoe no). Accedemos a este estado cuando recibimos **triples ACKs duplicados**, donde se estable el $cwnd$ en:
$$cwnd = ssthresh + 3 = \frac{cwnd'}{2} + 3$$
Si recibimos un ACK diferente al duplicado, es que todo ha ido bien, y reestablecemos $cwnd = sshthresh$.
***