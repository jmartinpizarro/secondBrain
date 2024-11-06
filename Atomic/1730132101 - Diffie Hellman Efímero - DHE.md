---
aliases:
  - Diffie Hellman Efímero - DHE
tags:
  - review
References: 
cssclasses:
---
# Diffie Hellman Efímero - DHE

Crea unas claves solo válidas para esa sesión que se descartan después de su uso. Esto se hace a través de unas funciones de derivación, *ephemeral keys*

## Diffie Hellman Efímero Autenticado

Buscamos *autenticar la clave pública*:
- Usamos un certificado en la clave pública del propietario que certifica, con un algoritmo de firma, que el protocolo se está usando de manera correcta.
- La clave pública se autentica usando criptografía simétrica si es que ambos interlocutores comparten la misma clave.


***