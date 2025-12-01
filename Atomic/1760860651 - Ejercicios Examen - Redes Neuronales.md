---
aliases:
  - Ejercicios Examen - Redes Neuronales
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Redes Neuronales

**1. - Explica la estructura básica de una neurona artificial, señalando el papel de los pesos, la función de activación y el sesgo.**

Podemos distinguir tres partes fundamentales:
- *Capa de input*: el input se procesa en dicha capa y los resultados se envían a las siguientes
- *Hidden Layers*: puede haber o no. Es un total de $n$ capas que se encargan de aprender patrones lineales y no lineales (depende de la función de activación). Aunque pueden mejorar la precisión, aumentan el tamaño de las redes y el número de parámetros
- *Capa de output*: se obtiene un valor para el resultado a predecir.

**Los pesos** son el conocimiento de la propia red neuronal; a través del aprendizaje esos pesos se van modificando hasta obtener una serie de valores que optimizan la red neuronal para que tenga la máxima precisión posible.

Sin embargo, una red neuronal puede estar sesgada dependiendo del dataset con la que se entrene o si hay un *data leakage*. Eso reduce la precisión de la generalización con datos nunca vistos.


**2. - Describe las diferencias entre una red de una sola capa y un perceptrón multicapa (MLP).**

La principal diferencia es que la red de una sola capa tiene las capas de entrada directamente conectadas a las de salida, mientras que un MLP tiene una o más capas ocultas que le permiten procesar relaciones no lineales.


**3. - ¿Qué se entiende por entrenamiento supervisado y cómo se ajustan los pesos durante el proceso de aprendizaje?**

El entrenamiento supervisado se basa en entrenar dado un conjunto de datos con entradas conocidas y sus salidas deseadas.

Durante el proceso:
1. Propagación directa: se calcula la salida del modelo a partir de las entradas y los pesos actuales
2. Cálculo del error: a través de la función de pérdida
3. *Backpropagation*
4. Actualización de los pesos


**4. Explica qué es el sobreajuste (overfitting) y qué técnicas pueden utilizarse para evitarlo.**

Cuando el modelo generaliza correctamente con los datos de entrenamiento, pero no con los de validación u otros con los que no ha entrenado. Es decir, no ha aprendido relaciones sino directamente el resultado.

- Validación cruzada
- Data augmentation
- Redes más simples
- Regularización (L1 y L2)


**5. Caso MCWA. Describe la arquitectura de red utilizada en el sistema de advertencia de colisión (tipo de red, entradas y salidas).**

Se basa en un perceptrón multicapa.
- Entradas: gap entre los vehículos, velocidad de ambos vehículos y su aceleración
- Salidas: una neurona que indica el nivel de advertencia de colisión (binaria)
$$
\begin{cases}
value <= 0.5 \rightarrow \text{no warning} \\
value > 0.5 \rightarrow \text{warning}
\end{cases}
$$

**6. Caso MCWA. Explica por qué un modelo neuronal puede superar a los enfoques basados en parámetros fijos como los de Honda o Berkeley.**

- Adaptabilidad
- No linealidad
- Mejor generalización
- Aprendizaje de contexto


**7. - Caso MCWA. Analiza cómo se evalúa el rendimiento del modelo mediante curvas ROC o precisión-recall y qué indican sus resultados.**

**Curva ROC**: identifica la tasa de verdaderos positivos, frente a la tasa de falsos positivos. Si AUC = 0.5, rendimiento aleatorio.

**Curva precisión-recall**: evalúa las predicciones correctas frente a la posibilidad de tener una generalización perfecta.

Por lo tanto, la red neuronal detecta potenciales colisiones mejor, reduce falsas alarmas y se adapta a condiciones reales.


**8. Caso MCWA. Explica qué preprocesamiento de datos se realiza antes del entrenamiento y por qué es importante.**

1. Segmentación temporal: datos de conducción se dividen en *rolling periods*. El modelo captura dinámica temporal, velocidad, aceleración...
2. Normalización de variables
3. Limpieza
4. Etiquetado
