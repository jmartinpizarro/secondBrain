---
aliases:
  - Regresión Lineal
tags:
"References":
cssclasses:
---
# Regresión Lineal

El objetivo es ajustar la curva (modelo) para poder generalizar los datos de manera correcta.

![[Pasted image 20250330193058.png]]

Existe siempre una variable $Y$ a predecir y una serie de variables independientes $x$. 

Existen dos maneras:
- Analítica
- Iterativa, mediante descenso de gradiente
## Modelos Lineales de solución analítica

Es muy costosa si tiene muchos atributos. Tiene una complejidad de $O(M^3)$.

Existe la posibilidad que, **si los atributos están muy correlacionados**, la matriz ($X^T \cdot X$) no sea invertible o muy inestable (en su defecto se puede usar la SVD).

Por ello, existe la **mejora iterativa mediante descenso de gradiente**.

## Modelos Lineales mediante descenso de gradiente

Para los modelos lineales, el error tiene forma de parábola, por lo que existe **un único punto donde el error es mínimo**. La idea es obtener un punto lo más cercano a dicho punto.

![[Pasted image 20250330193714.png]]

1. Inicializar ($w_0, w$) aleatoriamente tal que:
$$y(x, w, w_0) = w_0 + w_1 \cdot x_1 + ... + w_M \cdot x_M$$
2. Durante un determinado número de iteraciones (epochs):
$$J = \frac{1}{2N} \cdot \sum_{i=1}^{i=N}(t_i - y(x,w,w_0))^2$$
$$w_0 \leftarrow w_0 - \alpha \frac{\delta J}{\delta w_0}$$
$$...$$

### Variante estocástica

Se actualizan los parámetros de cada instancia. 

Suele ser más rápida, porque se producen más actualizaciones de pesos que con la versión batch. Cuando se usa con redes de neuronas, funciona mejor para evitar mínimos locales.

## Regresión Polinómica

Para modelar datos no lineales usando regresión lineal.

Basta con añadir tablas de datos $X^2, ..., X^P$, donde 
$$P = \text{grado del polinomio, actúa como hiperparámetro que controla la complejidad del modelo}$$

## Regularización para overfitting

Incluso modelos simples como estos pueden tener overfitting si tienen demasiados pesos. 

>[!DANGER]
>Si un modelo tiene 1 variable relevante, y 99 irrelevantes, es posible que el modelo tome como referencia ciertas variables irrelevantes por culpa de los pesos $w$. 

### Regularización Ridge o L2

Se añada para optimizar el modelo, un término para penalizar la complejidad del modelo y forzar a que los $w$ sean pequeños.

Se basa en la suma de los coeficientes al cuadrado.

De esta manera, un coeficiente $w_j$ podrá tener un valor alto, sólo si contribuye a reducir el error. De otra manera, su penalización $𝑤_𝑗$ será demasiado grande, y la optimización tenderá a disminuir su valor, y como consecuencia, que la variable $x_j$ tenga menos relevancia para el modelo.

### Regularización Lasso o L1

Con Ridge los coeficientes disminuyen, pero nunca llegan a 0. Para conseguir que los pesos $w_j$ lleguen a 0, se usa Lasso.

Se basa en el error absoluto, no en la suma de coeficientes al cuadrado.

Somos capaces de descartar variables en su totalidad.

### Elasticnet

Combinación de L1 y L2. Se parametriza con $\alpha$. Dependiendo del valor de $\alpha \in [0, 1]$, se tira más de L1 o de L2 respectivamente. 

## Regresión logística

Usado para problemas de clasificación. 
Se usa un modelo lineal, cuya salida se le pasa a la función sigmoide. La función logística es la aplicación particular de la función lineal de los datos a un funcional:
$$\sigma(z) = \frac{1}{1+e^{-z}}$$
Es una función suave y progresiva, que representa la posibilidad que un instancia pertenezca a una clase u a otra.

>[!NOTE]
>Las redes de neuronas están basadas en un modelo de regresión logística anidado.

