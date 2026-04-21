---
aliases:
  - Protocolos para la gestión de nubes de dispositivos IoT
tags:
"References":
cssclasses:
---
# Protocolos para la gestión de nubes de dispositivos IoT

Los protocolos estándar son las herramientas que unen y encapsulan datos sin procesar de un sensor a algo significativo y formateado para que la nube lo acepte. Los más predominantes son **MQTT** y **CoAP**

Estos protocolos se encuentran en la propia capa de aplicación. Usualmente se encuentran fuera del protocolo HTTP, ya que los dispositivos IoT están muy restringidos. 

## Middleware orientado a mensajes

**Middleware Orientado a Mensajes (MoM)**. La comunicación entre dos dispositivos se realiza mediante colas de mensajes distribuidos.

Estos servicios se basan en un servicio orientado a mensajes (MQTT) que utiliza un servidor broker y editores y suscriptores de un evento. La información puede almacenarse o no en colas para una mayor resiliencia.

## RESTful

La alternativa de MoM es RESTful. Un servidor posee el estado de un recursos, pero el estado no se transfiere en un mensaje al servidor desde el cliente.

Utilizan métodos HTTP como GET, PUT; POST, DELETE... para colocar solicitudes en el **Identificador de Recursos Universal (URI)**.

## Protocolo MQTT

Creado para abordar problemas en sistemas distribuidos independientes y no concurrentes - además de comunicarse de forma segura.

- Fácil de implementaer
- Ligero y eficiente en ancho de banda
- Agnóstico respecto a los datos

### Publicación-suscripción

Este tipo de arquitecturas (frente a las de cliente-servidor), se presentan como una alternativa útil para los usos de IoT.

**Es una forma de desvincular a un cliente que transmite un mensaje de otro cliente que recibe un mensaje.** No existen ningún identificador físico (como IP o puerto). Además, no tiene una cola de mensajes (estos se pueden perder o ignorar si no está escuchando).

MQTT son invariantes en el tiempo: un mensaje publicado por un cliente puede ser leído y respondido en cualquier momento por un suscriptor. Un suscriptor podría estar en un estado muy bajo de consumo de energía y responde minutos u horas después de un mensaje.

### Arquitectura

Basado en [[1728882855 - TCP|TCP]]. Es un protocolo basado a la conexión: el cliente establece conexión con el broker antes de la comunicación.

En el centro hay un corredor de MQTT que tiene la responsabilidad de conectar clientes y filtrar datos.
- Filtrado de temas: por diseño, los clientes se suscriben a temas y ciertas ramas de temas y no reciben más datos de los que desean.
- Filtrado de contenido: los corredores tienen la capacidad de inspeccionar y filtrar los datos publicados.
- Filtrado de tipo: un cliente escucha un flujo de datos suscrito también puede aplicar sus propios filtros.
![[Pasted image 20260413173049.png]]

Usualmente se carga un mensaje MQTT con texto JSON o datos binarios. El tamaño máximo es de 256 MB (una carga muy grande).

#### Funcionamiento de la arquitectura del protocolo MQTT

Se basa especialmente en peticiones y en respuestas similares a un ACK (ver [[1728882855 - TCP|TCP]]).

![[Pasted image 20260413173224.png]]

El paquete MQTT se encuentra en la parte superior de la capa TCP, siendo un total de 2 bytes. Puede contener un encabezado de tamaño variable (opcional) y concluye con la carga útil.

**Desconexión inesperada**: existe un contador *keep-alive timer timeout*. Cuando este llega a cero, el servidor deja de publicar a dicho cliente.

### Calidad de servicio

- QoS-0 (transmisión no asegurada): nivel mínimo. Modelo análogo a disparar y olvidar detallado en algunos de los protocolos inalámbricos. Eficiente, pero el receptor puede no reconocer el mensaje o el remitente no puede volver a intentar la transmisión.
- QoS-1 (transmisión asegurada): garantiza la entrega del mensaje **al receptor** a través de un acuse de recibo `PUBACK`.
- QoS-2 (servicio asegurado en aplicaciones): garantiza que tanto el remitente como el receptor han recibido el mensaje.

>[!DANGER] ¿Cuándo usar cada uno?
>- QoS-0: debe usarse cuando no se necesita la cola de mensajes. Conexiones por cable.
>- QoS-1: uso predeterminado.
>- QoS-2: misiones críticas. Retransmisión de un mensaje duplicado puede generar fallos.

### MQTT-SN

Derivado de MQTT para redes de sensores. Mantiene la misma filosofía como un protocolo ligero, pero diseñado para los matices de una red de área personal inalámbrica típica en entornos de sensores.

No requiere de pila TCP/IP. Se suele usar a través de un protocolo de enlace simple. Se puede usar sobre UDP.

- **Puertas de enlace**: responsabilidad de convertir el protocolo MQTT-SN a MQTT y viceversa. Las puertas de enlace también pueden ser agregadas o transparentes.
- **Retransmisores**: ruta entre un sensor y una puerta de enlace. Puede tomar muchos caminos.
- **Clientes** y **servidores**: igual que un MQTT normal.
#### Anuncio y descubrimiento de una puerta de enlace

- ADVERTISE: transmite periódicamente desde una puerta de enlace para anunciar su presencia
- SEARCHGW: emitido por un cliente cuando busca una puerta de enlace particular. 
- GWINFO: respuesta de las puertas de enlace al recibir un mensaje SEARCHGW. Contiene el ID y la dirección de la puerta de enlace, solo se transmite cuando SEARCHGW se envía desde un cliente.

## Protocolo de Aplicación Restringida - CoAP

Diseñado como un protocolo de comunicación para dispositivos restringidos. Es excelente para:
- Proporcionar una estructura similar y fácil de direccionamiento de recursos, familiar para cualquier persona con experiencia en el uso de la web, pero con recursos reducidos y demandas de ancho de banda.
- Proporciona una funcionalidad similar con significativamente menos gastos generales y requisitos de energía.

La forma de usarlo sería tal que: `coap: // host [: puerto] / [ruta] [? consulta]`. Se usan métodos como GET, POST, DELETE...

- **Puntos finales**: orígenes y destinos de un mensaje CoAP. 
- **Proxies**: endpoint al que los clientes de CoAP le asignan la tarea de realizar solicitudes en su nombre.

### Tipos de mensajes
- Confirmable (CON): requiere un ACK. Si se envía con un mensaje CON, se debe de recibir un ACK dentro de un intervalo de tiempo aleatorio.
- No-confirmable (NON)
- Reconocimiento (ACK)
- Reseteo (RST)