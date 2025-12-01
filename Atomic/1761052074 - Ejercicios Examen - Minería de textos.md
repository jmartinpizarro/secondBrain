---
aliases:
  - Ejercicios Examen - Minería de textos
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Minería de textos

**1. Define qué es la minería de textos y en qué se diferencia de la minería de datos, especialmente en el contexto de los textos generados por IA.**

Proceso de extraer patrones o información útil de textos no estructurados. Implica tareas como análisis semántico, clasificación, extracción de entidades... En la IA, busca aplicar, entender y generar el contenido obtenido por la IA Generativa.

La minería de datos, por otro lado, procesa datos estructurados para descubrir correlaciones.


**2. - Explica el papel del procesamiento del lenguaje natural (PLN) dentro del proceso de minería de textos.**

Busca entender el lenguaje natural y convertirlo en gramáticas para que los computadores puedan procesarlo más óptimamente.

Busca, entre otras cosas:
- Segmentación de texto
- Desambiguación de palabras 
- Detectar semánticas que implican acciones


**3. Describe las etapas principales de un proceso de minería de textos (desde la adquisición del corpus hasta la extracción de conocimiento).**

1. Adquisición del corpus: recopilación de los textos fuentes
2. Preprocesamiento: eliminación de ruido, tokenización, *stop-words*
3. Representación del texto: conversión del lenguaje a una forma estructurada, como puede ser la matriz término-documento.
4. Minería o aprendizaje: usando técnicas de aprendizaje automático o estadística, 
5. Evaluación
6. Extracción del conocimiento: interpretación y presentación de lo obtenido de manera comprensible.


**4. Explica qué es el análisis de sentimiento y cómo puede integrarse en un flujo de minería de textos.**

Aplicación de PLN que es capaz de detectar emociones y sentimientos de las personas a través de lo que dicen - busca identificar la carga emocional de un texto -.

Se puede utilizar en una etapa intermedia de detección, tras la extracción introduce en el modelo y él es capaz de detectar los grados de probabilidad de ciertas emociones. Los resultados se aplican a un modelo y la fase de extracción de conocimiento.


**5. Caso: Industria 4.0. Resume el objetivo principal del estudio de Pejic-Bach et al. y el motivo por el cual se aplicó minería de textos a ofertas laborales de LinkedIn.**

El estudio busca mapear y caracterizar qué se pide en los anuncios de empleo relacionados con Industria 4.0 para que entidades como RRHH puedan anticipar mejor las competencias y perfiles emergentes.

Se usa minería de textos:
- No se había probado nunca antes
- Las ofertas tienen mucha información rica en requisitos -> reflejan directamente datos buscados
- Necesidad de herramientas ágiles, ya que los puestos de Industria 4.0 cambian constantemente

**6. Caso: Industria 4.0. Describe las características del conjunto de datos analizado (fuentes, periodo, idioma y número de ofertas).**

Fuentes: anuncios de todo tipo (Industria 4.0) en LinkedIn.  El tiempo fue solo tres meses, donde se recopilaron cerca de 2500 ofertas, donde solo 1400 fueron insertadas (inglés).

**7. Caso: Industria 4.0. Explica qué técnicas se utilizaron para la extracción de palabras, frases y tópicos y cómo se aplicó el coeficiente de Jaccard.**

Para el preprocesamiento se hizo una limpieza de ruido y una tokenización.

Para la extracción de palabras claves, los autores del *paper* identificaron palabras frecuentes, que agrupadas recogían terminología compuesta (*internet of things*). También se marcan co-ocurrencias, palabras que aparecen juntas en los anuncios.

Para la detección de tópicos, se basaron en los propios empleos para generar los tópicos de las ofertas de trabajo

El índice de Jaccard se usa para medir la similitud entre dos conjuntos. 
$$J(A,B) = \frac{|A \cap B |}{|A \cup B|}$$
Lo usaron para medir la similitud entre frases o térmicos en clusters. También se podría haber usado para ver la similitud entre las propias ofertas de empleo.