---
aliases:
  - Modelos basados en similaridad - KNN
tags:
  - review
"References":
cssclasses:
---
# Modelos basados en similaridad - KNN

Método perezoso, ya que el entrenamiento del modelo se reduce únicamente a almacenar los datos.

1. Se guardan todos los datos
2. A la hora de predecir, se busca los vecinos más cercanos dada esa instancia.

Se puede extender fácilmente a regresión, calculando la media de la respuesta de los $k$ vecinos.

## Hiper-parámetros y generalización del modelo

Hay una relación entre el hiper-parámetro $k$ y la capacidad de generalización del modelo (aciertos).

- Con $k=1$, las instancias ruidosas tienen demasiado peso, lo que aumenta la tasa de fallos.
- Con $k>1$, se toman más vecinos en cuenta, por lo tanto los *outliers* se tienen menos en cuenta y generan menos ruido.
- Con $k > n$, donde $n$ es un número arbitrariamente grande, la generalización comienza a falla y la precisión se reduce.

## Medir las distancias entre vecinos

Normalmente se usa la **distancia Euclidea**:
$$d = \sqrt{(x_2 - x_1)^2  + (y_2-y_1)^2}$$
Para atributos categóricos, se puede usar la **[[1748079240 - Distancia de Hamming|Distancia de Hamming]]**.

## Consecuencias del uso de distancias de KNN

- Influencia negativa de atributos con distintos rangos de valores: **re-escalar (normalizar) los datos**.
- Influencia negativa de los atributos irrelevantes: **selección de atributos**.

## Normalización

Los atributos pueden tener un rango de valores muy distinto, lo que puede hacer que el modelo otorgue más importancia a unos que a otros.

- MinMax: va del rango 0-1.
$$x^{'}_{ij} = \frac{x_{1j} - min(x_1)}{max(x_1) -min(x_1)}$$
- Estandarización
$$x^{'}_{ij} = \frac{x_{1j} - \bar x_1}{\sigma_1}$$
- Robust Scaler: especialmente bueno cuando hay un exceso de *outliers*. 
$$x^{'}_{ij} = \frac{x_{1j} - median(x_1)}{IQR(x_1)}$$

### Dar peso a las instancias de entrenamiento

Es de gran interés otorgar menos peso a las instancias que estén más alejadas del nodo a predecir. 
- `uniform`: distancia Euclidea
- `distance`: distancia Euclidea inversa

## Limitaciones de KNN

- Lento: **uso de los *ball trees***.
- Altas necesidades de almacenamiento: **pre-proceso con condensación**
- Sensible al ruido: **normalización de atributos**
- Sensible a atributos irrelevantes: **selección de atributos**