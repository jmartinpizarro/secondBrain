El problema recae en cómo transferir datos seguros por un canal inseguro

**Interfaces:**

>[!NOTE] Definiciones
>- **rdt_send()**: función usada para enviar datos por un canal seguro
>- **udt_send()**: función usada para enviar datos por un canal inseguro
>- **rdt_rcv()**: función usada para recibir datos de manera segura
>- **deliver_data()**: función que transporta los datos a la aplicación

- **Las transmisiones de datos son unidireccionales**: donde hay un sistema con un emisor y un receptor. No puede haber ningún mensaje enviado por el receptor. Si queremos que *el receptor pueda enviar mensajes*, implementamos esta mismo modelo hacia el otro lado.
- Nos aseguramos que los datos sean seguros. **No nos aseguramos de la transmisión de los paquetes de reconocimiento**.

Podemos determinar distintos tipos de errores de transmisión en un canal dependiendo del tipo de error (dónde, cómo...):
- [[Envío con errores de bit]] 
- [[Envío con errores y pérdidas]]


Se puede solucionar también con una [[Sliding Window]]. 