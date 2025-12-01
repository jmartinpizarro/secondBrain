---
aliases:
  - Sistemas Multiprocesadores
tags:
"References":
cssclasses:
---
# Sistemas Multiprocesadores

## Introducción

### TLP - paralelismo a nivel de hilo

TLP implica la existencia de múltiples contadores de programa. Asumimos **MIMD**.

**Multiprocesador**: es un computador formado por procesadores altamente acoplados con:
- Coordinación y uso: típicamente controlados por un sistema operativo único
- Compartición de memoria: mediante un único espacio de direcciones compartido

**Modelos de software**:
- Procesamiento paralelo: conjunto de hilos acoplados que cooperan
- Procesamiento de peticiones: ejecución de procesos independientes originados por usuarios
- Multiprogramación: ejecución independiente de múltiples aplicaciones
### Multiprocesadores y memoria compartida

- **SMP: Symmetric-Multi-Processor**: 
	- Memoria compartida centralizada
	- Comparten una memoria centralizada única a la que todos acceden por igual -> UMA **Uniform Memory Access**. 
- **DSM: Distributed Shared Memory**: 
	- Memoria compartida distribuida. 
	- La memoria se distribuye entre los procesadores -> necesaria cuando hay muchos procesadores
	- NUMA -> **Non Uniform Memory Access** (latencia depende de la ubicación del dato)
## Arquitecturas de memoria compartida centralizada

Cachés grandes multi-nivel reducen la demanda de ancho de banda sobre la memoria principal.

$\exists$ varios tipos de datos en memoria caché:
- Privados: usados por un único procesador
- Compartidos: datos usados por varios procesadores

>[!DANGER] Problema Datos Compartidos
>Pueden replicarse en múltiples caches, reduciendo la contención (cada procesador accede a su copia local). Problemas de coherencia de cache.

### Incoherencia de cache

Se genera por la dualidad de estado entre el estado global y local.

Un sistema de memoria es **coherente** si cualquier lectura de una posición devuelve el valor más reciente que se haya escrito para esa posición.

#### Condiciones para la coherencia

- **Preservación de orden de programa**
- **Vista coherente de la memoria**
- **Serialización de escrituras**

### Consistencia de memoria

Define en qué momento un proceso que lee verá una escritura.

**Coherencia** y **consistencia** son complementarias:
- Coherencia: comportamiento de lecturas y escrituras a una única posición de memoria.
- Consistencia: comportamiento de lecturas y escrituras con respecto a accesos a otras posiciones de memoria.

## Alternativas de coherencia de cache

### Multiprocesadores coherentes

- **Migración de datos compartidos**
	- Un dato puede moverse a una cache local y usarse de forma transparente
	- Reduce latencia de acceso a dato remoto y demanda de ancho de manda de la misma memoria compartida
- **Replicación de datos compartidos leídos simultáneamente**
	- Se realiza una copia del dato en cache local
	- Reduce latencia de acceso y contención de las lecturas

Para que esto funcione de manera efectiva, existen **protocolos de coherencia de cache**:
- **Basados en directorios**:
	- El estado de compartición se mantiene en un directorio
	- **SMP**: directorio centralizado en memoria o en caché de más alto nivel
	- **DSM**: para evitar cuello de botella se usa un directorio distribuido (+ complejo)
- **Snooping** (espionaje):
	- Cada cache mantiene el estado de compartición de cada bloque que tiene
	- Las caches accesibles mediante medio bus
	- Todas las caches monitorizan el bus para determinar si tiene una copia de bloque o no.

#### Protocolos de espionaje

- **Invalidación de escrituras**:
	- Garantiza que un procesador tiene acceso exclusivo a un bloque antes de realizar una escritura
	- **Invalida el resto de copias** que pueda tener otros procesadores
- **Actualización de escrituras**:
	- Difunde todas las escrituras a todas las caches para modificar el bloque
	- Consume más ancho de banda

>[!NOTE] 
>Estrategia más común -> **invalidación**

### Protocolo MSI

// TODO