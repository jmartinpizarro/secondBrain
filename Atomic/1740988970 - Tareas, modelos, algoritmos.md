---
aliases:
  - Tareas, modelos, algoritmos
tags:
  - review
"References":
cssclasses:
---
# Tareas, modelos, algoritmos

## Tareas

Tipos de aprendizaje automático. Se basan en el lenguaje en el que se expresan los modelos.
- Aprendizaje basado en atributos: se aprenden modelos cuyas entradas son atributos y cuyos datos se suelen representar con tablas.
- Aprendizaje relacional: se aprenden modelos que utilizan relaciones entre objetos y cuyo lenguaje es la lógica de predicados (representados en PROLOG)

Dependiendo del grado de supervisión de las tareas:
1.  Aprendizaje basado en atributos
	- Aprendizaje supervisado
		- Clasificación
		- Regresión - predicción numérica
	- [[1740989508 - Aprendizaje semi-supervisado|Aprendizaje semi-supervisado]]
	- [[1740989793 - Aprendizaje no supervisado|Aprendizaje no supervisado]]
		- Agrupamiento o clustering
		- Asociación
	- [[1740989810 - Aprendizaje por refuerzo|Aprendizaje por refuerzo]]
2. Aprendizaje relacional

### Feature Space - Espacio de instancias

Las instancias posibles que habilitan un espacio $d$-dimensional, donde $d$ es el número de atributos posibles como entrada.

## Aprendizaje Automático

El modelo siempre aprender a partir de un conjunto de datos *finitos*. Se espera que dicho modelo haga predicciones correctas para cualquier dato futuro, especialmente los no vistos durante el entrenamiento.

>[!NOTE]
>Al pasar de lo **concreto** a lo **general** se le domina **generalización o inducción**.

>[!DANGER] Problema de la inducción
>La inducción es filosóficamente imposible, puesto que un número finito de puntos pueden ser ajustados por un número infinito de soluciones.

En la práctica, sí que se puede obtener buenas generalizaciones si:
- El *dataset* es lo suficientemente grande.
- Si se hacen ciertas suposiciones sobre los tipos de modelo que resulten del aprendizaje. Por ejemplo, se puede suponer que el modelo tiene que ser "simple” (Navaja de Ockham). Esta suposición suele funcionar bien (obtener modelos que generalizan bien) en el mundo real.






