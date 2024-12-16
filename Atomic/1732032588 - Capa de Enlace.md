---
aliases:
  - Capa de Enlace
tags:
  - review
"References":
cssclasses:
---
# Capa de Enlace

Permite que dos nodos conectados a un medio puedan conectarse entre ellos siempre que estén adyacentes entre ellos.

Los switches sirven para no tener que utilizar un bus. No se considera un nodo, *sino un cable*. Los puntos de acceso wifi (que no routers) se consideran lo mismo.

Las **tramas** son los paquetes que se trabajan en esta capa, que provienen de los datagramas.

Se implementan a través de tarjetas o antenas (componente físico). Es ahí donde se generan procesan y envían las tramas.

## Servicios de la capa de enlace

- *Framing*: encapsular un datagrama en una trama, añadiendo la cabecera y la cola. La dirección MAC en la cabecera identifican el emisor y el receptor. El canal es un medio compartido, se pueden generar colisiones.
- *Transmisión de información de manera eficiente entre nodos adyacentes*: los links sin conexión física tienden a tener una tasa de errores altas.
- *Control de flujo*: usado para que un receptor lento no se vea abrumado por un emisor rápido. Muchos no lo implementan
- *Detección y corrección de errores*: para mejorar la fiabilidad. Usamos [[Checksum]] entre otros. Algunos protocolos son capaces de **corregir** el error.
- *Half-Duplex y Full-Duplex*: en la primera, los nodos no pueden transmitir simultáneamente entre ellos. En la segunda, sí que se permite una comunicación bidireccional al mismo tiempo.

## Protocolos y múltiples conexiones entre nodos

Existen dos tipos de links:
- Punto a punto 
- Broadcast

### Protocolo de acceso multiple ideal

1. Cuando un nodo quiere transmitir, lo hace a una velocidad constante $R$
2. Cuando $M$ nodos quieren transmitir, lo hacen a una velocidad constante $R/M$.
3. La conexión es totalmente descentralizada

### Protocolos MAC

Encontramos tres clases:
- **Particionamiento del canal**: dividimos el canal en piezas más pequeñas, guardando una para cada nodo. Por tiempo o por frecuencia.
- [[1732036403 - Acceso Aleatorio|Acceso Aleatorio]]: el canal no se encuentra dividido, permite colisiones y métodos de recuperación a estas.
- **Por turnos**: los nodos tienes turnos, los nodos con más mensajes tendrán turnos más largos
***