---
aliases:
  - Replicación de los datos
tags:
"References":
cssclasses:
---
# Replicación de los datos

## Modo maestro-esclavo

Uno de los nodos del cluster se designa como primario, mientras que el resto son esclavos.

**Nodo maestro**: fuente autorizada de los datos, responsable de las actualizaciones.

**Nodo esclavo**: resto de nodos, usualmente de lectura

**Ventajas**:
- Escala excelentemente en entornos intensivos de lecturas
- Aumenta la resiliencia a lecturas
**Desventajas**:
- Escalabilidad está limitada por dos factores:
	- Capacidad del maestro para el procesado de las actualizaciones
	- Capacidad (latencia) de la red para actualizar el estado del maestro a los esclavos

### Disponibilidad

El maestro se convierte en un único **punto de fallo**. Si el maestro desaparece, se designa a un nodo esclavo como maestro. Dos procedimientos:
- Recuperación manual
- Recuperación automática: se hace un análisis de los esclavos en el momento de la caída-> genera complejidad en la gestión y recuperación del cluster 

Se puede ver como un servidor monolítico con un sistema backup en caliente. Es una de las primeras arquitecturas tolerante a fallos.
1. Nodo maestro realiza el trabajo
2. Nodo esclavo comprueba latidos del maestro
3. Si el esclavo no recibe latido tras un timeout, asumimos que ha caído.

### Operativa

El tráfico de escritura debe de dirigirse al maestro, y el de lectura hacia los esclavos.
- Mejora el rendimiento por utilizar varios sistemas (aumenta la concurrencia)
- Los nodos esclavos se pueden ubicar próximos a los clientes para mejorar los tiempos de respuesta

Una operación de escritura bloquea al cliente que la realiza durante el tiempo que tarda la operación en hacerse persistente. Es dependiente de:
- El tiempo que tarde el SGDB local para procesar la información
- El tiempo que tarde en propagarse 

## Peer-to-Peer

Todas las réplicas tiene el mismo peso y la misma responsabilidad. Todas aceptan escrituras y lecturas. La pérdida de cualquiera de ellas no impide el acceso global al almacén.

**Ventajas**:
- Cluster se hace resistente a la pérdida de varios nodos
- Se aprovecha mucho más los recursos existentes
- Escalable en forma horizontal, entornos intensivos escritura y lectura.
**Desventajas**:
- La escritura distribuida puede generar un conflicto
- Puede no preservarse la escritura de un sistema
- Se complica la gestión, ocupando recursos del cluster para el control de este