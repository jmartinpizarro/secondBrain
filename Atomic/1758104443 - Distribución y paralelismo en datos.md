---
aliases:
  - Distribución y paralelismo en datos
tags:
"References":
cssclasses:
---
# Distribución y paralelismo en datos

## Arquitecturas físicas de los sistemas de información

### Sistemas Monolíticos

Datos y software de gestión están centrados en un **único lugar**. La aplicación puede estar en otro sistema.

Proporciona control preciso del tiempo que simplifica los procesos de coordinación.

### Arquitectura centralizada

Usados para procesar **grandes volúmenes de datos en entornos transaccionales**. 

Compuesto por:
- Estructuras de memoria: System Global Area y Program Global Area
- Procesos en segundo plano: Database Writer, Log Writer...

Existen ficheros *log* para mantener consistencia y recuperación de información.

Caché de datos para optimizar transferencia de información. El **buffer de Redo Log** se encarga de mantener la consistencia de la información y recuperación en conflictos o caídas.

### Redes de sistemas

Aparecen por:
- Unificación de las islas de información derivadas de la explosión de servidores departamentales
- Abaratamiento del hardware y de las redes de comunicación
- Globalización de los servicios.

La **gestión del tiempo se complica** dado que aumenta la capacidad de paralelización, aumentando necesidades de control.

### Características de los sistemas distribuidos

El sistema de información es una unidad lógica única y global, aislada de los detalles físicos.

Cada nodo tiene independencia local y participa en actividades de manera coordinada.

### Sistemas paralelizados

Sistemas orientados al alto rendimiento computacional.
- Vías de interconexión internas cortas y rápidas
- Servidores monolíticos multi-core

Dos tipos:
- [[1758105201 - Sistemas paralelizados de disco compartido|Sistemas paralelizados de disco compartido]]
- [[1758105218 - Sistemas paralelizados sin disco compartido|Sistemas paralelizados sin disco compartido]]

## Modelos de distribución

**Escalabilidad horizontal** es más económica que la vertical, pero introduce complejidad añadida a la gestión del cluster.

>[!DANGER]
>La clusterización de un sistema solo debe realizarse cuando los **beneficios superen a los costes**. 

Se puede organizar la distribución de los datos:
- **[[1758105452 - Fragmentación de los datos|Fragmentación de los datos]]**: datos repartidos en varios nodos
- **[[1758105448 - Replicación de los datos|Replicación de los datos]]**: datos copiados en varios nodos buscando redundancia

Son técnicas complementarias que pueden ser usadas simultáneamente. 

Todo este tipo de modelos distribuidos genera un problema en la [[1758544602 - Consistencia de los datos y la información|Consistencia de los datos y la información]] que se tiene que manejar.

## Control de concurrencia

Dos estrategias posibles:
- **Nivel de conflictos muy alto**: posibilidad de rollback alta -> *enfoque pesimista*: detectar conflicto y sincronizar lo antes posible
- **Nivel de conflictos muy bajo**: posibilidad rollback baja -> *enfoque optimista*: posponer sincronización lo más posibles.

Para ello hay dos mecanismos de control:
- [[1758550237 - Bloqueos - Locking|Bloqueos - Locking]]: aislar las transacciones
- [[1758550251 - Marcas de tiempo - Timestamps|Marcas de tiempo - Timestamps]]: ordenar los desarrollos temporales y poder tomar decisiones

También existen los [[1758551750 - Interbloqueos - Deadlocks|Interbloqueos - Deadlocks]].

## Teorema de CAP

- *Consistency*: el sistema se comporta como si solo existiera un único nodo que procesa las operaciones una a una.
- *Availability*: toda petición recibida por un nodo que está disponible debe de conducir a una respuesta.
- *Partition Tolerance*: capacidad de sobrevivir a particiones de red que aíslen los nodos.

![[Pasted image 20250922164340.png]]