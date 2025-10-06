---
aliases:
  - Jerarquía de memoria
tags:
"References":
cssclasses:
---
# Jerarquía de memoria

Sigue la estructura de:
1. Procesador
2. Caché L1
3. Caché L2
4. Caché L3
5. Memoria Principal

**Bloque o línea**: unidad de copia. Formada por múltiples palabras.

Si el dato está presente en el nivel superior: **acierto**:
$$h = \frac{aciertos}{accesos}$$
Si el dato accedido está ausente:
- **Fallo**: bloque se copia a nivel inferior
- Acceso a dato en nivel superior.
- Tiempo necesario -> Penalización de fallo
$$m = \frac{fallos}{accesos} = 1 - h$$
**Tiempo medio a acceso a memoria**:
$$t_M = t_A + (1-h) \cdot t_F$$
**Ciclos de detención de memoria**:
$$IC = \text{accesos a memoria}_{instr} \cdot (1-h) \cdot \text{penalizacion}_{fallo}$$

## Políticas y estrategias

### Ubicación de bloque

**Correspondencia directa**: 
- Caché organizada por líneas de caché
- Un bloque de memoria se ubica en una línea determinada por su dirección
- Ubicación -> bloque mod $n_{bloques}$

**Correspondencia totalmente asociativa**:
- Cada bloque de memoria tiene asociada una etiqueta única.
- Cada línea de la caché guarde de la etiqueta del bloque que contiene.
- Un bloque de memoria se ubica en cualquier línea de la caché.
- Ubicación -> cualquier lugar.

**Correspondencia asociativa por conjuntos**:
- Las líneas de la caché se organizan en conjuntos
- Queda conjunto tiene varias líneas.
- Selección de conjunto determinada por dirección del bloqueo.
- Ubicación dentro de conjunto determinada por etiqueta

## Identificación de bloque

**Dirección de bloque:
- Etiqueta: identifica la dirección de entrada
- Índice: selecciona el conjunto
**Desplazamiento de bloque**
- Selecciona datos dentro de un bloque.
**Con mayor asociatividad**:
- Menos bit de índice
- Más bits de etiquetas

## Reemplazo de bloque

Relevante para asociativa y asociativa por conjuntos.
- Aleatorio
- LRU: menos reciente usado
- FIFO: aproxima LRU con menor complejidad

## Estrategia de escritura

**Escritura inmediata**:
- Todas las escrituras van a bus y memoria
- Fácil de implementar
- Problemas de rendimiento de SMPs

**Post-escritura**:
- Muchas escrituras son aciertos
- Aciertos de escritura no van a bus y memoria
- Problemas de propagación y serialización
- Más complejo

## Optimizaciones básicas de caché

- **[[1758563207 - Reducción de tasa de fallos|Reducción de tasa de fallos]]**
- **[[1758563527 - Reducción de penalización de fallos|Reducción de penalización de fallos]]**
	- Cachés multinivel
	- Prioridad de lecturas sobre escrituras
- **Reducción de tiempo de acierto**
	- Evitar traducción de direcciones en indexado en caché

Pero esto es una alta mariconada, por lo que tenemos [[1759158555 - Optimizaciones avanzadas de caché|Optimizaciones avanzadas de caché]].