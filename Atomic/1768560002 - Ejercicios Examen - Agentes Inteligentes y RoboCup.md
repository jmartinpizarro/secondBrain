---
aliases:
  - Ejercicios Examen - Agentes Inteligentes y RoboCup
tags:
"References":
cssclasses:
---
# Ejercicios Examen - Agentes Inteligentes y RoboCup

**Problema 1. Explica el concepto de agente inteligente y analiza cómo integra percepción, razonamiento y acción en entornos físicos o digitales.**

Un agente inteligente es una entidad que percibe su entorno mediante sensores o entradas, razona (decidiendo según sus objetivos, estado y conocimiento) y actúa. La idea clave del ciclo es:
1. Percepción: se actualiza el estado interno. Transforma señales en una representación útil.
2. Razonamiento -> política/plan: selecciona acciones para maximizar un objetivo
3. Acción -> efecto + feedback: ejecuta y observa consecuencias, ajustando decisiones en el siguiente ciclos.

En entornos físicos, percepción implica visión/LiDAR. En entornos digitales, implica lectura de datos, queries, lenguaje digital... 

---

**Problema 2. Describe la evolución de la IA desde los agentes simbólicos y reactivos hasta los agentes cognitivos y generativos basados en LLMs, destacando cómo cambia el rol del agente en cada etapa.**

1. Agentes simbólicos: representan conocimiento con reglas y lógica explícita. Fuertes en dominios cerrados y explicables, limitados ante ambigüedad y ruido.
2. Agentes reactivos: priorizan una respuesta rápida -> acción con poca planificación. Bueno para control y tiempo real.
3. Agentes cognitivos: integran planning, modelos del mundo... Manejan tareas más largas con objetivos y restricciones.
4. Agentes generativos basados en LLMs: incorporan lenguaje natural como interfaz y como herramienta de razonamiento heurístico. Orquestan flujos, coordinan herramientas...

---

**Problema 3. A partir de la idea de agentificación de la IA, analiza cómo la autonomía, la memoria y la interacción en lenguaje natural transforman el diseño de sistemas en las organizaciones.**

La agentificación implica diseñar sistemas donde la IA no solo responde, sino que opera con cierto grado de autonomía. Tres cambios clave:
- Autonomía: el sistema pasa de asistente bajo demanda a actor que ejcuta tareas. Esto obliga a definir permisos, límites...
- Memoria: permite continuidad, recuerda contexto de cliente, historial de decisiones. Cambia el diseño porque añade: caducidad, versionado de conocimiento, política de datos...
- Lenguaje natural como API de alto nivel: reduce fricción y democratiza su uso.

Las organizaciones integran workflows de trabajo para usar estos agentes.

---

**Problema 4. Compara los distintos tipos de agentes de la taxonomía (robóticos, de software, cognitivos, generativos) y discute sus implicaciones para el diseño de soluciones organizacionales.**

- Robóticos: actúan en el mundo real; requieren de seguridad funcional, percepción robusta...
- Agentes de software: actúan en sistemas digitales. Rápidos de desplegar, pero existen riesgos en la seguridad y en la escalabilidad. Permiten la automatización de procesos.
- Cognitivos: orientados a objetivos, planificación, modelo de estados... Buenos con procesos con reglas, aunque hay excepciones.
- Generativos: fuertes en lenguaje, flexibilidad... Se requiere un control y son útiles porque permite una traducción usuario-máquina-acción..

---

**Problema 5. Interpretando el gráfico de Alcance de los Agentes Inteligentes, explica cómo se relacionan movilidad, interactividad e inteligencia en el diseño de agentes avanzados.**

Un agente avanzado maximiza simultáneamente tres dimensiones:
- Movilidad: capacidad de operar en distintos espacios
- Interactividad: habilidad para comunicarse y coordinarse
- Inteligencia: calidad de decisión: planning, learning, adaptación, manejo de incertidumbre.

Los agentes más avanzados son los que equilibran las tres: permiten ser operados en el ámbito físico y digital, además de ser altamente interactivos y ser altamente inteligentes.

---

**Problema 6. Diferencia teoría de agentes, sistemas basados en agentes y sistemas multiagente, explicando el cambio de foco de diseño y aportando un ejemplo aplicable a una organización.**

- Teoría de agentes: marco conceptual sobre como modelar a un agente: políticas, utilidad, intenciones...
- Sistemas basados en agentes - ABS: sistema construido como una colección de agentes que simular o ejecutan comportamientos.
- Sistemas multiagentes - MAS: varios agentes autónomos que interactúan para resolver tareas distribuidas.

---

**Problema 7. Explica por qué la simulación basada en agentes es útil para estudiar fenómenos complejos y cómo este enfoque puede aplicarse en contextos organizacionales o urbanos.**

Muchos fenómenos complejos emergen de interacciones locales; no basta con ecuaciones promedio. Ventajas:

- Capturan heterogeneidad
- Modela interacciones y reglas locales
- Permite ver emergencia
- Permite experimentar sin arriesgar la operación real.

---

**Problema 8. Analiza el valor de RoboCup como benchmark de investigación en IA y discute si este tipo de retos sigue siendo relevante en la era generativa.**

Robocup fuerza la integración completa: percepción, control, planning, cooperación, robustez e inferencia en tiempo real en un entorno parcialmente impredecible. 
- Busca fiabilidad, latencias bajas y cierre sensor/motor.
- La evaluación es más objetiva: goles, tiempos, tareas completadas...

---

**Problema 9. Describe las principales ligas de RoboCup y explica qué capacidades de los agentes (percepción, planificación, cooperación, resiliencia…) se ponen a prueba en cada una.**

- Soccer
- Rescue: navegación en entornos dañados, exploración, asignación de tareas, mapas...
- Home: interacción humano-robot, reconocimiento objetos-voz, navegación doméstica, planificación de tareas del hogar.
- Industrial: manipulación, precisión, logística industrial, integración con procesos, seguridad y fiabilidad.

---

**Problema 10. En la liga de Fútbol Tamaño Mediano, analiza los desafíos técnicos relacionados con percepción, planificación y cooperación multiagente en un entorno dinámico.**

Se operen robots con mayor tamaño y velocidad, lo que incrementa retos:
- Percepción: estimar la posición del balón, compañeros, y rivales.
- Planning y control: decisiones en tiempo real con control de trayectoria, evitación de colisiones, considerando errores de actuadores.
- Cooperación multiagente

---

**Problema 11. Explica las diferencias entre las ligas de Fútbol Tamaño Pequeño, Plataforma Estándar y Humanoides, destacando cómo cambian los retos de comunicación, locomoción y autonomía.**

- Small Size League: robots pequeños, control centralizado y visión global externa. Se busca conseguir una estrategia rápida con un control preciso.
- Standard Platform League: misma plataforma para todos (hardware estandarizado). Autonomía distribuida, percepción a bordo, coordinación sin depender de infraestructura externa.
- Humanoids: locomoción bípeda, equilibrio y manipulación más complejos. El reto principal es la locomoción, estabilidad, caídas y recuperación...

---

**Problema 12. Analiza cómo RoboCup Rescue, @Home y @Work ilustran la aplicación de agentes inteligentes en contextos críticos, domésticos e industriales, comparando sus requisitos técnicos y de cooperación.**

- Rescue: prioriza la robustez: navegación en entornos desconocidos, percepción con ruido, planning con bajo riesgo y tiempo. 
- Home: prioriza la interacción natural con humanos: lenguaje, reconocimiento de objetos.
- Work: precisión, reproducibilidad y seguridad funcional.