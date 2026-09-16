---
aliases:
  - Sistemas de altas prestaciones en entornos distribuidos
tags:
"References":
cssclasses:
---
# Sistemas de altas prestaciones en entornos distribuidos

## Introducción

**Cómo se consigue más velocidad?**
- Mejores algoritmos
- Mejores procesadores
- Paralelismo

### Tipos de paralelismo

- Tareas independientes
- Tares cooperativas
	- Pipeline
	- Coordinación (mutex y condiciones)

**Speed-up** - Ley de Amdahl: ejecución paralela con $n$ elementos de cómputo será:

$$\frac{1}{s + \frac{(1-s)}{n}}$$

Ver [[1789400114 - Taxonomía de Flynn|Taxonomía de Flynn]]

Ver [[1762768357 - Memoria compartida distribuida|Memoria compartida distribuida]], interfaz MPI.