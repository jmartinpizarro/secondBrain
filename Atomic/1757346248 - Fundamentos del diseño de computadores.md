---
aliases:
  - Fundamentos del diseño de computadores
tags:
"References":
cssclasses:
---
# Fundamentos del diseño de computadores

## Perspectiva histórica

### Primera Revolución: microprocesador

Suficientes transistores en un único chip para un procesador de 16 bits. Más rápido y más barato. Nacen las computadoras de escritorio, CD/DVD, MP3, GPS...

Eliminación casi total de la necesidad de programación en ensamblador.

### Segunda Revolución

Extracción del paralelismo implícito a nivel de instrucción (ILP), pero el hardware tenía recursos que podían usarse en paralelo.

**Elementos**:
- Segmentación: permitió incrementar frecuencias del reloj
- Caché: necesarias para incrementar las frecuencias del reloj.
- Coma flotante: integradas en el chip.
- Emisión múltiple: arquitecturas superescalares.
- Planificación dinámica: ejecución fuera de orden.

### Tercera Revolución

Soporte a paralelismo explícito de datos y de hilos.
- Hardware ofrece recursos paralelos y software especifica su uso
- El paralelismo deja de ser ocultado por el hardware
- **Razón**: beneficios cada vez menores de ILP

### Tendencias arquitectónicas

- Paralelismo a nivel de instrucción
- Nuevos modelos para mejorar el rendimiento
	- Data-Level Parallelism
	- Thread-Level Parallelism
	- Request-Level Parallelism

## Clasificación de computadores

- IoT de las cosas y computación empotrada
- Dispositivos Móviles Personales
- Computadores de escritorio
- Servidores
- Clústeres y Computadores de Escala de Almacén

## Paralelismo

- Paralelismo de datos: una operación aplicada a muchos datos.
- Paralelismo de tareas: tareas operan independientemente y en paralelo.

### Paralelismo Hardware

- ILP: Instruction-Level Parallelism
- Arquitecturas vectoriales y GPUs
- TLP: Thread-Level Parallelism
- RLP: Request-Level Parallelism

### Taxonomía de Flynn

Primeras dos letras, número de instrucciones; dos últimas letras, número de datos devueltos

Una clasificación de arquitecturas paralelas posibles.
- **SISD**: SIngle Instruction Stream / Single Data Stream.
	- Mono-procesador
	- Puede usar técnicas de ILP
- **SIMD**: Single Instruction Stream / Multiple Data Streams
	- Las mismas instrucciones ejecutadas por procesadores diferentes sobre datos distintos.
	- *Alternativas*: procesadores vectoriales, extensiones multimedia y GPUs
- **MISD**: Multiple Instructions Streams / Single Data Stream
	- No se conocen implementaciones comerciales
- **MIMD**: Multiple Instructions Streams / Multiple Data Streams

## Arquitectura del computador

