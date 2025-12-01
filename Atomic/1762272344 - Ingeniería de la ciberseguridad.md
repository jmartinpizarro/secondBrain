---
aliases:
  - Ingeniería de la ciberseguridad
tags:
"References":
cssclasses:
---
# Ingeniería de la ciberseguridad

## Seguridad en la capa de transporte - [[1730133054 - Protocolo TLS|Protocolo TLS]]

TLS es el estándar de seguridad de internet (de autenticación y cifrado). Es necesario tener en mente los [[1731938621 - Certificados e Intraestructuras de Clave Pública]]. 
### TLS 1.3

Más rápido que TLS 1.2 -> se añade el **KEY SHARE** (solamente se realiza el *handshake* la primera vez hasta que pasa $t$ tiempo):
- 1 viaje para completar el *handshake* (TLS 1.2 en dos)
- 0 viajes para sitios ya visitados (lo que acarreaba problemas de seguridad)

Más seguro que TLS 1.2:
- Eliminaba algoritmos inseguros u obsoletos como SHA-1, RC4, DES, 3DES, AES-CBC...
- Se rediseñó la derivación de claves


### End-To-End Security

La comunicación en TLS se realiza directamente cliente-servidor, sin necesidad de intermediarios.

**Problemas**:
- Escucha a escondidas
- Inyección, MITM
- Impersonación 