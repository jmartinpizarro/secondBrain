# Capa de Transporte VS Cada de Red servicios y protocolos

- Capa de Red: comunicación lógica entre hosts.
- Capa de Transporte: comunicación lógica entre procesos.

## Acciones de la capa de transporte

- Emisor:
	- la capa de aplicación genera un mensaje y lo pasa
	- determina el valor de la cabecera del segmento
	- crea el segmento
	- pasa el segmento a la IP
- Receptor:
	- recibe el mensaje desde la IP
	- comprueba los valores de la cabecera
	- extra el mensaje de la capa aplicación
	- demultiplexea el mensaje y lo envía a la capa de aplicación

## ¿Cómo funciona el demultiplexeo?

Tanto el multiplexeo como el demultiplexeo  se basan en el segmento, las cabeceras del datagrama.
**UDP**: demultiplexeo usando el puerto del destinatario
**TCP**: demultiplexeo usando una tupla de 4 valores, IPs de origen y destino y los puertos.

1. El host recibe el datagrama con la IP
2. El host usa la IP y los puertos para dirigir el segmento al socket correspondiente

Hay que tener en cuenta que puede haber varios sockets. Puede haber un mismo puerto (P:80) con varios sockets que procesen distintos segmentos.

# Transporte contact-less: UDP

Los segmentos de UDP pueden perderse o quedarse fuera de contexto de la app.
- Emisor y receptor no se conectan (no hay handshaking).
- Cada segmento enviado es independiente al resto.

## Acciones de la capa de transporte (UDP)

- Emisor:
	- Pasa un mensaje de la capa de la aplicación
	- Determina las cabeceras del mensaje
	- crea el segmento de UDP
	- Pasa el segmento a la IP
- Receptor:
	- Recibe el segmento desde la IP
	- Comprueba el checksum
	- Extrae el mensaje
	- Lo demultiplexea y lo envía a la capa de aplicación

### UDP Checksum

Tanto el TCP como el UDP usan el [[Checksum]]
Mecanismo que se encarga de comprobar si ha habido algún error durante la transmisión del paquete.

Comprueba el checksum del emisor con el del receptor (usualmente una cadena de 16 bits)