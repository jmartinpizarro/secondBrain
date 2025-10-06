---
aliases:
  - Consistencia de los datos y la información
tags:
"References":
cssclasses:
---
# Consistencia de los datos y la información

## Consistencia y coherencia

**Consistencia**: relacionada con la estabilidad, solidez de los datos. Se refiere a que todos los actores involucrados vean el **mismo valor del dato** tras la realización de un determinado conjunto de acciones.

**Coherencia**: relacionada con la conexión interna de las partes, como la lógica y el razonamiento. Es menos utilizada en las bbdd y se refiere principalmente a la **conservación del orden temporal de las acciones**.

## Integridad de la información

Mantener la **integridad** de la información es garantizar **la exactitud, precisión y consistencia** a lo largo de su ciclo de vida.
- Aplicación es responsable de mantener la exactitud y precisión
- La consistencia se mantiene gracias al sistema de almacenamiento.

>[!DANGER]
>Los problemas de inconsistencias entre actores distintos aparecen en **sistemas monolíticos**, ya que:
>- Se permite la concurrencia para mejorar el rendimiento del sistema
>- **Intercalan las acciones individuales** sin criterio alguno

Mantener consistencia en sistemas distribuidos es complicado ya que:
- El dato se puede encontrar en **múltiples lugares**.
- El nivel de concurrencia es mayor

### Transacción

Creación de un apunte contable: partida doble.
1. Si se hace la escritura en una tabla y no en la otra, la contabilidad queda desequilibrada.
2. Para mantener la integridad de la contabilidad la escritura en las dos tablas debe de ser una **operación indivisible**.

**Transacción -> operación atómica: todo o nada**.

>[!NOTE]
>Es necesario indicar el comienzo y el final de un bloque de operaciones que constituye la transacción.

1. Iniciar la transacción
2. Ejecutar un conjunto de consultas (con o sin modificación de datos)
3. Si no se produce ningún error, **confirmar (commit)** la transacción -> consolidar todas las operaciones.
4. Si se produce un error, **revertir (rollback)** la transacción -> abortar todas las operaciones.

Una transacción sigue las propiedades [[1758545176 - ACID|ACID]].

Para que ocurran **[[1758545446 - Conflictos entre transacciones|Conflictos entre transacciones]]**, debe de ocurrir tres circunstancias:
- Cada operación pertenece a una **transacción distinta**
- Al menos una de las operaciones es de **escritura**.
- Las operaciones actúan sobre el **mismo dato**.