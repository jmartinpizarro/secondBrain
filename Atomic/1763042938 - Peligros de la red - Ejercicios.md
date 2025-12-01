---
aliases:
  - Peligros de la red - Ejercicios
tags:
"References":
cssclasses:
---
# Peligros de la red - Ejercicios

**Problem 82 (Threats to network communications) Write down a table with four
rows, one for each category of threat actions to network communications (intercep-
tion, modification, fabrication, and interruption). Provide for each threat category
the security property that is affected (confidentiality, integrity, availability, etc.) and
one countermeasure that can be applied to network communications to mitigate the
threat**

- Interceptación: un ataque de este tipo consiste en el que un mensaje de $A$ a $B$ es accedido por $C$.  Afecta a la **confidencialidad**. **Contramedidas**: cifrado del mensaje; autenticación en la comunicación (canal confidencial y autenticado).
- Modificación: el emisor $A$ manda un mensaje $M$ al receptor $B$, pero el atacante $C$ es capaz de modificarlo a $M'$. Afecta a la **integridad**. **Contramedidas**: uso de MAC y de la [[1731333961 - Firma Digital|Firma Digital]].
- Fabricación: un adversario $C$ envía un mensaje $M$ al receptor $B$ haciéndose pasar por $A$. Afecta a la **autenticación**. **Contramedidas**: añades mecanismo robusto de autenticación (MAC o firmas).
- Interrupción: se detiene el servicio de las comunicaciones. Afecta a la **disponibilidad**. **Contramedidas**: filtrado de tráfico. 

**Problem 103 (So you pwned a CA, and now what?) Assume that a certificate authority, ACME-CA, which is present in the root store of many popular browsers and operating systems, has been hacked and it is now under the control of an attacker without anyone noticing.**
1. Sketch a possible attack that the attacker can stage now.
2. Can browsers rely on revocation mechanisms such as CRLs or OCSP to protect against this type of attacks? Explain why
---
1. Se crea un certificado firmado por la CA, pero a una entidad falsa/maliciosa (por ejemplo `*google`). Se te da una clave pública, y el certificado se firma por la CA (recordemos que solo necesidad la clave privada de la CA para hacer esto). Luego, podemos hacer un servidor *on-path*: el servidor que enruta a un dominio determinado enrute a tu dominio, no al otro (envenenamiento de DNS). Cuando se inicia el TLS. nuestro ataque enviará el certificado malicioso a la máquina.
2. No se puede. Los CRLs revocan, pero el daño ya está hecho. El OCSP actúa de similar manera, pero obtenemos el mismo error: el daño ya está hecho.