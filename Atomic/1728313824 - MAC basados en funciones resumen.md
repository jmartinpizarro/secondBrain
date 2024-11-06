---
aliases:
  - MAC basados en funciones resumen
tags:
  - review
  - mac
References: 
cssclasses:
sr-due: 2024-11-02
sr-interval: 15
sr-ease: 290
---
# MAC basados en funciones resumen

Conocidos como *HMAC*, emplea funciones hash existentes. Aplican la función resumen sobre una versión del mensaje al que añaden un conjunto de bits calculados a partir de la clave.

$$HMAC(K, M) = H[(K' \oplus opad) \space || \space H[(K' \oplus ipad) \space || \space M]]$$


***