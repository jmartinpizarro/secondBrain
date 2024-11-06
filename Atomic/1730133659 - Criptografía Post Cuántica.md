---
aliases:
  - Criptografía Post Cuántica
tags:
  - review
References: 
cssclasses:
---
# Criptografía Post Cuántica

Los algoritmos como el RSA y el DH se verán afectados cuando esta tecnología se desarrolle en los próximos años. Algoritmos como el AES podrían verse afectados, aunque en menor medida. Sin embargo, ya se estudian nuevos algoritmos para reemplazar al RSA y al DH.

## Mecanismo de encapsulación de clave simétrica (KEM)

Un KEM permite la transición de una clave secreta a través de un canal público entre dos entidades.

- **Generación de clave (Keygen)**: genera un par de claves (una pública $pk$ y otra privada $sk$). La clave pública se usará para encapsular la clave de sesión $k$, mientras que la clave privada se usará para descifrar el contenido encapsulado.
- **Encapsulación (Encaps)**: utiliza la clave pública para encapsular una clave de sesión aleatoria. Como salida, se genera un par: una versión cifrada de la clave de sesión y la propia clave de sesión. La clave de sesión la almacena y envía la versión cifrada al receptor.
- **Decapsulación (Decaps)**: este algoritmo, ejecutado por el receptor, toma el texto encapsulado y la clave privada correspondiente para recuperar la clave de sesión.
***