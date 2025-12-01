---
aliases:
  - Memoria compartida distribuida
tags:
"References":
cssclasses:
---
# Memoria compartida distribuida

$\exists$ problemas con los protocolos de espionaje -> requieren comunicación con todas las caches.

**Ventajas**: ausencia de estructura de datos centralizada, bajo coste de implementación
**Desventajas**: ausencia de estructura de datos centralizada -> comunicaciones limitan la escalabilidad

## Protocolo basado en directorio

**Idea**: mantener el estado de cada bloque de caché -> bits de estado del bloque

Multicores con cache externa compartida
- Vector de bits de longitud igual a número de cores
	- Indica que caches privadas pueden tener copia de bloque
	- Solamente se envía invalidación a caches marcadas en mapa de bits.
- Esquema funciona bien dentro de un único multicore

Un directorio centralizado evita broadcast, pero se convierte en cuello de botella a medida que el número de procesadores aumenta.

**Solución: Directorio distribuido**.
- Distribuir el directorio con la memoria
- Cada directorio tiene información de la memoria local asociada
- Distintas peticiones de coherencia van a distintos directorios

## Bases del protocolo de directorio

Operaciones básicas:
- Tratamiento de fallo de lectura
- Tratamiento de escritura en un bloque compartido limpio
El directorio debe mantener el estado de cada bloque:
- **Compartido**: uno o más nodos tienen el bloque en caché y el valor en memoria está actualizado
- **No cacheado**: ningún nodo tiene una copia del bloque
- **Modificado**: solamente un nodo tiene la copia del bloque en cache y lo ha escrito

## Protocolo basado en directorio

La coherencia interna se mantiene mediante directorio centralizado.
El mismo directorio puede actuar como directorio local en DSM.

**Implementación del protocolo**:
- Transición de estados de caché local
	- Envían peticiones a directorio local
- Transición de estados del directorio

### Entrada no cacheada

El valor de memoria está actualizado.

Peticiones:
- **Fallo de lectura**:
	- Se envía dato de memoria a nodo peticionario
	- Nodo peticionario es el único en estado compartido
	- Estado pasa a compartido
- **Fallo de escritura**:
	- Se envía dato de memoria a nodo peticionario
	- El bloque se pasa a estado exclusivo
	- Nodo peticionario es el propietario
### Entrada compartida

El valor de memoria está actualizado.

Peticiones:
- **Fallo de lectura**:
	- Se envía el dato de memoria al nodo peticionario
	- El nodo peticionario se añade al conjunto de nodos de la entrada
- **Fallo de escritura**
	- Se envía el dato de memoria al nodo peticionario
	- Se envían los mensajes de invalidación al conjunto de nodos de la entrada
	- Se activa en el conjunto solamente el nodo peticionario
	- Se pasa a estado exclusivo
### Entrada exclusiva

El valor del bloque se encuentra en caché en el nodo identificado por el conjunto

Peticiones:
- **Fallo de lectura**
	- Se envía mensaje de captación a propietario
	- Se escribe dato en memoria
	- Se envía dato a nodo peticionario
	- Se añade nodo peticionario a conjunto de nodos
- **Post-escritura**
	- Ocurre cuando el propietario hace post-escritura del bloque
	- El bloque pasa a estado no cacheado
	- Se vacía el conjunto de la entrada
- **Fallo de escritura**:
	- El bloque tiene nuevo propietario
	- Se invalida bloque en antiguo propietario y se obtiene valor
	- Se envía valor al nodo peticionario
	- Se activa en el conjunto solamente el nuevo peticionario