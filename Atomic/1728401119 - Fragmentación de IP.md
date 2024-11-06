---
aliases:
  - Fragmentación de IP
tags:
  - review
  - ip
References: 
cssclasses:
sr-due: 2024-10-29
sr-interval: 11
sr-ease: 270
---
# Fragmentación de IP

El router conoce la MTU (unidad de transmisión máxima) de cada red a la que está conectada. De esta manera, si recibimos un paquete con un tamaño mayor que la MTU, dividiremos dicho paquete (en el router) para poder enviarlo de forma correcta ( se denomina *ensamblado*).

En el router destino, existe el *reensamblado*, un proceso inverso a la fragmentación.

Todo esto ocurre a nivel de la *capa de red* o *capa de IP*.
***