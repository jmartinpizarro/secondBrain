---
aliases:
  - Principios de nivel de red. Circuitos virtuales y datagramas. Arquitectura de un router.
tags:
  - review
  - "#ip"
  - retardos
References: 
cssclasses:
---
# Principios de nivel de red. Circuitos virtuales y datagramas. Arquitectura de un router. 

Un router se encarga principalmente de dos funciones: **reenvío** y **enrutamiento**. El retardo de procesamiento está relacionado con el enrutamiento.

Cabe destacar que un router solo tiene *hasta los tres primeros niveles de red*:
1. Físico
2. Enlace
3. Red

**Maximum Transfer Unit**: also known as MTU. Es el máximo número de bytes que puede procesar por dicha tecnología (fibra, cable...). Si se recibe un paquete de mayor tamaño, no se procesa, se borra.

Para permitir que todos los paquetes sean capaces de atravesar la red, usaremos la [[1728401119 - Fragmentación de IP|Fragmentación de IP]].

## Pre-Router Control Plane

Una tabla que tiene cada router que se encarga de enrutar cada paquete a su destino. Todas las tablas tienen una red $0.0.0.0$, la genérica (esta la usamos cuando no sabemos a qué IP pertenece).

Está dividida en varias columnas:
- Prefijo destino: dirección IP del destino (red de destino)
- Interfaz de salida: salida de un router
- Siguiente salto: interfaz receptora del router receptor

Esta tabla se puede editar de manera:
- Local: cada administrator maneja su router
- Software (SDN - Software Defined Network): cuando un administrador maneja muchos routers en una LAN.

## Direccionamiento IP

Todo dispositivo que se conecte a internet tiene una dirección IP *dependiente de la conexión en ese momento*.

>[!NOTE]
>Un router tiene una dirección IP por cada red que conecta.

>[!CAUTION]
>Una dirección IP del tipo V4: $80.22.32.1$ . Todos esos números deben de ser *convertidos a binarios de 8 bits*. El rango máximo de la V4 es de $[0.0.0.0, 255.255.255.255]$

>[!BUG]
>Las direcciones IP no pueden ser únicas, es computacionalmente imposible. Para ello tenemos:
>- IP del tipo V6: una versión IP mejorada que permite más IPs
>- Direccionamiento privado: son direcciones reservadas, no se pueden usar en el internet. Dentro de cada red (con una IP), podemos usar IP que sean solamente válidas para dicha red pública.

**Máscara de red**: las direcciones IP disponibles van a ser $2^n$ donde $n$ es igual al número de ceros totales que tenemos.

Por ejemplo: $255.255.255.128 \rightarrow 255.255.255.10000000$ 
Tenemos  $2⁷$ posibles IPs, pero tenemos que reservar siempre 2:
- La de menor valor -> el ID de la red
- La de mayor valor -> dirección de broadcast

## Formato del datagrama

![[EstructuraDatagrama.png]]

TTL o Time To Live suele ser una serie de saltos máximos que, si no llega el paquete a su destino en esos saltos, se pierde en la red. 











***