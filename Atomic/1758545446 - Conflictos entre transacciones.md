---
aliases:
  - Conflictos entre transacciones
tags:
"References":
cssclasses:
---
# Conflictos entre transacciones

Para solucionarlas, los SGDB utilizan el concepto de **desarrollo temporal (scheduling)**.

SE dota de herramientas a los SGDB para prever lo que puede ocurrir en un futuro si dos o más transacciones se ejecutan concurrentemente en el sistema.

Una transacción concurrente se basa en el principio de [[1758549849 - Seriabilidad]].

>[!NOTE]
>La forma más evidente de evitar conflictos es **no permitir la concurrencia**
>- **Serial**: toda transacción espera a que la que está en curso termine.

## Tipos de conflictos

- Lectura-escritura (R-W): **lecturas irrepetibles**. Una transacción intenta volver a leer un objeto para el que otra transacción cerrada ya ha realizado una solicitud de escritura.
- Escritura-lectura (W-R): **lectura de datos no confirmados**. Una transacción solicita leer un objeto, para la cual otra transacción no cerrada ya ha realizado una solicitud de escritura.
- Escritura-escritura (W-W)