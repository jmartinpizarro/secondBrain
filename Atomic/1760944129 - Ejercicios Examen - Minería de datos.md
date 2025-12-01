---
aliases:
  - Ejercicios Examen - Minería de datos
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Minería de datos

**1. Explica qué etapas componen el proceso de minería de datos según el modelo CRISP-DM y qué tipo de tareas se realizan antes de la modelización.**

Las etapas:
1. Comprensión del negocio
2. Comprensión de los datos
3. Preparación de los datos
4. Modelización
5. Evaluación
6. Despliegue


**2. ¿Por qué la preparación y comprensión de los datos suele consumir la mayor parte del esfuerzo en un proyecto de minería de datos?**

La mayoría de datos iniciales no llegan en el formato correcto o deseado para el modelado del proyecto: valores faltantes, sobrantes, duplicados, erróneos, sin normalizar...

Hace falta una análisis previo de los datos para poder dejarlos útiles, demandando tiempo y criterio experto de evaluación.


**3. Describe brevemente la diferencia entre Data Mining, Machine Learning, Deep Learning e Inteligencia Artificial Generativa, y cómo se relacionan entre sí.**

- Inteligencia Artificial Generativa: tipo de IA basada en Deep Learning que es capaz de generar nuevo contenido
- Machine Learning: subcampo de la IA que permite automáticamente a un programa aprender sobre un conjunto de datos sin ser programados explícitamente.
- Data Mining: proceso de descubrir patrones en grandes volúmenes de datos para su procesado, usando estadística y ML.

---

**1. Métodos de selección de atributos (filtro, envoltura e integrados) y su papel en el estudio**

- **Filtro:** selecciona atributos según criterios estadísticos (correlación, chi-cuadrado) sin usar el modelo.
    
- **Envoltura:** evalúa subconjuntos de atributos midiendo el rendimiento de un modelo concreto.
    
- **Integrados:** la selección ocurre durante el entrenamiento (por ejemplo, Random Forest o Lasso).
    

En el estudio, estos métodos se usaron para **reducir la dimensionalidad** y **eliminar variables redundantes**, mejorando la eficiencia y la interpretabilidad del modelo de predicción del estrés.

---

**2. Caso: Estrés del conductor – Tipos de datos recogidos**

- **Fisiológicos:** ritmo cardíaco, conductancia de la piel, variabilidad de la frecuencia cardíaca. Reflejan directamente el nivel de activación o estrés del conductor.
    
- **Contextuales:** velocidad, aceleración, condiciones del tráfico y del entorno. Representan las situaciones que pueden provocar estrés.
    
- **Personales:** edad, género y experiencia de conducción. Aportan información individual que modula la respuesta al estrés.
    

Estos tres tipos de datos fueron esenciales para construir un modelo **multidimensional y realista** del estado del conductor.

---

**3. Caso: Estrés del conductor – Desbalanceo de clases y uso de SMOTE**

El conjunto de datos presentaba **muchas más muestras de no-estrés que de estrés**, lo que sesgaba los modelos hacia la clase mayoritaria.  
Para corregirlo, se aplicó **SMOTE (Synthetic Minority Over-sampling Technique)**, que genera **nuevos ejemplos sintéticos** de la clase minoritaria mediante interpolación de sus vecinos más cercanos.  
Esto permitió **equilibrar las clases** y mejorar la **capacidad del modelo para detectar estados de estrés**.

---

**4. Caso: Estrés del conductor – Mejor rendimiento de Random Forest**

El algoritmo **Random Forest** superó a **KNN, SVM y redes neuronales** porque:

- Maneja bien **datos heterogéneos y ruidosos**.
    
- Realiza **promedio de múltiples árboles**, reduciendo el sobreajuste.
    
- Evalúa automáticamente la **importancia de las variables**.
    

Su naturaleza **ensemble** lo hace más robusto y estable, obteniendo **mayor precisión y AUC**.

---

**5. Caso: Estrés del conductor – Variables más importantes y su impacto en sistemas ADAS**

Las variables más relevantes fueron:

- **Frecuencia cardíaca** y **conductancia de la piel** (indicadores directos del estrés).
    
- **Velocidad**, **aceleración** y **densidad de tráfico** (factores externos desencadenantes).
    

Estas variables permiten a los **sistemas ADAS** (Advanced Driver Assistance Systems) **detectar y anticipar estados de estrés**, adaptando la asistencia (alertas, control de velocidad, intervenciones automáticas) para **mejorar la seguridad y el confort del conductor**.

