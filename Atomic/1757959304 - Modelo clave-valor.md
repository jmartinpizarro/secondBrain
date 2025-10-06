---
aliases:
  - Modelo clave-valor
tags:
"References":
cssclasses:
---
# Modelo clave-valor

Menor expresividad semántica.

Cada elemento se identifica de manera única por una clave, que puede ser del dominio o no.

**Atomicidad a nivel de clave**.

La base de datos no conoce la estructura del agregado, solamente será conocida por los programas de la aplicación.

- Alto rendimiento de lectura/escritura.
- Velocidad en las consultas.
- Fáciles de escalar.
- Fáciles de implementar