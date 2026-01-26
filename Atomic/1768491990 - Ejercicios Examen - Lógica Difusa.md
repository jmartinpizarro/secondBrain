---
aliases:
  - Ejercicios Examen - Lógica Difusa
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Lógica Difusa

**Problema 1. Explica los conceptos fundamentales de la lógica difusa, incluyendo el significado de “concepto borroso” y “conjunto borroso”, y analiza en qué se diferencia este enfoque de la lógica clásica.**

La lógica difusa es un marco para razonar con información imprecisa en lugar de obligar a decisiones "todo o nada". Su base matemática es la teoría de conjuntos borrosos.

- Concepto borroso: es una idea cuya frontera no es nítida. Viento alto, pendiente moderada...
- Conjunto borroso: formaliza ese concepto asignando a cada valor $x$ un grado de pertenencia $u(x) \in [0, 1]$

La principal diferencia con la lógica clásica es que esta solo puede ser binaria, existe o no existe, mientras que la difusa tiene una pertenencia continua.

---

**Problema 2. Describe detalladamente el funcionamiento general de un sistema difuso, incluyendo evaluación del antecedente, inferencia, agregación y defuzzificación. Compara el modelo Mamdani con el modelo Sugeno.**

1. Fuzzificación: convierte entradas numéricas en grados de pertenencia a etiquetas lingüísticas.
2. Evaluación del antecedente (activación de reglas): cada regla tiene una forma tal que: *Si viento es Alto Y solar es Medio ENTONCES idoneidad es ALTO*
	1. Se calculan los grados de verdad para dicha combinación
	2. Se combinan con operadores AND/OR
3. Inferencia: se usa el grado de activación del antecedente para recortar o escalar el consecuente:
	1. En Mamdani: el consecuente es un conjunto difuso (Idoneidad = Alta) que se recorta según el *firing strength*.
	2. En Sugeno: el consecuente es una función constante o lineal de las entradas
4. Agregación: combina las salidas de todas las reglas en una salida global
	1. Mamdani: se unen, normalmente con MAX, los conjuntos difusos resultantes en una única función de pertenencia de salida.
	2. Sugeno: se combinan valores numéricos ponderados.
5. Defuzzificación: convierte la salida difusa agregada a un valor crisp.
	1. Mamdani: típico centroide
	2. Sugeno: la salida ya es crisp por construcción (promedio ponderado)

Mientras que Mamdani es muy interpretable y se requiere la defuzzificación al final del proceso, Sugeno es muy eficiente y fácil de optimiza con métodos numéricos; aunque más complicado de justificar.

---

**Problema 3. Analiza cómo se representan los operadores lógicos (AND, OR, NOT) en la lógica difusa y discute cómo su interpretación afecta a la combinación de variables en sistemas de decisión.**

AND/OR/NOT se definen con operadores sobre $[0, 1]$.

- NOT: suele ser el complemento:
$$\mu_{\overline{A}}(x) = 1 - \mu_{A}(x)$$
- AND: se implementa con una t-norma. Dos opciones muy comunes:
	- mínimo: $min(\mu_A, \mu_B)$
	- producto: $\mu_A \cdot \mu_B$
- OR: se implementa con una t-conorma:
	- máximo: $max(\mu_A, \mu_B)$
	- suma probabilística: $\mu_{A \lor B} = \mu_A + \mu_B - \mu_A\mu_B$

- Con $AND = min$; basta con que un criterio sea bajo para tirar muy abajo la regla.
- CON $AND = producto$; el sistema es más suave, pero penaliza todavía combinaciones mediocres.
- Con $OR = max / suma$ favorece mejor criterio/acumula evidencia.

---

**Problema 4. A partir del caso base, explica por qué la selección de sitios óptimos para energías renovables (solar, eólica o híbrida) constituye un problema adecuado para la lógica difusa, considerando la naturaleza gradual y ambigua de los factores involucrados.**

- Criterios continuos y graduales: viento, irradiación, pendiente, elevación... Son valores continuos.
- Criterios de componentes humanos/normativos: cercanía a asentamientos, restricciones ambientales... 
- Conflictos entre objetivos: maximizar un recurso y minimizar coste/impacto.

---

**Problema 5. Evalúa el papel de los factores humanos, climatológicos y topográficos en el modelo difuso del caso. Describe cómo cada grupo de factores influye en la toma de decisiones sobre ubicación óptima.**

