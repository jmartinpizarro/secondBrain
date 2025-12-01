---
aliases:
  - Ejercicios Examen - Sistemas Expertos
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Sistemas Expertos


**1. - Define qué es un sistema experto y señala sus componentes principales (base de conocimiento, motor de inferencia, interfaz y sub-sistema de explicación).**

Es un conjunto de programas que realiza unas tareas con el nivel de un experto humano bajo un dominio bien definido. 

- Base de conocimiento: contiene los hechos y reglas del dominio
- Motor de inferencia: aplica las reglas para obtener conclusiones
- Interfaz: permite la comunicación con el sistema
- Sistema de explicación: justifica las decisiones o conclusiones


**2. - Explica cómo funciona el proceso de inferencia en un sistema basado en reglas IF-THEN.**

Se basa en la concadenación de reglas; si una regla se cumple entonces pasa una cosa. De esta manera, se crea una especie de "árbol de decisión" a través del cual luego es posible, de manera recursiva, justificar la respuesta.


**3. Describe cómo los sistemas expertos manejan la incertidumbre mediante enfoques como las reglas de creencia o el razonamiento evidencial.**

A través de dar grados de confianza a las reglas o los hechos.
- Reglas de creencia: cada regla tiene un peso o una probabilidad
- Razonamiento evidencial: combina evidencias parciales para estimar la credibilidad de la conclusión sin usar las probabilidades.


**4. Explica el papel del sub-sistema de explicación y por qué es esencial para la confianza del usuario.**

Muestra cómo y por qué el sistema llegó a esa conclusión y es fundamental para generar confianza durante su interacción.


**5. Caso Agricultura IoT. Describe la arquitectura del sistema experto agrícola presentado en clase y cómo se integran los sensores IoT con el motor de inferencia.**

Podemos definir tres apartados clave en la arquitectura:
- Sensores: los sensores recogían la información y lo iban pasando por nodos a través de una *gateway* hasta que llegaba al ordenador central, donde se encontraba el motor de inferencia.
- Sistema: donde se ejecutaba el sistema experto siguiendo las reglas definidas. El sistema luego generaba un documento que enviaba a la interfaz del agricultor.
- Interfaz: el agricultor interactúa con el sistema a través de la interfaz. 


**6. Caso Agricultura IoT. Explica cómo se actualiza la base de conocimiento y qué tipo de variables se utilizan para el control de riego o plagas.**

Por parte del control de plagas: depende del tipo de larva, gusano, síntomas de la planta, el tiempo, estación y si las plantas ya tenían una plaga o no.

Por parte del control de riego: el tipo de planta, el área, la estación, mes y hora...


**7. Caso Inundaciones BRBES. Analiza cómo el sistema basado en reglas de creencia gestiona la incertidumbre y qué tipo de datos requiere.**

Genera grados de creencia, combinando evidencias para poder predecir con la mayor precisión posible. Para ello necesita basarse en datos cuantitativos y cualitativos: mediciones, sensores...

**8. Caso Inundaciones BRBES. Indica las ventajas del razonamiento evidencial frente a los sistemas expertos clásicos cuando existen datos incompletos.**

El razonamiento evidencial permite combinar información parcial o incierta sin necesitar probabilidades exactas.  
Ventajas: maneja datos incompletos, reduce errores por falta de información y mejora la flexibilidad en la toma de decisiones.
