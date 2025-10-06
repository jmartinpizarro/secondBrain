---
aliases:
  - Bloqueos - Locking
tags:
"References":
cssclasses:
---
# Bloqueos - Locking

Utilizamos bloqueos para cada operación de acceso a los datos, los tipos de conflictos identificados anteriormente conducen a una **matriz de compatibilidad.**

**Shared Lock**: bloqueos de lectura.
**Exclusive Lock**: bloqueos de escritura.

Bloqueos disminuyen la concurrencia y necesitan protocolo para forzar la [[1758549849 - Seriabilidad]].

## Protocolos

- **De una fase (One Phase Locking, 1PL)**: consiste en tomar un bloqueo sobre un item antes de acceder a él y liberarlo tan pronto como se termine de utilizarlo.
	- Aumenta concurrencia
	- No garantiza seriabilidad
- **De dos fases (Two Phase Locking, 2PL)**
	- Primera fase de crecimiento: las transacciones solo adquieren bloqueos y no liberan ninguno hasta que se conceden todos los que necesitan
	- Segunda fase de encogimiento: van liberando bloqueos **sin solicitar más**.
	- Existen variantes como C2PL, S2PL, SS2PL.
