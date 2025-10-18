---
aliases:
  - Predicción dinámica - BHT
tags:
"References":
cssclasses:
---
# Predicción dinámica - BHT

Tabla histórica de saltos (Branch History Table):
- Índice: bits menos significativos de dirección (PC)
- Valor: 1 bit (salto tomado o no la última vez)

**Efectos**:
- Se desconoce si la predicción es correcta
	- Podría venir de otra instrucción situada en una dirección diferente con los mismos bits menos significativos
- Número de bits menos significativos implica tamaño de bufer
	- 10 bits = 1024 entradas
- Si la predicción falla se invierte el bit
- **Desventajas**: bifurcación de bucle falla dos veces.