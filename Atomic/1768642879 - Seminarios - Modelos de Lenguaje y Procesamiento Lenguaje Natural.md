---
aliases:
  - Seminarios - Modelos de Lenguaje y Procesamiento Lenguaje Natural
tags:
"References":
cssclasses:
---
# Seminarios - Modelos de Lenguaje y Procesamiento Lenguaje Natural

**Problema 1. Explica qué es un modelo de lenguaje y describe las principales características del lenguaje natural que dificultan su procesamiento automático (espontaneidad, ambigüedad, multimodalidad)**

Un modelo de lenguaje - LM - es un sistema que aprende la probabilidad de generar secuencias de palabras o tokens y, a partir de ello, puede predecir, generar, clasificar o transformar texto. Su objetivo es capturar regularidades léxicas, sintácticas y semánticas del lenguaje.

Las principales dificultades son:
- Espontaneidad: el lenguaje es informal, contiene errores, cambios de tema... Rompe supuestos rígidos.
- Ambigüedad
- Multimodalidad: el significado depende de otras señales. El texto aislado suele ser insuficiente.

---

**Problema 2. Compara los enfoques clásicos de NLP (extracción de características, modelos estadísticos) con enfoques modernos basados en embeddings y transformers. Explica por qué estos últimos representan un avance significativo.**

**Enfoques clásicos**
- Representación: bag-of-words, TF-IDF, n-grams...
- Modelos de Bayes, HMM, SVM, Regresión Logística.
- Ventajas: simples, interpretables y eficientes con pocos datos
- Limitaciones de orden largo y semántica profunda, generalizan mal.

**Enfoques modernos**:
- Embeddings densos: palabras/frases se representan en espacios continuos donde la semántica y el contexto se preservan.
- Transformers: atención auto-regresiva/bidireccional que captura dependencias largas y contexto global, altamente paralelizables.
- Ventajas clave:
	- Representaciones contextuales
	- Transferencia de conocimiento a múltiples tareas
	- Rendimiento superior en comprensión, generación y razonamiento textual.
- Limitaciones: mayor coste computacional y energético; menor interpretabilidad directa.

---

**Problema 3. Describe el proceso de preentrenamiento y fine-tuning en modelos de lenguaje, indicando por qué permiten adaptar modelos generales a tareas específicas en organizaciones sin necesidad de entrenar desde cero.**

- Pre-entrenamiento: el modelo aprende patrones generales del lenguaje a gran escala. Adquiere gramática, semántica y conocimiento general.
- Fine-tuning: se ajusta el modelo a tareas o dominios concretos con datos específicos.

Esto tiene grandes ventajas para las organizaciones porque reduce drásticamente el coste y el tiempo, además que requiere menos datos etiquetados.

---

**Problema 4. Analiza aplicaciones actuales de NLP en empresas (chatbots, traducción, ventas, soporte, educación, sanidad) y explica los principales retos técnicos que presentan, incluyendo alucinaciones, eficiencia energética y limitaciones del modelo.**

Los principales retos son:
- Alucinaciones: generación de contenido plausible pero falso, crítico en dominios regulados. Se usa RAGs para reducir que esto ocurra.
- Eficiencia energética y coste: los modelos grandes consumen recursos, necesidad de compresión y uso selectivo.
- Limitaciones del modelo: conocimiento desactualizado si no se conecta a fuentes vivas. Sesgos heredados de los datos.
- Gobernanza y seguridad: control de los datos, trazabilidad y evaluación continua.