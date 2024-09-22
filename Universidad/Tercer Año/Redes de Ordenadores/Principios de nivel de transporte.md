# Capa de Transporte VS Cada de Red servicios y protocolos

- Capa de Red: comunicación lógica entre hosts.
- Capa de Transporte: comunicación lógica entre procesos.

## Acciones de la capa de transporte (UDP)

- Emisor:
	- se pasa un mensaje de la capa de aplicación
	- determina el valor de la cabecera del segmento
- Receptor:
	- recibe el mensaje desde la IP
	- comprueba los valores de la cabecera
	- extra el mensaje de la capa aplicación
	- demultiplexea el mensaje
