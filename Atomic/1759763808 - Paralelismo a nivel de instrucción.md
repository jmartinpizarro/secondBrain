---
aliases:
  - Paralelismo a nivel de instrucción
tags:
"References":
cssclasses:
---
# Paralelismo a nivel de instrucción

**Segmentación**: técnica de implementación en la que una la ejecución de múltiples instrucciones se solapan en el tiempo.
- Se divide una operación costosa en varias sub-operaciones simples.
- Ejecución de las sub-operaciones por etapas.

**Aumenta** el *throughput*.
**No aumenta** la latencia.

## Etapas

- **Captación**
	1. Envío de PC de memoria
	2. Lectura de instrucción
	3. Actualización de PC
- **Decodificación**
	1. Decodificación de instrucción
	2. Lectura de registros
	3. Extensión de signos de desplazamientos
	4. Cálculo de posible dirección de salto
- **Ejecución**: operación de ALU sobre operandos
	- **Referencia a memoria**
	- **Instrucciones registro/registro**
	- **Instrucciones registro/dato inmediato**
	- **Bifurcación condicional**
- **Memoria**: lectura o escritura a memoria
- **Post-escritura**: escritura de resultado en banco de registros 

## Riesgos

Situación que impide que la siguiente instrucción pueda comenzar en el ciclo de reloj previsto. Los riesgos reducen el rendimiento de las arquitecturas segmentadas.

- Riesgo estructural: el hardware no puede soportar todas las posibles secuencias de instrucciones. Evitable pero encare el hardware.
- Riesgo de datos: la segmentación modifica el orden de accesos de lectura/escritura a los operandos.
	- **RAW**: Read After Write. La instrucción $i+1$ trata de leer un dato antes de que la instrucción $i$ lo escriba. **Solución**: envío adelantado (*[[1759771491 - Forwarding de datos|Forwarding de datos]]*)
	- **WAR**: Write After Read. No puede ocurrir en un pipeline de 5 etapas. **Solución**: renombrado de registros estático por compilador o dinámico por hardware.
	- **WAW**: Write After Write. No puede ocurrir en un pipeline de 5 etapas. **Solución**: renombrado de registros estático por compilador o dinámico por hardware.
- [[1760368441 - Riesgos de control|Riesgos de control]]

Aproximación simple ante riesgos:
- Detener el flujo de instrucciones
- Las instrucciones que ya han iniciado continúan.

## Predicción de saltos

Existen varios tipos:
- Predicción basada en perfil de ejecución:
	- Se ejecuta una vez para recoger estadísticas
	- Se utiliza la información para modificar el código
- [[1760370284 - Predicción dinámica - BHT|Predicción dinámica - BHT]]

## Aprovechamiento de ILP

ILP aplicable directamente a bloques básicos.

**Bloque básico**: secuencia de instrucciones sin saltos.
Programa típico en procesadores RISC.
- Tamaño medio de bloque básico de 3 a 6 instrucciones.
- Poco aprovechamiento de ILP dentro del bloque.

---

- **Aprovechamiento de paralelismo**: 
	- Entrelazar ejecución de instrucciones no relacionadas
	- Rellenar detenciones con instrucciones
	- No alterar los efectos del programa original