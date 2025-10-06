---
aliases:
  - Optimizaciones avanzadas de caché
tags:
"References":
cssclasses:
---
# Optimizaciones avanzadas de caché

## Cachés pequeñas y simples

### Cachés pequeñas

Proceso de búsqueda:
- Selección de línea utilizando índice
- Lectura de etiqueta de linea
- Comparación con etiqueta de dirección

El tiempo de búsqueda **se incrementa con el tamaño de la caché**.

Una caché más pequeña permite:
- Hardware de búsqueda más simple
- La caché cabe en el chip del procesador (muy importante).

>[!NOTE]
>Caché pequeña mejora resultados de búsqueda


### Cachés simples

Uso de mecanismos de correspondencia lo más sencillo posibles.

**Correspondencia directa**: se permite paralelizar la comparación de la etiqueta con la transmisión de datos.

>[!WARNING]
>La mayoría de procesadores modernos se centran en las cachés pequeñas más que en la simplificación.

## Predicción de vía

>[!DANGER] **PROBLEMA**
>- **Correspondencia directa**: rápida pero con muchos fallos.
>- **Asociativa por conjuntos**: menos fallos pero más conjuntos (más lentas).

Se crea la **predicción de vía**:
- Se almacenan bits adicionales para predecir la vía que se seleccionará en el próximo acceso.
- Acceso adelantado al bloque y comparación con una única etiqueta.

## Acceso segmentado a la caché

Se segmenta el acceso a caché en varios ciclos de reloj; aumentando el ancho de banda de la caché.

- Se reduce el ciclo de reloj
- Se puede iniciar un acceso en cada ciclo de reloj
- Se aumenta el ancho de banda de la caché
- Se aumenta la latencia

## Cachés no bloqueantes

>[!DANGER] PROBLEMA
>Fallo de caché genera una parada hasta que se obtiene el bloque.

Entonces se hace una **ejecución fuera de orden**.

- Acierto durante fallo:
	- Permite accesos con acierto mientras espera
	- Reduce la penalización de fallo
- Acierto durante fallos / Fallo durante fallo:
	- Permitir fallos solapados
	- Necesita memoria multi-canal
	- Altamente compleja

## Palabra crítica primero y reinicio después

No esperar a recibir todo el bloque de memoria, tan solo la primera (ya que suele ser la única vital).

- **Palabra crítica primero**: bloque se recibe reordenado con la palabra que necesita el procesador al principio
- **Reinicio temprano**: el bloque se recibe sin reordenar.

## Buffer de escritura

Un buffer de escritura permite **reducir** la penalización de fallo.
- Cuando se ha escrito en el buffer el procesador da la escritura adecuadamente
- Escrituras simultáneas en memoria son más eficiente que una única escritura.

**Usos**:
- Escritura inmediata
- Post-escritura: solo cuando se reemplaza  un bloque.

## Optimizaciones de compilador

**Generar código que provoque menos fallos de instrucciones y datos.**

### Reordenación de procedimientos

Reducir los fallos por conflicto debidos a que dos procedimiento coincidentes en el tiempo se corresponden con la misma linea de caché. 

**Técnica**: reordenar los procedimientos en memoria.

### Fusión de arrays

Existen dos opciones:
- Dos arrays
- Arrays fusionados

### Intercambio de bucles

Mejorar localidad espacial.

### Fusión de bucles

Se busca mejorar localidad temporal, pero puede empeorar la espacial.