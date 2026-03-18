---
aliases:
  - Arquitectura Cloud
tags:
"References":
cssclasses:
---
# Arquitectura Cloud

**Solución IoT**: significa un producto o servicio de un extremo a otro, o una combinación de ambos.
**Aplicación IoT**: se refiere a software o una aplicación móvil (o ambos). Más limitado que la solución IoT, ya que no engloba todo.

![[Pasted image 20260223113012.png]]

### Dispositivos

Sensores y actuadores físicos. Miden varios parámetros y los traducen a datos eléctricos o digitales. Estos sensores están conectados/integrados a los dispositivos *host*. Son **nodos críticos** de una aplicación de IoT y deben ofrecer una funcionalidad de solución completa actuando como entradas, salidas o ambas.
- **Sensores y actuadores**: captan datos del entorno físico, como temperatura o movimiento y los convierten en señales eléctricos.
- **CPU**
- **Memoria**
- **Interfaz de comunicación**: permite que el dispositivo se conecte a otros dispositivos o internet para enviar/recibir datos. 
- **Unidad de alimentación**

### Comunicaciones

Las **puertas de enlace** son dispositivos de borde que permiten comunicar sensor-sistema de dos posibles manera: con o sin puerta de enlace.

Algunos dispositivos permiten la conexión a internet a través del protocolo IP, lo que simplifica la integración de la comunicación de estos módulos usando REST, MQTT, AMQP, CoAP...

Otros dispositivos no tienen este tipo de puerta de enlace, lo que hace que se comuniquen a través de otro dispositivo externo para enviar a sus datos a la capa ascendente. Esto implica tecnologías de comunicación dual, lo que implica que pueden comunicarse de manera ascendente y descendente (GSM y RF, GSM y Bluetooth...)

#### Capa de enlace

Determinan cómo se envían físicamente los datos a través de la capa física o el medio de la red. 

**Ethernet**: es un conjunto de tecnologías y protocolos que se utilizan principalmente en redes LAN.

**WiFi**: forma parte del conjunto de protocolos LAN IEEE y especifica el conjunto de protocolos de control de acceso al medio (MAC) y capa física. 

**Wi-Max**: usado para redes metropolitanas inalámbricas. Especializado en acceso inalámbrico de banda ancha punto a multipunto.

#### Capa de red

Responsable del envío de datagramas IP desde la red de origen a la red de destino. La capa de red realiza el direccionamiento del host y el enrutamiento de paquetes.

**IPv4**: una dirección de protocolo de internet es una etiqueta numérica asignada a cada dispositivo conectado a una red informática que utiliza el protocolo de Internet para la comunicación.

**IPv6**: actualización del IPv4 que permite poder añadir más direcciones IP (128 bits). Destinado a sustituir a su predecesor.

#### Capa de transporte

**TCP** y **UDP**

#### Capa de aplicación

**HTTP**

**WebSocket**

**MQTT**: protocolo de conectividad máquina a máquina (M2M - IoT). Se diseño como un transporte de mensajería extremadamente ligero y útil para conexiones con ubicaciones remotas en las que se requiere un código de tamaño reducido. Se ejecuta sobre la pila de redes TCP/IP.

**XMPP**: Protocolo Extensible de Mensajería y Presencia (XMPP) es un protocolo de comunicación para *middleware* orientado a mensajes basado en XML. Permite el intercambio casi en tiempo real de datos estructurados pero extensibles entre dos o más entidades de red.

**AMQP**: consisten en un conjunto de componentes rígidos y rápidos que enrutan y guardan mensajes dentro de un transportista intermediario, con un conjunto de políticas para conectar los componentes entre sí.

