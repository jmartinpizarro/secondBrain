---
aliases:
  - Entrevista Técnica - Machine Learning Prácticas
tags:
  - review
  - machine-learning
References: 
cssclasses:
---
# Entrevista Técnica - Machine Learning Prácticas

Para información más detallada de la asignatura, véase: [[1740988541 - Main - Aprendizaje Automático|Main - Aprendizaje Automático]]
## Tipos de Machine Learning

- **Aprendizaje supervisado**: el uso de un conjunto de datos _etiquetados_ para entrenar un modelo. Compuesto por dos vectores, uno de entrada (atributos), y otro de salida (valor esperado)
- **Aprendizaje no supervisado**: el uso de un conjunto de datos _sin etiquetar_ (no existe ningún conocimiento) para entrenar un modelo. La idea es que el algoritmo de encargue de encontrar y relacionar patrones en el conjunto numérico para poder así genera un vector de salida adecuado.
- **Aprendizaje por refuerzo**: el agente tiene que aprender una estrategia $\pi$ para saber qué acción tomar en cada situación $S$. El agente aprende dicha estrategia a partir de ensayo y error, usando una metodología basada en **costes o beneficios**.

## Overfitting y underfitting

**Overfitting**: modelo se ajusta demasiado a los datos de entrenamiento, *capturando incluso el ruido y las variaciones aleatorias presentes en ellos*. Esto resulta en una pérdida de capacidad para generalizar a nuevos datos, lo que significa que el modelo funciona bien con los datos de entrenamiento pero no con datos desconocidos.

**Underfitting**: un modelo es demasiado simple para capturar la complejidad subyacente de los datos de entrenamiento, por lo que realiza predicciones bastante malas con el dataset de entrenamiento y otros datos.

## Bias-variance tradeoff

Equilibrio entre el **sesgo**-**varianza**. El objetivo es encontrar un equilibrio entre estos dos parámetros para crear modelos que generalicen de manera correcta nuevos datos.

Técnicas como [regularización](##Regularización), [cross-validation](##Cross-validation) y [métodos de ensamblaje](#Métodos de Ensamblaje) ayudan a gestionar este equilibro.
### Sesgo

Un modelo es demasiado simple y no puede capturar adecuadamente las relaciones subyacentes de los datos. Usualmente esto genera **Overfitting**.

### Varianza

Un modelo es demasiado complejo, ajustándose al ruido encontrado en los datos de entrenamiento. Usualmente esto genera **Underfitting**.

## Regularización

Son una serie de métodos usados para reducir el overfitting. A efectos prácticos, se pierde un poco de precisión en el modelo de entrenamiento para lograr una mayor generalización con un conjunto nuevo de datos.
- **Lasso regression** or $L1$ regularization. Penaliza los coeficientes de correlación con valores altos. Es capaz de **eliminar atributos multicolineales**.
- **Ridge regression** or $L2$ regularization. Difiere de $L1$ matemáticamente, aunque también penaliza los coeficientes de correlación altos.
- **Elastic net regularization**: combina $L1$ y $L2$. 

## Cross-validation

Dividir los datos en subconjuntos y entrenar el modelo con todos menos uno, evaluándolo con el subconjunto restante. El proceso se repite para cada subconjunto, promediando los resultados para obtener una validación más robusta del modelo.

## Métodos de Ensamblaje

Combinar predicciones de varios modelos, promediar errores idiosincráticos (que hacen diferir) y producir mejores predicciones generales. 
- **BAGGing**: dado un dataset, se generan varios subconjuntos. Cada uno de estos subconjuntos se usa para entrenar un modelo distinto de manera separada. La predicción final dependerá de los resultados de estos modelos.
- **Boosting**: aprendizaje secuencial. El algoritmo entrena un modelo con la totalidad del dataset, y los modelos posteriores se construyen ajustando valores del [[1741427700 - Error Residual|Error Residual]] del modelo inicial.

## Feature Engineering

Proceso de transformar los datos en un formato mucho más adecuado para mejorar el rendimiento de los modelos. Incluye la creación de nuevas características, el manejo de valores faltantes, selección de características y la detección de valores atípicos.

## Modelos de Regresión

- **Regresión Lineal**: describe una variable continua $Y$ como una función lineal de una o más variables predictoras. Se usa para modelar relaciones lineales entre variables.
- **Regresión Logística**: utilizada para predecir variables binarias, modelando la probabilidad de que ocurra un evento en función de las variables predictoras. 
- **Regresión Polinómica**: extensión de la regresión lineal que utiliza términos polinomiales para modelizar relaciones no lineales.

## Árboles de decisión

- **Árboles de decisión**: modelos que utilizan una estructura de árbol para tomar decisiones basadas en condiciones de las variables predictoras. Los datos pueden ser categóricos o numéricos.
- **Random Forest**: conjunto de árboles de decisión entrenados sobre subconjuntos aleatorios de datos, combinando sus predicciones para mayor robustez.
- **Gradient boosting**: familia de algoritmos que entrenan modelos secuencialmente, cada uno enfocado en corregir los errores del anterior: *XGBoost, LightGBM, CatBoost*.

## Evaluación de modelos

- **MSE (Media de Errores Cuadráticos)** y **RMSE (Raíz Cuadrada de la Media de Errores Cuadráticos)**: Métricas para evaluar el error en modelos de regresión.
- **$R^2$ (Coeficiente de Determinación)**: Mide la proporción de varianza explicada por el modelo.
- **AUC-ROC (Área bajo la Curva ROC)**: Evalúa la capacidad del modelo para distinguir entre clases en problemas de clasificación.
- **F1-score**: Combina precisión y recuerdo para evaluar modelos de clasificación.
- **Matriz de confusión**: Tabla que resume las predicciones correctas e incorrectas del modelo.

## Redes neuronales básicas y Deep Learning

- **Redes neuronales**: modelos inspirados en la estructura de un cerebro, conformados por capas de nodos (neuronas), que procesan la información.
- **Deep Learning**: redes neuronales con muchas capas, capaces de aprender patrones complejos en datos como imágenes y audio.

## Algoritmos de clustering

- **k-means**: agrupa datos en $k$ clusters basándose en la similitud de ellos.
- **DBSCAN**: agrupa dados en clusters basándose en la densidad y proximidad entre puntos
- **Agglomerative clustering**: combina puntos individuales en clusters más grandes mediante un proceso jerárquico.


