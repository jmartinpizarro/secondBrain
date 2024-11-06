---
aliases:
  - Protocolo TLS
tags:
  - review
  - RSA
  - diffieHellman
References: 
cssclasses:
---
# Protocolo TLS

## Establecimiento de clave en TLS

La clave secreta se establece en un sub-protocolo denominado *Handshake*. En este sub-protocolo, las entidades pueden autenticarse mutuamente usando la información contenida en certificados digitales.

## TLS Handshake (RSA - Based)

Está compuesto por cuatro pasos:
1. El cliente inicia la comunicación, enviando los algoritmos soportados en una [[1729419322 - Suites de Cifrado|Suites de Cifrado]] y un número aleatorio.
2. El servidor responde con la suite de cifrado elegida, un certificado de clave pública y un número aleatorio.
3. El cliente verifica el certificado y envía una *Pre-Master Key (PMKs)* (bytes aleatorios) cifrada con la clave pública del servidor. Además envía unos paquetes para comunicar que ya está listo para realizar cifrados simétricos
4. El servidor recibe y descifra con su clave privada la PMS. Tanto el cliente como el servidor usarán PMS para derivar claves maestras y claves de sesión. El servidor envía unos paquetes para comunicar que ya está listo para realizar cifrado simétricos.

## TLS Handshake ((EC)DHE-based)

Versión del Handshake en TLS 1.3

![[TLSHandshake1.3..png]]
***