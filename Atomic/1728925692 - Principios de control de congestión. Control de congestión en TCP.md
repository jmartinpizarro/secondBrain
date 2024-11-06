---
aliases:
  - Principios de control de congestión. Control de congestión en TCP
tags:
  - review
"References":
cssclasses:
sr-due: 2024-10-19
sr-interval: 4
sr-ease: 270
---
# Principios de control de congestión. Control de congestión en TCP

Demasiadas fuentes envían mensajes de manera muy rápida a un mismo receptor. Los síntomas suelen ser largos retrasos y pérdida de paquetes (buffers llenos).

>[!CAUTION]
>El control de congestión ocurre cuando varios dispositivos envían a un solo receptor. El control de flujo ocurre cuando un solo dispositivo envía paquetes muy rápido a un solo receptor

### Casos y consecuencias de la congestión

#### Escenario 1

El más simple. Dos emisores y receptores a través de un router. Podemos sacar conclusiones del tipo:
1. La máxima velocidad de conexión será $\frac{R}{2}$.
2. Cuando mayor sea el nivel de datos, mayor es el retardo de manera exponencial.
![[CongestionEscenario1.png]]
#### Escenario 2

Igual que el primero, pero los emisores retransmiten los paquetes perdidos. Pueden darse varias situaciones:
1. El emisor tiene *conocimiento perfecto* del espacio libre del buffer. Podemos evitar pérdidas. De nuevo, la velocidad de conexión es $\frac{R}{2}$.
2. El emisor tiene *algún conocimiento parcial* del espacio libre del buffer. Aunque puede haber pérdidas, el emisor sabría cuándo reenviar el paquete.
3. El emisor *no tiene conocimiento* del espacio libre del buffer. Podríamos tener duplicados innecesarios y pérdidas de paquetes.
![[CongestionEscenario2.png]]

#### Escenario 3

Este escenario es más complejo, ya que podemos encontrar:
- Cuatro remitentes
- Timeouts y retransmisiones
- Rutas con múltiples saltos

Si todos los hosts enviasen a máxima velocidad, la red colapsaría.
![[CongestionEscenario3.png]]

Entonces, podemos sacar unas **conclusiones generales** de estos escenarios.
1. El rendimiento no excede la capacidad
2. El retardo aumenta a medida que se acerca a la capacidad
3. Las pérdidas y las retransmisiones reducen el rendimiento efectivo
4. Los duplicados innecesarios reducen el rendimiento efectivo 
5. Desperdicio de la capacidad de transmisión por la cantidad de paquetes (duplicados).

### Enfoques de control de congestión

- **Control de congestión extremo a extremo**: la congestión se infiere a partir de las perdidas de paquete y los retardos observados. Usado por TCP.
- **Control de congestión asistido por la red**: los routers envían retroalimentación a los hosts con los flujos de datos que atraviesan el router congestionando. Se indica la congestión con un solo bit.

## Control de congestión TCP - AIMD

**AIMD**: algoritmo en el que los remitentes aumentan progresivamente la tasa de envío hasta que se detecta congestión/pérdida de un paquete, momento en el que se disminuye la tasa de envío. 

Los [[1728926076 - Métodos del AMID|Métodos del AMID]] se encargan de varias la tasa de envío de manera exponencial, lineal o inicializadora.
***