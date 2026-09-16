---
aliases:
  - Introducción a la planificación automática
tags:
"References":
cssclasses:
---
# Introducción a la planificación automática

**Estado**: "pantallazo" del momento, de la realidad
**Acción u operador**: transformación de un estado a otro
**Estado inicial y final**
**Objetivo o meta**
**Plan**: secuencia de acciones que permiten la transición de un estado inicial a un estado meta
**Heurística**: función de conocimiento que permite la generación eficiente de un plan 

---

**Modelo de lenguaje**: PDDL. Set de descripciones de acciones.
**Problema**: estado inicial, conjunto de metas, métricas a optimizar.
Se busca obtener un **set de acciones** que consigue alcanzar a la meta desde el estado inicial, optimizando la métrica al mismo tiempo.

--- 

**Scheduling**

Dado un :
- set de acciones
- una serie de restricciones con precedencia, aspectos temporales y recursos
Obtener una asignación de un recurso temporal a las actividades