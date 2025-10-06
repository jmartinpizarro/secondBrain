---
aliases:
  - Evaluación del rendimiento de sistemas informáticos
tags:
"References":
cssclasses:
---
# Evaluación del rendimiento de sistemas informáticos

## Métricas de rendimiento

El rendimiento $R(x)$ es una métrica inversa al tiempo de ejecución $T(x)$.
$$R(x) = \frac{1}{T(x)}$$
Y se ejecuta $n$ veces más rápido que X:
$$n = \frac{T(x)}{T(y)} = \frac{R(x)}{R(y)}$$
La única métrica fiable para comparar el rendimiento de computadores es la ejecución de programas reales.
- Cualquier otra métrica conduce a errores
- Cualquier alternativa a programas reales conduce a errores

- **Tiempo de ejecución**: 
	- Tiempo de respuesta: tiempo total transcurrido
	- Tiempo de CPU: tiempo de la CPU que ha estado ocupada
		- Con un solo procesador suele ser menor el tiempo de respuesta.
		- Con varios procesadores suele ser mayor que el tiempo de respuesta.

## Benchmarks

El rendimiento de un computador depende de la carga de trabajo con el que se evalúa.

**Benchmark**: aplicación o conjunto de aplicaciones usadas para evaluar el rendimiento.

**Aproximaciones**:
- Kernels: partes pequeñas de aplicaciones reales
- Programas de juguetes: programas cortos
- Benchmarks sintéticos: inventados para representar aplicaciones reales

### Suites de benchmarks

Está formada por un conjunto de programas y evalúa el rendimiento de todos los programas.
- Puede definir las opciones de compilación
- Incluye la carga de trabajo para cada programa

## Ley de Amdahl

El incremento de rendimiento obtenido usando un modo de ejecución más rápido está limitado por la fracción de tiempo que se puede usar dicho modo.

Una mejora es más efectiva cuanto más grande es la fracción de tiempo en la que esta se aplica.
$$S = \frac{1}{(1-f) + \frac{f}{S_n}}$$
Para mejorar un sistema complejo hay que optimizar los elementos que se utilicen durante la mayor parte del tiempo.

Campos de aplicación en las optimizaciones:
- Dentro del procesador
- En el juego de instrucciones
- En el diseño de la jerarquía de memoria, la programación y la compilación.

## Rendimiento del procesador

Un procesador ejecuta cada instrucción en varios ciclos de reloj.
$$tiempo_{cpu} = \frac{ciclos_{cpu}}{\text{frecuencia reloj}} = CPI = \frac{ciclos_{cpu}}{IC}$$
$$tiempos_{cpu} = CPI \cdot IC \cdot T $$
