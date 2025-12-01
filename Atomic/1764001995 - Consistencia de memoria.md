---
aliases:
  - Consistencia de memoria
tags:
"References":
cssclasses:
---
# Consistencia de memoria

**Modelo de consistencia de memoria**: interfaz entre el programa y sus transformaciones
- Conjunto de reglas que define como se procesa  el sistema de memoria
- Contrato programador-sistema
- Determina qué optimizaciones son válidas sobre problemas correctos

## Modelo de memoria monoprocesador

Las operaciones de memoria ocurren en orden de programa. La semántica está definida por orden del programa secuencial.
- Razonamiento simple pero restringido
- Las operaciones independientes pueden ejecutarse en paralelo
- Las optimizaciones preservan la semántica

### Restricciones de la consistencia secuencial

- **Orden de programa**: operaciones de memoria de un programa deben hacerse visibles a todos los procesos en el orden del programa
- **Atomicidad**: el orden total de ejecución entre procesos debe ser consistente requiriendo que todas las operaciones sean atómicas.

Restringe todas las operaciones de memoria:
- Write -> Read
- Write -> Write
- Read -> Read, Read -> Write

Es un modelo simple para razonar sobre programas paralelos. **Reordenaciones simples del procesador** pueden violar el modelo de consistencia secuencial. Ocurren cuando:
- Reordenación de hardware para mejorar el rendimiento
- Optimizaciones de compilador que aplican transformaciones que reordenan operaciones de memoria
- Transformaciones por programadores o herramientas de *refactoring* también modifican la semántica del programa.

### Violación de la consistencia secuencial

Si las caches usan bufer de escritura:
- Escrituras se retrasan en bufer
- Lecturas obtienen el valor antiguo
- Se invalida el algoritmo de Dekker: primera solución conocida al problema de la exclusión mutua.

Las restricciones para la consistencia secuencial son exigentes: **puede haber condiciones necesarias menos exigentes**

#### Optimizaciones respecto a las restricciones de consistencia

- Modelos que relajan el orden de ejecución del programa
	- Relajar W -> R: orden de almacenamiento total
	- Relajar W -> W, W -> W: orden de almacenamiento parcial
	- Relajar todo

## Ordenamiento débil

Divide las operaciones a memoria en operaciones de datos y operaciones de sincronización.

Las **operaciones de sincronización** actúan como una barrera:
- Todas las operaciones de datos previas en orden de programa a una sincronización deben completarse antes de ejecutar la sincronización.
- Todas las operaciones posteriores tiene que esperar a que se complete la sincronización.
- Las sincronizaciones se realizan en orden de programa.

**Se implementa a través de un contador que tiene el procesador. Si se emite una operación, se incrementa. Si se completa, se reduce. Se sincroniza cuando PC = 0**.

