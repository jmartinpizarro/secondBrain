# Envío con errores y pérdidas

El mecanismo previamente mencionado (véase las soluciones mencionadas a los errores de bits), este sistema se queda estancado esperando unos paquetes que nunca llegarán.

**Solución**: incluir un temporizador.

1. El emisor envía un paquete, empezando un temporizador.
2. Si pasados $X$ segundos no se recibe ninguna respuesta por parte del receptor, se asume que el paquete no ha llegado.
3. El emisor repite el mensaje.

Esto puede acarrea una serie de problemas que pueden ser solucionados:
- Todavía existen los duplicados -> pueden ser descartados al estar numerados.
- El temporizador espera exactamente **1 RTT** (Round Trip Time).
	- La única variable que puede cambiar el RTT es el retardo de cola -> **el último paquete no es un buen indicativo de lo que tardará el siguiente**
	- RTT es una estimación, puede fallar
- Con el primer paquete:
	- Empezamos con un RTT muy pequeño que se irá aumentando.
	- Empezamos con un RTT muy grande que se irá reduciendo.

## Problemas de rendimiento

El sistema tiene problemas de rendimiento debido al tiempo de espera del RTT que puede conllevar. 

Se puede resolver permitiendo **varios paquetes al mismo tiempo**: seguir enviando paquetes aunque no hayamos recibido ACKs de los primeros paquetes.
