---
aliases:
  - Normalización en NoSQL
tags:
"References":
cssclasses:
---
# Normalización en NoSQL

Poco utilizado en el modelo relacional.

Su objetivo es **reducir la redundancia y aumentar la coherencia** de la información, generando una protección frente a errores de actualización.

Provoca una **fragmentación** y una red de vínculos que es necesario recorrer para volver a reconstruir la información tal y como se tiende a utilizar.

Implica el uso masivo de operadores del tipo **JOIN**. 

Computacionalmente es muy costosa, con un alto impacto en el rendimiento del sistema.