- Climatológicos: viento y radiación solar determinan el potencial bruto de generación. En el modelo, se convierten en pertenencias y empujan la idoneidad del sistema
- Topográficos: pendientes y elevación afectan a la estabilidad...
- Humanos: áreas de asentamiento y proximidad a líneas de red.

---

**Problema 6. El caso utiliza mapas de velocidad del viento, irradiación solar y pendiente del terreno. Explica cómo estos datos se incorporan a un sistema difuso mediante funciones de pertenencia y rangos de clasificación (Reject, Average, Excellent).**

1. Tomar cada mapa raster (viento, solar, pendiente) y para una celda tener un valor numérico.
2. Definir funciones de pertenencia para clasificar cada variable en etiquetas lingüísticas (Reject/Average/Excellent).
	1. Triangular para variables suaves como solar y viento.
	2. Trapezoidal para asentamientos; para modelar una caída abrupta si estás dentro del área (variable binaria).
3. Combinar pertenencias con reglas y agregación para obtener un índice de idoneidad por celta y finalmente un mapa de decisión.

---

**Problema 7. Discute la importancia del análisis de pendiente del terreno dentro del proceso de decisión. ¿Por qué pendientes superiores a 15º o 25º pueden invalidar un sitio para la instalación de infraestructuras renovables?**

La pendiente afectaba directamente al coste, la seguridad y la eficiencia. El modelo marca como reject pendientes mayores de 15º lo que formaliza que a partir de ahí la viabilidad cae fuertemente.

---

**Problema 8. En el artículo se optimizan automáticamente las funciones de pertenencia y la base de reglas. Explica por qué la optimización es relevante y cómo puede mejorar simultáneamente la precisión y la interpretabilidad del sistema difuso.**

La optimización es relevante porque hay dos fuentes de subjetividad:
1. Parámetros de las funciones de pertenencia (donde empieza Average y termina Excellent...)
2. Base de reglas y umbrales.

Se integra un algoritmo en Matlab para optimizar parámetros y optimizar la base de reglas ajustando umbrales para la interpretabilidad.

- Ajustar parámetros y reglas puede mejorar la precisión.
- Optimizar la intepretabilidad evita parámetros extraños (reglas redundantes, orden lógico...)

---

**Problema 9. Describe el proceso de digitalización y georreferenciación aplicado en el caso, y analiza cómo se integran los mapas difusos con herramientas GIS para obtener los sitios más adecuados.**

Se usan técnicas GIS clave:
- Digitalización: trazado de fronteras y elementos geográficos. 
- Construcción de capas temáticas: asentamientos, líneas de red, pendiente, viento y cantidad de sol...
- Fuzzificación por capa y superposición: cada capa se convierte a grados de satisfacción y luego se combinan con AND para un índice global.
- Selección de sitios.

---

**Problema 10. Analiza la metodología de validación de robustez del modelo. Explica qué se entiende por “robustez” en este contexto y cómo se comprueba que los resultados no dependen de pequeñas variaciones en las entradas.**

Robustez significa que las zonas buenas identificadas por el modelo no cambian de forma drástica ante perturbaciones razonables del proceso de decisión. Entre 0.6 e 1.0.

---

**Problema 11. Evalúa los resultados obtenidos para los dos sitios identificados (Le Morne y La Laura–Malenga). Explica cómo el sistema difuso combina recursos solares, eólicos y condiciones geográficas para estimar el potencial energético total.**

- Random Forest: por ensamble y bagging, tiende a promediar decisiones y reducir la varianza; eso suele dar robustez ante ruido moderado, pero en ruido alto puede aún degradar si muchos splits aprenden correlaciones espurias. Además, en features binarios seleccionados, Random Forest trabaja con señales discretas fuertes.
- CNN: tiene mucha más capacidad. Con ruido alto puede:
	- Memorizar patrones erróneos si no hay suficiente regularización/datos.
	- Volverse inestable si el target es inconsistente.

---

**Problema 12. A partir del enfoque utilizado, discute cómo podría adaptarse esta metodología difusa para seleccionar ubicaciones óptimas de otras infraestructuras críticas (por ejemplo, baterías, plantas de hidrógeno, estaciones de recarga eléctrica), indicando qué factores adicionales deberían considerarse.**

La metodología es transferible: se define un conjunto de capas GIS, se fuzzifican con parámetros interpretables, se establecen reglas y se obtiene un mapa final de idoneidad. Solamente cambian los criterios.