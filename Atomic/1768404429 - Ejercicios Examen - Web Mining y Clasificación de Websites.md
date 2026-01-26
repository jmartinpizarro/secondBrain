---
aliases:
  - Ejercicios Examen - Web Mining y Clasificación de Websites
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Web Mining y Clasificación de Websites

**Problema 1. ¿Qué es web mining y por qué clasificar websites es especialmente complejo?**

*Web mining* es la aplicación de técnicas de [[1760944129 - Ejercicios Examen - Minería de datos|Ejercicios Examen - Minería de datos]] y *machine learning* sobre datos extraídos de la web, con el objetivo de descubrir patrones útiles.

La clasificación de websites es especialmente compleja en este dominio por tres motivos principales:
- No existe un estándar: cada web implementa contenido, navegación y diseño de forma distinta.
- Volumen: una web no es un documento único; puede contener decenas o cientos de páginas. Para clasificar el sitio, hay que resumir el website completo en un registro tratable.
- Ruido: el scraping y el HTML introducen mucho texto irrelevante (menús, cookies). Se debe de realizar **una reducción del ruido y feature selection**.

---

**Problema 2. Fases del proceso de categorización automática y por qué importan**

El enfoque general convierte websites en un problema supervisa clásico:
1. Construir registros por sitio
2. Seleccionar términos
3. Entrenar clasificadores

El proceso se puede expandir a:
1. **Scrapping (crawling desde home con profundidad):** extrae texto visible y también metadatos y atributos. Sin esto no existe nunca el documento que minar.
2. **OCR** (imágenes) recupera texto incrustado en el diseño. El texto suele ser altamente discriminativo (compra, pagos).
3. **Limpieza + tokenización**: elimina símbolos no alfabéticos y separa los tokens. Importa para bajar el ruido y normalizar la entrada (el vocabulario puede ser no válido si no se hace así).
4. ***Stopwords removal:*** elimina palabras funcionales sin poder discriminativo. Importa porque reduce dimensionalidad y ruido semántico.
5. **Extracción de términos**: construye diccionarios de *unigrams* y *n-grams* desde el conjunto de entrenamiento.
6. **Normalización lingüística**: lematiza unigrams, para n-grams usa POS para filtrar combinaciones con sentido. Importa porque reduce variantes morfológicas y conserva n-grams útiles.
7. **Selección**: puntúa términos por asociación con la clase y se queda con ~1000. Es la principal defensa contra la alta dimensionalidad y el ruido.
8. **Clasificación**: entrena modelos y ajusta hiperparámetros maximizando F1.

---

**Problema 3. Desafíos de extracción automática de contenido**

- **Páginas anidadas**: si bajas mucho la profundidad, aumentan páginas periféricas -> más ruido y coste. El scrapping debe de tener una profundidad máxima.
- **Elementos gráficos como portadores de significado**: muchas páginas se expresan con iconografía/botones. 
- **Atributos HTML y metainformación**: además del texto visible, extraen atributos de elementos HTML, nombres de imágenes y keywords. Esto ayuda a recuperar señales que no aparecen en el texto renderizado.
- **Necesidad de OCR en screenshots**: capturas de la homepage permiten leer frases con tipografías/símbolos complicados que el scrapping textual no recupera bien.

---

**Problema 4. Papel del text cleaning, tokenización, stopwords, lematización y POS-lagging**

El objetivo global es transformar un texto web enorme (hasta > 1M palabras por sitio en su caso) en una representación con menos ruido y vocabulario controlado.

- **Text cleaning**: elimina caracteres no alfabéticos que en la web abundan. Reduce tokens basura.
- **Tokenización**: impone fronteras claras entre términos; sin ella el conteo es inconsistente.
- **Stopwords removal**: quita palabras de alta frecuencia y baja información (artículos, preposiciones), evitando que dominen la estadística.
- **Lematización (unigrams)**: agrupa variantes morfológicas bajando dimensionalidad y aumentando robustez.
- **POS-tagging (n-grams)**: filtra n-grams con sentido (patrones sintácticos permitidos). Es una forma de *feature engineering* lingüística para los n-grams no sean combinados ciegamente.

---

**Problema 5. Evaluación crítica de unigrams/n-grams + Chi-cuadrado: necesidad e impacto**

Por qué es necesaria esta fase: sin selección, el espacio de términos web es enorme y dominado por ruido. El artículo explícitamente introduce ***Term Evaluation*** para reducir dimensiones y quedarse con un conjunto relevante.

- Chi-cuadrado como TE:
	- Mide asociación entre presencia del término y clase, es clásico en categorización de texto por su eficiencia y buen rendimiento en escenarios BoW.
	- En el artículo, ordenan términos por score y seleccionan un conjunto T ~ 1000 (800 unigrams, 200 n-grams).

