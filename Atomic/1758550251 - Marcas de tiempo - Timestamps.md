---
aliases:
  - Marcas de tiempo - Timestamps
tags:
"References":
cssclasses:
---
# Marcas de tiempo - Timestamps

Ordenamiento mediante marcas de tiempo. A cada transacción se le asigna una marca de tiempo, según la lectura de un reloj en el momento en el que la transacción entra en el sistema.

**Las transacciones realizan los commits siguiendo su edad**, lo que lleva a realizar un ordenamiento por adelantado.

Se coordina el acceso a los recursos mediante las marcas temporales.

Tres reglas:
1. **Regla de acceso**: cuando dos transacciones intentan acceder simultáneamente y en conflicto a un mismo dato, se da prioridad a la transacción antigua y se hace esperar a la otra.
2. **Regla de transacción tardía**: una transacción antigua no puede leer ni escribir un elemento de datos que ya haya sido escrito por una transacción reciente
3. **Regla sobre las transacciones más recientes**: puede leer o escribir un elemento de datos que ya ha sido escrito por una transacción más antigua.