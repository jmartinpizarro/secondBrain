---
aliases:
  - Modelos basados en árboles
tags:
  - review
"References":
cssclasses:
---
# Modelos basados en árboles

Basados en reglas lógicas. Existen varios:

- **ID3**: construye árboles de decisión de manera recursiva, de la raíz hasta las hojas, seleccionando en cada momento el mejor nodo.
- **C4.5**: trata con valores continuos y utiliza criterios estadísticos para evitar que el árbol se sobreadapte
- **CART**: (Classification and Regression Trees) es otra manera de obtener árboles para clasificación (y también para regresión)

### Algoritmo ID3

1. Detener la construcción del árbol si:
	1. Todos los ejemplos pertenecen a la misma clase
	2. Si no quedan ejemplos o atributos
2. Si no, elegir el mejor atributo para poner en ese nodo (el que minimice la entropía media)
3. Crear de manera recursiva tantos subárboles como posibles valores tenga el atributo seleccionado

## Nodo raíz - ¿cuál es el mejor?

Nos basamos en la elección de la menor entropía $H$ de todos los atributos.

## Hiper-parámetros de los árboles de decisión

- min_samples_split: número mínimo de instancias que tiene que tener un nodo para poder ser dividido.
- max_depth: máxima profundidad del árbol
- min_impurity_decrease: el descenso en *impurity* (entropía, gini) tiene que ser mayor que este valor para seguir subdividiendo el árbol.

## Árboles para predicción numérica

Ambos (de regresión y modelos) se construyen de manera similar, pero existen ciertas diferencias:
- Para los árboles de regresión se calcula la media de las hojas
- Para árboles de modelos se construyen modelos lineales en las hojas

En árboles de clasificación, se busca **minimizar la entropía o Gini**. 
En árboles de predicción numérica, se busca **minimizar la varianza o desviación estándar**.

## Desventajas

- Si no se ajustan bien los hiper-parámetros, el método tiende a producir árboles demasiado profundos que no generalizan bien (*overfitting*)
- Las fronteras de decisión pueden ser muy simples para algunos problemas.

