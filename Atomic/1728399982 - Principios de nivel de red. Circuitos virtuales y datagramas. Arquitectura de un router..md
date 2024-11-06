---
aliases:
  - Principios de nivel de red. Circuitos virtuales y datagramas. Arquitectura de un router.
tags:
  - review
  - "#ip"
  - retardos
References: 
cssclasses:
sr-due: 2024-10-19
sr-interval: 4
sr-ease: 272
---
# Principios de nivel de red. Circuitos virtuales y datagramas. Arquitectura de un router. 

Un router se encarga principalmente de dos funciones: **reenvío** y **enrutamiento**. El retardo de procesamiento está relacionado con el enrutamiento.

Cabe destacar que un router solo tiene *hasta los tres primeros niveles de red*:
1. Físico
2. Enlace
3. Red

**Maximum Transfer Unit**: también conocida como MTU. Es el máximo número de bytes que puede procesar por dicha tecnología (fibra, cable...). Si se recibe un paquete de mayor tamaño, no se procesa, se borra.

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

## Formato del datagrama

![[EstructuraDatagrama.png]]

TTL o Time To Live suele ser una serie de saltos máximos que, si no llega el paquete a su destino en esos saltos, se pierde en la red. 
***