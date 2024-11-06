---
aliases:
  - Inicialización y finalización de conexiones
tags:
  - review
"References":
cssclasses:
sr-due: 2024-10-29
sr-interval: 11
sr-ease: 270
---
# Inicialización y finalización de conexiones

Antes de **empezar la conexión**, se realiza el siguiente proceso:
1. Se quiere establecer la conexión, *el cliente* envía un segmento especial sin datos de la capa de aplicación. 
2. El servidor, al recibirlo, reserva recursos para la conexión y envía un ACK que incluye:
	- $SYN$
	- $ACK = \text {client\_isn} + 1$ 
	- Número de secuencia del servidor $server\_isn$ 
3. El cliente también asigna recursos necesarios (como el tamaño de la ventana) y envía un tercer fragmento: $server\_isn+1$ en el campo ACK.

Antes de **cerrar la conexión**, se realiza el siguiente proceso:
1. El cliente envía un segmento de apagado al servidor, con el bit indicador de $FIN$ a 1.
2. El servidor envía un segmento ACK al cliente.
3. El servidor envía un segmento de apagado al servidor, con el bit indicador de $FIN$ a 1.
4. El cliente envía un segmento ACK al servidor.
***