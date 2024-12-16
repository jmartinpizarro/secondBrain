---
aliases:
  - Acceso Aleatorio
tags:
  - review
"References":
cssclasses:
---
# Acceso Aleatorio

## ALOHA v2

Dividimos todas las tramas al mismo tamaño. Generamos ranuras de tiempo, donde una ranura $=$ tiempo que tarda en enviarse una trama.

Si queremos enviar un paquete, esperamos a la siguiente ranura y enviamos. Si dos o más nodos deciden transmitir en la misma ranura, se produce colisión. Si ha habido una colisión, el receptor no mandará un ACK, los emisores entenderán que deben repetir el mensaje.

El problema recae en el reloj centralizado.

## CSMA - Carrier Sense Multiple Access

Al enviar una trama:
- Si el canal está libre, envías.
- Si el canal está ocupado, escuchas y esperas a que se quede libre

No evita colisiones, pero sí que las reduce drásticamente.

## CSMA/CD - Collision Detection

Emitimos y escuchamos al mismo tiempo:
- Si finalizamos y hemos escuchado lo mismo que lo emitido, todo ha ido bien.
- Si emitimos pero escuchamos otra cosa, detectamos una colisión antes de tiempo. Podemos detenernos. Esperamos un tiempo aleatorio y reintentamos.

No es necesario implementar ACKs. Es fácil de implementar en cable, pero muy difícil en radio.
***