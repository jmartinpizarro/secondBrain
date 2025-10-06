---
aliases:
  - Repositorios de Datos
tags:
"References":
cssclasses:
---
# Repositorios de Datos

### BBDD Relacionales

- Estructura y esquema bien definido
- Datos homogéneos
- Formato tabular
- Lenguaje de consulta estándar: SQL
- Normalización de los datos
- Procesamiento confiable de las transacciones: siguen la normativa **[[1758545176 - ACID]]**, atomicidad, consistencia, aislamiento y durabilidad

### BBDD NoSQL

Surgen en respuesta al volumen, diversidad y velocidad a la que se generan los datos en la actualidad, principalmente debido a los avances en la computación en la nube, IoT.

Se usan para procesar datos de manera masiva.

Propiedades **BASE**: coherencia eventual flexible básicamente disponible.

- **Basically Available**: básicamente disponible para todos los usuarios de forma simultáneamente.
- **Soft State**: datos flexibles con estados transitorios
- **Eventually consistent**: la coherencia se alcanza tras completarse las actualizaciones simultáneas.

### Data Warehouses

Repositorio central que fusiona información proveniente de diversas fuentes a través de un proceso ETL de extracción, transformación y carga.

Orientado al análisis y el Business Intelligent.

Históricamente ha sido relacionado, pero con la aparición de NoSQL también se utilizan esta tipología de warehouses.

Se basa en una **arquitectura de tres niveles**:
1. **Nivel inferior**: incluye los servidores de las bases de datos que extraen los datos de diversas fuentes
2. **Nivel intermedio**: incluye un servidor OLAP (procesamiento analítico online) que permite a los usuarios procesar y analizar la información que proviene del nivel inferior
3. **Nivel superior**: capa front-end del cliente.

Beneficios de Data Warehouses basados en la nube:
- Costos más bajos.
- Almacenamiento ilimitado.
- Capacidades de cómputo.
- Escala de pago por uso.
- Recuperación rápida ante desastres.

### Data Lakes

Repositorio que permite almacenar grandes volúmenes de datos en **formato crudo**. Esto incluye datos estructurados, semiestructurados y no estructurados.

Sigue una estructura ELT: no es necesario definir la estructura ni el esquema de los datos antes de cargarlos.

Los datos se almacenan directamente tal y como llegan.

### Almacenes Big Data

Infraestructura computacional y de almacenamiento distribuido para almacenar, escalar y procesar conjuntos de datos masivos.

Apache Hadoop proporciona almacenamiento y procesamiento distribuido de grandes conjuntos de datos en clusters en PCs con un hardware básico.