Por un lado, es rápido interpretable y reduce el overfitting, además que mejora el coste computacional y a menudo sube el F1.  Por otro lado, es univariante, tiende a favorecer términos muy correlacionados con el dataset y puede infra-representar señales raras pero útiles.

---

**Problema 6. El artículo proyecta cada website en un vector binario de 1000 dimensiones. Explica este proceso de representación y discute sus ventajas e inconvenientes frente a otras alternativas de representación textual.**

Se basa en construir un vector binario de 1000 dimensiones, donde se marca si dicho término $h$ aparece en el texto $T$. 

**Ventajas**
Robusto y simple. Evita que las páginas repetitivas inflen frecuencias.
Interpretabilidad: puedes inspeccionar qué términos activan la decisión.
Computacionalmente ligero.

**Desventajas**
Pierde frecuencia, importancia relativa y contexto (no hay TF-IDF) ni semántica.
No capta dependencias largas ni significado distribuido
Si la señal depende de densidad, el binario puede ser insuficiente.

Suele usarse TF-IDF, embeddings...

---

**Problema 7. Compara los cuatro modelos de clasificación empleados (SVM, CNN, Random Forest y Logistic Classifier). Explica los fundamentos de cada uno y discute por qué algunos modelos pueden resultar más robustos o precisos en este tipo de tarea.**

- [[1743357316 - Máquinas de vectores de soporte - SVMs|Máquinas de vectores de soporte - SVMs]]: suele rendir muy bien en texto "sparse" de alta dimensión, especialmente con buen tuning.
- Logistic Classifier
- Random Forest: puede ser robusto a ruido y capturar no linealidades/interacciones discretas, con texto sparse a veces no supera a soluciones más lineales.
- CNN: aprende filtros locales sobre secuencias (sobre una matriz de tokens). Aprende patrones composicionales, pero se requieren de mucho más datos y su robustez al ruido de etiquetas depende mucho del régimen de entrenamiento.

---

**Problema 8. El caso base presenta un dataset altamente desbalanceado (20% positivos vs. 80% negativos). Analiza las estrategias aplicadas (undersampling, oversampling, ponderación de clases) y discute su adecuación para este problema.**

- Undersampling (reducir negativos): reduce sesgo hacia la clase mayoritaria y acelera el entrenamiento, pudiendo tirar información útil.
- Oversampling: mejora recall y estabilidad del entrenamiento. Riesgo de sobreajuste a positivos replicados, SMOTE en texto binario no es recomendado.
- Ponderación de clases: suele ser la opción más limpia en texto: no altera la distribución de X, solo el coste. Requiere tuning, si hay mucho ruido en positivos, aumentar su peso puede amplificar el daño.

---

**Problema 9. Describe el proceso de digitalización y georreferenciación aplicado en el caso, y analiza cómo se integran los mapas difusos con herramientas GIS para obtener los sitios más adecuados.**

1. Se construye un dataset con etiquetas corregidas $R⁰$ y luego se toma un training set $S$ (50%).
2. Perturban aleatoriamente etiquetas del training en niveles de 0% a 21% y con 3 modelos: observado, balanceado, uniforme.

Modelos:
- Observado: más errores en positivos, imitando el patrón real observado.
- Balanced: mismo número de errores en cada clase, independientemente del tamaño
- Uniform: misma tasa global por instancia.

En desbalance, donde cae el ruido importa: si se corrompen muchos positivos, destruyes justo la señal escasa que define la clase; si corrompes mayoritariamente negativos, el modelo todavía ve positivos relativamente limpios.

---

**Problema 10. Analiza la metodología de validación de robustez del modelo. Explica qué se entiende por “robustez” en este contexto y cómo se comprueba que los resultados no dependen de pequeñas variaciones en las entradas.**

El rendimiento degrada al aumentar la perturbación, pero no excesivamente. A partir del 15% de perturbación extra empieza a degradarse exponencialmente.

--- 

**Problema 12. Integra todo lo aprendido analizando cómo podría adaptarse esta metodología a otros problemas de clasificación de websites (por ejemplo, detección de phishing, categorización temática o análisis institucional). Menciona qué partes del pipeline se mantendrían y cuáles deberían modificarse.**

Se mantiene:
1. Scrapping con control de profundidad + extracción de metadatos HTML
2. Limpieza, tokenización, stopwords y selección de términos.
3. Diseño explícito de evaluación con desbalance + métricas tipo F1.

Se modificaría para:
- Phising: añadiría features no textuales. URL lexical, certificados, redirecciones...
- Categorización temática: ampliaría la representación y quizás subiría la profundidad, permitiendo la multi-etiqueta.
- Análisis institucional: mantener OCRs para escudos/logos, además de reforzar la extracción de secciones típicas.
