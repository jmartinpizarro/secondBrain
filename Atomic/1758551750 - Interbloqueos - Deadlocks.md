---
aliases:
  - Interbloqueos - Deadlocks
tags:
"References":
cssclasses:
---
# Interbloqueos - Deadlocks

2PL ([[1758550237 - Bloqueos - Locking|Bloqueos - Locking]]), puede producir interbloqueos. 

Dos transacciones se esperan una a la otra. Tres alternativas:
- **Prevención:** gestionar los deadlocks antes de que ocurran. **Preadquisición de bloqueos**: toma todos los bloqueos necesarios antes de empezar -> es necesario conocerlos de antemano.
- **Evitación**: durante el conflicto forzar la salida. **Gestor de bloqueos** (usando *timestamps*).
	- Espera-muere: sin una transacción tiene una marca de tiempo más reciente, fuerza a la antigua a esperar.
	- Hiere-espera: una transacción aborta (la que sea más antigua).
- **Detección y eliminación**: se provoca la espera y una vez que se detecta se elimina. **Por temporizador**: vencimiento de un temporizador global.

**Criterios para elegir a la víctima**:
- Seleccionar la transacción más reciente
- Seleccionar la transacción más corta
- Seleccionar la transacción con la menor sobrecarga de reinicio.