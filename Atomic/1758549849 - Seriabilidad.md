---
aliases:
  - Seriabilidad
tags:
"References":
cssclasses:
---
# Seriabilidad

Garantiza que, tras la ejecución de múltiples transacciones ejecutadas a la vez, el resultado final sea siempre el mismo.

Crea la ilusión de que cada **transacción se ejecuta de forma aislada**, sin que otras interfieran con sus operaciones.

**Evita conflictos** anteriores y mantiene la integridad y consistencia de los datos

Es el nivel **más alto de aislamiento**.

1. Si **dos operaciones generan un conflicto**, la transacción en la ocurre antes la operación involucrada en el conflicto debe realizar su **commit** antes que la otra.
2. Un **desarrollo temporal** implica **varios pares de operaciones conflictivas** durante su ejecución y hay que analizarlos todos.
3. Si el **orden de commits** se representa mediante un grafo dirigido que representa la precedencia en el cierre de las transacciones (commits), para que un desarrollo sea serializable el grafo debe de ser acíclico. 