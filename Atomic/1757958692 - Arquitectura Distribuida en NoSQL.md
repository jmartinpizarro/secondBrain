---
aliases:
  - Arquitectura Distribuida en NoSQL
tags:
"References":
cssclasses:
---
# Arquitectura Distribuida en NoSQL

- **Fragmentación horizontal**: división por filas.
	- Técnicas de dispersión, basadas en hash (clave-valor)
	- En función del valor de atributos (BBDD orientadas a documentos, a columnas)
- **Fragmentación vertical**: división por columnas.
- **Replicación masiva de los datos**: en diferentes servidores (nodos)
- Ventajas:
	- Incrementar el nivel de paralelismo
	- Mejorar eficiencia de consultas