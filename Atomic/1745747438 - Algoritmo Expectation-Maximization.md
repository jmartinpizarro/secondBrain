---
aliases:
  - Algoritmo Expectation-Maximization 
tags:
"References":
cssclasses:
---
# Algoritmo Expectation-Maximization 

Algoritmo iterativo usado para generar clusters a través de métodos probabilísticos. Para ello, se busca estimar los parámetros a través de dos métodos:

- Expectation: se calcula la probabilidad de que cada instancia (basándose en parámetros) pertenezca a un cluster u a otro.
- Maximization: los parámetros del modelo se maximizan (medias, varianzas), para maximizar el parecido de las instancias.

El proceso se detiene cuando los parámetros del modelo dejan de ser relevantes.