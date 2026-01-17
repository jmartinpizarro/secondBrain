---
aliases:
  - Seminarios - Inteligencia de Enjambre y Sistemas Multiagente
tags:
"References":
cssclasses:
---
# Seminarios - Inteligencia de Enjambre y Sistemas Multiagente

**Problema 1. Explica los principios clave de la Inteligencia de Enjambre (autoorganización, estigmergia, emergencia y adaptación) y analiza cómo la interacción local entre agentes simples puede generar comportamientos globales complejos.**

La inteligencia de enjambre se inspira en sistemas naturales (hormigas, abejas, termitas) donde agentes simples, sin control central producen comportamientos altamente eficaces.

- Autoorganización: cada agente sigue reglas locales simples y el sistema converge espontáneamente a estructuras o patrones útiles.
- Estigmergia: comunicación indirecta a través del entorno. Un agente modifica el entorno y otros agentes responden a dichas modificaciones. Esto reduce la necesidad de comunicación explícita y mejora la escalabilidad.
- Emergencia: propiedades globales no están programadas explícitamente en ningún agente individual. Surgen de la interacción repetida entre agentes y entorno.
- Adaptación: el sistema responde a cambios, ajustando patrones colectivos: rutas que refuerzan/debilitan, redistribución de agentes...

Interacciones locales + reglas simples + retroalimentación.

---

**Problema 2. Compara los Sistemas de Enjambre y los Sistemas Multiagente (MAS) en términos de autonomía, comunicación, capacidad de coordinación, heterogeneidad, planificación y adecuación a diferentes tipos de problemas organizacionales.**

| Dimensión               | Sistemas de Enjambre                                     | Sistemas Multiagente (MAS)                                     |
| ----------------------- | -------------------------------------------------------- | -------------------------------------------------------------- |
| **Autonomía**           | Alta, pero con reglas simples y locales                  | Alta, con agentes más complejos                                |
| **Comunicación**        | Indirecta, implícita (estigmergia)                       | Explícita (mensajes, protocolos)                               |
| **Coordinación**        | Emergente, no planificada globalmente                    | Deliberada, mediante negociación/roles                         |
| **Heterogeneidad**      | Baja o moderada (agentes similares)                      | Alta (agentes con roles/capacidades distintas)                 |
| **Planificación**       | Mínima o inexistente a nivel individual                  | Planificación individual y/o colectiva                         |
| **Escalabilidad**       | Muy alta                                                 | Media–alta (depende del protocolo)                             |
| **Robustez**            | Muy alta (tolerancia a fallos)                           | Alta, pero más sensible a fallos clave                         |
| **Problemas adecuados** | Optimización distribuida, exploración, balanceo, routing | Asignación de tareas, negociación, flujos de trabajo complejos |

---

**Problema 3. Describe los principales mecanismos de coordinación y comunicación utilizados en sistemas multiagente (por ejemplo, estigmergia, FIPA-ACL, KQML, Contract Net Protocol) y explica cómo permiten lograr cooperación efectiva en sistemas distribuidos sin control centralizado.**

Los MAS usan distintos tipos de coordinación:
- Estigmergia: comparación indirecta vía entorno. Favorece escalabilidad y robustez, reduciendo control fino y explicabilidad.
- FIPA-ACL: lenguaje estándar de comunicación entre agentes con actos comunicativos (inform, request, agree...). Permite interoperabilidad y coordinación explícita.
- Knowledge Query and Manipulation Language - KQML: enfocado en intercambio de conocimiento. Útil en sistemas basados en conocimiento distribuido.
- Contract Net Protocol - CNP: un agente orquestador anuncia una tarea, el resto la oferta, adjudicándose el contrato. Facilita asignación distribuida de tareas. 

---

**Problema 4. Analiza el caso práctico presentado por tu grupo dentro del seminario y explica qué aporta el enfoque distribuido o de enjambre frente a soluciones centralizadas, considerando ventajas, limitaciones y retos.**

En simulación urbana de evacuaciones: cada peatón se modela como un agente humano con estados internos y una tasa de pánico. Permite:
- Capturar comportamientos no lineales e irracionales.
- Representar interacciones locales entre individuos en el entorno.
- Modelar el peligro como agente activo.

Además, se puede comprobar la robustez y seguridad en sistemas críticos como en la red eléctrica.