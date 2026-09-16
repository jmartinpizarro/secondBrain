---
aliases:
  - Conceptos generales de algoritmos evolutivos
tags:
  - AG
References:
cssclasses:
---
# Conceptos generales de algoritmos evolutivos

Evolución se basa en: **población, diversidad, herencia y selección**.

**Computación evolutiva**: se busca generar la mejor solución a un problema, para los que obtener la solución óptima no es posible, pero sí una que sea lo suficientemente buena.

El problema tiene que poder describirse como un conjunto de estados, con una función objetivo para medir la solución al problema. Hay que generar soluciones cada vez mejores en un espacio de búsqueda inmenso.

**Meta-heurísticas**: se pueden aplicar a una variedad de problemas, la búsqueda se hace de forma poblacional, no mediante trayectoria. Técnicas estocásticas.

---

**Procedimiento**

1. Selección de Progenitores
2. Reproducción
3. Nueva población de descendientes
4. Evaluación de la descendencia

Las representaciones pueden ser:
- Discretas - [[1789136267 - Algoritmos Genéticos|Algoritmos Genéticos]]
- Continuas - [[1789136309 - Estrategias Evolutivas|Estrategias Evolutivas]], [[1789136293 - Expresiones Genéticas|Expresiones Genéticas]]
- Basadas en árboles - [[1789136279 - Programación Genética|Programación Genética]]

## Población Inicial

- **Aleatoria Uniforme**: generar una población de $n$ individuos de dimensión $k$ de forma aleatoria, con $n$ tamaño de la población, $k$ tamañño de cada individuo.
- **Muestreo uniforme hipercúbico**: la aleatoriedad genera regiones más y menos representadas por individuos. Se puede:
	1. Dividir el espacio en $n$ regiones iguales
	2. Se generan individuos en cada región de forma aleatoria
- **Secuenciado simple inhibido**: se elige una distancia mínima $\Delta$, se genera una primera solución $L1$ de forma aleatoria. Se itera $n-1$ veces.
- **Heurística** para inicializar la población, y se itera buscando acercarse a una función objetivo.

## Evaluación

Los individuos son evaluados en función de su capacidad para resolver el problema.

- **Evaluación cuantitativa**: se asigna un valor numérico a la capacidad de un individuo para resolver un problema
- **Evaluación cualitativa**: no se produce un valor numérico, sino que se determina la capacidad de un individuo por su comparativa con el resto

La función de evaluación es lo que más tiempo de cálculo consume, hay que simplificarla al máximo -> se debe de estar sguro de lo que queremos maximizar/obtener

## Selección

