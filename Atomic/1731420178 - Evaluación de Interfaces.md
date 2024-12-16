---
aliases:
  - Evaluación de Interfaces
tags:
  - review
"References":
cssclasses:
---
# Evaluación de Interfaces

## Proceso de diseño

Se define según varios pasos:
1. Tener en cuenta el objetivo del sistema para poder satisfacer las necesidades del usuario.
2. Involucrar a las personas en cada fase del proceso -> Diseño Centrado en el Usuario.
3. Iterar varias veces en el proceso aportando mejoras en el diseño -> Diseño Iterativo.

## Evaluación

- El objetivo de los métodos de evaluación es la identificación de problemas
- Los problemas identificados llevan a repetir la fase de análisis de requisitos, incluyendo personas y escenarios, para poder proponer un diseño mejorado.
- La nueva versión del diseño volverá a evaluarse para volver identificación personas.

Es parte de un *diseño iterativo*, centrado en el diseño y en el cumplimiento de unos objetivos. Se puede llevar a cabo varias veces durante el proceso de diseño. 

Se pueden dividir en dos partes:
- Sin stakeholders
- Con stakeholders

### Evaluación sin stakeholders

Se basa en **encontrar problemas en la interfaz en una fase temprana del proceso de diseño** sin contar con ningún usuario externo al equipo de desarrollo.

Es más económica. Existen varios métodos para evaluar una interfaz:
- Análisis de tareas - Evaluación cuantitativa
	- HTA
	- Modelos predictivos
- Métodos cualitativos

**Tareas**: las acciones que el usuario tiene que llevar a cabo a través de la interfaz. **Análisis de tareas**: estudio de las acciones necesarias para llevar a cabo las tareas.

## HTA - Hierarchical Task Analysis

Dividir una tarea en subtareas de forma recursiva. Se focaliza en acciones observables y físicas, no están relacionadas con el software.

1. Se establece un objetivo de usuario e identificar las tareas principales.
2. Subdividimos las tareas principales en subtareas.
3. Agrupamos las subtareas en un plan (composición de tareas asociadas).

## GOMS

Goals, Operators, Methods and Selection Rules.
- Goals: objetivos que el usuario quiere conseguir
- Operators: acciones físicas y cognitivas que hay que llevar a cabo para lograr las metas
- Methods: procedimientos aprendidos para conseguir las metas
- Selection rules: reglas que se establecen para determinar qué método elegir

## Ley de Fitt

El tiempo requerido para conseguir un objetivo es proporcional a la distancia y al tamaño del objetivo.
- Las opciones más importantes deben tener mayor tamaño/visibilidad que las secundarias.

El Índice de dificultad (ID) se define como la dificultad en términos de distancia y anchura
$$ID = log_2(\frac{D}{W} +1)$$

El tiempo medio (MT) necesario para alcanzar un elemento es de:
$$MT = a + b \cdot ID$$
donde $a$ representa el tiempo de inicio y $b$ mide la velocidad inherente del dispositivo.


***