---
aliases:
  - MAC basados en cifradores de bloque
tags:
  - review
  - mac
References: 
cssclasses:
---
# MAC basados en cifradores de bloque

Cifran el mensaje mediante un algoritmo de cifrado simétrico en bloque en modo CBC ($\oplus$).  El valor del MAC es el resultado del cifrado del último bloque. Consiguen que el MAC dependa de todos los bits del mensaje.
***