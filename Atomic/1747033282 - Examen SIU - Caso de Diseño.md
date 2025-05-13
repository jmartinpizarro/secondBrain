---
aliases:
  - Examen SIU - Caso de Diseño
tags:
"References":
cssclasses:
---
# Examen SIU - Caso de Diseño

**Propón un sistema interactivo basado en interfaz natural (voz, gestos...), sensores y Web APIs. Describe:**
- **El escenario de caso de uso**
- **El tipo de interacción esperada**
- **Las tecnologías utilizadas**
---
Se propone un caso de diseño de una cocina inteligente orientada especialmente a personas de edad avanzada o con alguna discapacidad (temporal o no). Este sistema permitiría usar la cocina de forma segura y efectiva para ellos; además que una persona sin discapacidad o joven podría usarla sin problemas; por ende estaríamos haciendo un **diseño universal**.

1. Una persona con alguna discapacidad física quiere hacer una receta que desconoce. La cocina, a través de comandos, podría guiarle en el proceso - diciéndole la receta - sin necesidad de tocar pantallas. Además, la vitrocerámica (por ejemplo) se podría encender usando comandos de voz.
2. La interacción esperada serían especialmente los comandos de voz. *¿Cómo se cuece un huevo? ¿Cuánto tiempo le queda al horno?* También se podrían usar gestos, aunque esto puede complicar su uso para ciertas personas, por lo que la interacción principal sería la de comandos por voz.
3. Las tecnologías usadas serían evidentemente APIs que nos permitan conectar funcionalidades con el mundo real. Para ello, se necesitaría un Speech-to-Text, reconocimiento de gestos como OpenCV o modelos de Hugging Face. APIs web para poder obtener recetas, y una integración de toda la cocina con IoT para poder conectarse a través de microservicios. 