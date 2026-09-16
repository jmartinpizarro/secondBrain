---
aliases:
  - Taxonomía de Flynn
tags:
"References":
cssclasses:
---
# Taxonomía de Flynn

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