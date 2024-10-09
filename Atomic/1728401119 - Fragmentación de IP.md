---
aliases:
  - Fragmentación de IP
tags:
  - review
  - ip
References: 
cssclasses:
---
# Fragmentación de IP

El router conoce la MTU de cada red a la que está conectada. De esta manera, si recibimos un paquete con un tamaño mayor que la MTU, dividiremos dicho paquete (en el router) para poder enviarlo de forma correcta.

En el router destino, existe el *reensamblado*, un proceso inverso a la fragmentación.

Todo esto ocurre a nivel de la *capa de red* o *capa de IP*.
***