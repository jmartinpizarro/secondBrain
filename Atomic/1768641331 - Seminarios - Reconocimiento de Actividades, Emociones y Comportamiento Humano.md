---
aliases:
  - Seminarios - Reconocimiento de Actividades, Emociones y Comportamiento Humano
tags:
"References":
cssclasses:
---
# Seminarios - Reconocimiento de Actividades, Emociones y Comportamiento Humano

**Problema 1. Explica los tres pilares de RAECH (reconocimiento de actividades humanas, reconocimiento de emociones y análisis del comportamiento) y describe qué tipos de datos suelen emplearse para entrenar sistemas en cada uno de ellos.**

RAECH integra tres líneas complementarias que comparten la idea de inferir estados o acciones humanas a partir de señales observables:
1. Reconocimiento de actividades humanas: identificar acciones o actividades complejas (rutinas). Datos inerciales, de visión o señales ambientales.
2. Reconocimiento de emociones: clasificar emociones discretas. Visión, voz, fisiológicos.
3. Análisis del comportamiento humano: patrones estables o de mayor nivel: hábitos, anomalías, intención... Datos contextuales, interacciones...

---

**Problema 2. Compara los principales métodos utilizados en RAECH, diferenciando entre enfoques clásicos (por ejemplo, extracción manual de características y modelos estadísticos) y enfoques modernos basados en redes neuronales profundas (CNN, RNN, LSTM, GRU, Transformers). Describe ventajas y limitaciones de cada paradigma.**

**Enfoques clásicos**:
- Pipeline: preprocesado -> segmentación en ventanas -> extracción de características -> clasificador
- Funcionan con pocos datos y son más fáciles de entrenar, además de ser más interpretables y con un menor coste computacional.
- Dependen de rasgos diseños a mano, generalizan peor.

**Enfoques modernos - DL**
- Aprenden representaciones directamente datos crudos o casi crudos.
- **CNN**:
	- Capturan patrones locales, eficientes, buenas en extracción automática de rasgos
	- Limitadas para dependencias largas si no se combinan varios módulos temporales.
- **RNN/LSTM/GRU**
	- Diseñadas para series temporales en medio largo plazo.
	- Buenas para HAR secuencial y fisiología.
	- Entrenamiento más lento, problemas con secuencias muy largas.
- **Transformers**: 
	- Modelan dependencias largas con atención; dominan en multimodalidad y secuencias largas
	- Gran capacidad y flexibilidad; integración multimodal potente.
	- Suelen necesitar *muchos datos* y cómputo; riesgo de overfitting si el dataset es pequeño. Difícil de desplegar en edge sin compresión.

---

**Problema 3. Explica las estrategias de fusión multimodal (early fusion, mid fusion y late fusion) y analiza en qué situaciones cada una puede resultar más adecuada dentro de sistemas de reconocimiento en salud, seguridad o interacción humano–máquina.**

- *Early fusion*: se concatenan señales al inicio. Sirve cuando las modalidades están bien sincronizadas y alineadas; existe el riesgo de desincronización y de una alta dimensionalidad.
- *Mid fusion*: cada modalidad tiene un encoder propio, se fusionan representaciones latentes. Sirve cuando hay modalidades hetereogéneas (vídeo + texto) con escalas distintas. Usada en salud y seguridad.
- *Late fusion*: cada modalidad produce una decisión/probabilidad; luego se combinan. Sirve cuando las modalidades pueden fallar o no estar disponibles.

---

**Problema 4. **Problema 4.  Analiza los principales desafíos éticos presentes en sistemas RAECH, especialmente en relación con privacidad, reidentificación, sesgos algorítmicos y fiabilidad del modelo. Explica por qué estos riesgos se amplifican cuando se utilizan datos biométricos o sensibles.**

1. Privacidad y vigilancia: RAECH puede inferir rutinas, estados emocionales, lo que se supone que su mal uso puede incurrir en vigilancia y de la extracción de información no consentida.
2. Reidentificación: aunque se anonimicen datos, señales como cara, voz y marcha pueden reidentificar a una persona. La combinación multimodal deja una huella única.
3. Sesgos algorítmicos: depende de la cultura, edad, género, tono de piel... Además de la capacidad física y mental de cada persona
4. Fiabilidad: en saludo, un error no es un mero fallo, puede activar protocolos, alarmas o errores no esperados.