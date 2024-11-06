---
aliases:
  - Suites de Cifrado
tags:
  - review
"References":
cssclasses:
---
# Suites de Cifrado

Estas condiciones (protocolos y algoritmos) son las condiciones que usará el cliente para realizar la comunicación segura por un canal inseguro. Existen un conjunto de suites de cifrado permitidas y seguras:

- **Protocolos**: indica el tipo de protocolo a usar, SSL o TLS, con sus correspondientes versiones (hay que tener en cuenta que el SSL está deprecado)
- **Algoritmo de cifrado y longitud de la clave**: algoritmo usado para el cifrado de las comunicaciones
- **Modo de cifrado**: modo de operación utilizado por el algoritmo de cifrado
- **Hash-MAC**: algoritmo de cifrado irreversible que verifica la integridad de los mensajes.
- También podemos encontrar *algoritmo de intercambio de claves*, *firma digital* y el *tamaño de la curva elíptica*.

![[SuitesCifrado.png]]

Para el cifrado de comunicaciones, los más recomendados son de *cifrado autenticado*:
- AESxxx-GCM
- ChaCha20-Poly1305

Para el aseguramiento de la integridad, los más recomendados son las *funciones resumen*:
- SHA256
- SHA384
***