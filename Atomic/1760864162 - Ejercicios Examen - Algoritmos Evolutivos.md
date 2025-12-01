---
aliases:
  - Ejercicios Examen - Algoritmos Evolutivos
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Algoritmos Evolutivos

**1. Define qué es un algoritmo evolutivo y en qué principios de la biología se inspira.**

Método de optimización y búsqueda que imita el proceso de evolución para encontrar soluciones óptimas o casi óptimas a un problema.

- Selección natural
- Cruzamiento
- Mutación
- Supervivencia del más apto


**2. Explica el papel de los operadores genéticos (selección, cruce y mutación) en la generación de nuevas soluciones.**

- Selección: elige las poblaciones más aptas, preservando la calidad de la población
- Cruzamiento: cruza las poblaciones, generando nuevas poblaciones mejores que las anteriores
- Mutación: añade pequeños cambios aleatorios en partes de la solución, añadiendo aleatoriedad para que el problema pueda avanzar sin quedar atrapado en mínimos locales.


**3. Describe qué es una función de fitness y cómo guía la búsqueda de soluciones óptimas.**

*Función fitness*: mide qué tan buena es la solución del estado actual.

Las soluciones con mejor fitness tienen mayor probabilidad de reproducirse. Al favorecer a individuos de mayor calidad, la solución siempre va a ir mejorando poco a poco.


**4. Distingue entre algoritmos genéticos generacionales y de estado estable, indicando ventajas y limitaciones.**

**Generacionales**: se reemplaza toda la población con nuevos individuos creados mediante selección, cruce y mutación.
- Mayor diversidad, facilita escapes de mínimos locales
- Puede perder buenas soluciones.

**Estado estable**: solo se reemplaza una pequeña parte.
- Conserva las soluciones de forma natural.
- Menor diversidad -> mínimos locales y más lento.


**5. Caso Reconocimiento Facial. Explica cómo los algoritmos genéticos optimizan la fusión visible/térmica en el sistema de Hermosilla et al.**

Se utiliza para optimizar la fusión entre las ondas visibles y térmicas. Busca una combinación óptima de pesos entre visible-térmica, maximizando la calidad de la imagen. De esta manera se mejora la robustez en entornos con iluminación variable.


**6. Caso Reconocimiento Facial. Describe cómo se representa un individuo (cromosoma) y qué significan los 64 pesos cromosómicos.**

Cada individuo representa una posible forma de combinar/fusionar la imagen visible y térmica.

El cromosoma está formado por 64 pesos, cada uno de ellos aporta información sobre como es la contribución a la imagen en el ratio visible-térmico.


**7. Caso NAO. Explica qué parámetros del robot se optimizan y cómo se define la función de fitness en el estudio de Al-Hami y Lakaemper.**

Se busca optimizar los ángulos de movimiento y articulaciones, el propio movimiento, velocidad y estabilidad.

La función de fitness penaliza desviaciones o caídas, mientras que fomenta que el robot llegue a un punto determinado.

**8. - Caso NAO. Analiza cómo el cruce por bloques y la mutación por articulaciones contribuyen a la diversidad y a evitar mínimos locales.**

- Cruce por bloques: combina grupos enteros de articulaciones (torso inferior, superior...). De esta manera, se mantiene una cierta configuración óptima por parte de los padres.
- Mutación por articulaciones: modifica aleatoriamente ángulos y movimientos de articulaciones.


**10. - Reflexiona sobre cómo los métodos evolutivos pueden integrarse con redes neuronales o IA generativa en sistemas híbridos de optimización.**

- Optimización de pesos
- Optimización de arquitecturas
- Data augmentation
- Evolución y mejora de prompts.