---
aliases:
  - Introducción a las Arquitecturas de datos
tags:
"References":
cssclasses:
---
# Introducción a las Arquitecturas de datos

## Ecosistema de los datos

### Tipos de datos

- **Estructurados**: formato rígido, esquema o estándar. Organizados en filas o columnas
- **Semiestructurados**: características consistentes, pero no se ajustan a una estructura fija. Contiene etiquetas o metadatos para ser organizados en una jerarquía (JSON, XML).
- **No estructurados**: no siguen ningún tipo de semántica, formato o regla en particular. Son datos complejos y con **información cualitativa** (que no se puede medir). 
	- Publicaciones en redes sociales
	- Documentos de procesadores de texto
	- Contenido multimedia

El tipo de dato **determina el tipo de repositorios de datos** en los que se pueden almacenar, y también las herramientas que se pueden utilizar para procesarlos.

- Datos estructurados -> DDBB Relacionales, Data Warehouses
- Datos semiestructurados -> DDBB NoSQL, Data Lake
- Datos no estructurados -> Data Lake, Big Data
### Tipos de metadatos

**Metadatos**: datos que proporcionan contexto sobre otros datos. Añaden contexto, facilitando búsqueda, gestión y calidad.

- **[[1757423859 - Metadatos Técnicos|Metadatos Técnicos]]**: estructura de la tabla
- **[[1757423915 - Metadatos de procesos|Metadatos de procesos]]**: cuándo y cómo se actualiza (ETL cada 24h)
- **[[1757423993 - Metadatos de negocio|Metadatos de negocio]]**: qué representan los campos ("importe" = total de venta con "IVA")
- **[[1757424001 - Metadatos de gestión|Metadatos de gestión]]**: quién es responsable y bajo qué política de acceso.

### Buenas Prácticas

![[Pasted image 20250909152442.png]]

## Ciclo de vida de los datos

1. **Adquisición de datos**: se establece qué datos recopilarse, además de una **base legal**. Se establece el uso previsto de estos datos y su política de privacidad y los propósitos.
2. **Procesamiento de datos**: se establece cómo se va a procesar los datos y cuál es la base legal para el procesamiento de estos datos (normalizar los datos, anonimizar datos personales). 
3. **Almacenamiento de datos**: se establece dónde se van a almacenar los datos, y las medidas a tomar para evitar problemas y amenazas de seguridad internas o externas.
4. **Intercambio de datos**: se establece qué proveedores externos de la cadena de suministro pueden tener acceso a los datos. Se define la responsabilidad de forma contractual sobre cómo hacer esos accesos.
5. **Conservación o eliminación de los datos**: se establecen políticas y procesos a seguir para la conservación o eliminación de datos personales después de un tiempo designado.

>[!DANGER]
>Importante tener un **registro auditable** en estas etapas.

## Gobernanza de los datos

**Gobernanza de los datos**: conjunto de políticas, procesos y roles que aseguran que los datos se gestionen de forma **eficiente, segura y con valor para la organización**, alineando tecnología, negocio y cumplimiento legal.

>[!NOTE]
>La gobernanza de datos convierte los datos en un activo estratégico para la toma de decisiones y la innovación.

Cabe destacar que existen [[1757958991 - Roles y responsabilidades respecto a los datos|Roles y responsabilidades respecto a los datos]] por parte de las entidades.

### Cadena de valor de los datos

La gobernanza no se encarga solo del control de los datos, sino que también garantiza que los datos sean un **activo valioso** que aporten valor al negocio -> **los datos son el núcleo del negocio**.

Surge el valor al combinar:
- **Datos** (volumen, diversidad, calidad)
- **Herramientas y plataformas**
- **Experiencia humana**

$$\text{Datos} \rightarrow \text{Herramientas y plataformas} \rightarrow \text{Experiencia Humana} = \text{VALOR EMPRESARIAL}$$

### Calidad de los datos

Se asegura que los datos sean útiles y confiables. Que contengan las siguientes características:

- **Completitud**: se conoce el dominio completo del dato
- **Unicidad**: sin duplicados
- **Precisión**: reflejan la realidad
- **Conformidad/Validez**: cumplen reglas y formatos
- **Oportunidad**: disponibles en el momento necesario
- **Procedencia**: se conoce el origen y la trazabilidad

### Dinámica de trabajo

1. **Definir y mantener los estándares**. Definir y mantener definiciones comunes, formatos, acceso y cumplimiento.
2. **Establecer responsabilidades de los datos**. Asignar roles claros.
3. **Gestionar el proceso completo de desarrollo de datos y comunicar cambios**. Verificación, evolución de datos y comunicación de actualizaciones.
4. **Proporcionar información acerca del entorno de datos**. Uso de metadatos, seguimiento de la procedencia y evaluación de calidad.

## Repositorios de los datos

Lugar donde se ha recopilado, organizado y aislado datos para que puedan ser utilizados, analizados o consultados.

**Bases de datos**: colección de datos diseñada para la entrada, almacenamiento, búsqueda, recuperación y modificación. Un Sistema de Gestión de Bases de Datos (DBMS) son un conjunto de programas que crean y mantienen la base de datos.

Existen distintos [[1757958560 - Repositorios de Datos|Repositorios de Datos]].
## Integración de datos

Abarca técnicas y herramientas que permiten a las organizaciones **acceder, transformar y almacenar datos de diferentes tipos**.

Las plataformas de integración combinan múltiples fuentes de datos, ya sean físicas o lógicas, para ofrecer una vista unificada y facilitar el análisis.

1. Recolección
2. Procesamiento
3. Limpieza
4. Integración (cruzar ventas con campañas)
5. Los usuarios necesarios tienen acceso y estudian los datos.

### Pipelines de datos

Conjunto de herramientas y procesos que cubren todo el ciclo de vida de los datos, desde los sistemas de origen hasta su destino final.

Los datos se integran dentro de una **pipeline de datos** utilizando dos procesos principales:
- **ETL (Extract-Transform-Load)**: transformación ocurre antes de la carga. Se obtiene un control de calidad antes de cargar, cumple con normativas pero **es un proceso más lento y poco flexible**.
- **ELT (Extract-Load-Transform)**: los datos se cargan primero y luego se transforman en el destino. $\exists$ escalabilidad, rapidez y **flexibilidad**, aunque puede llevar a datos inconsistentes.  
## Arquitectura de plataformas de datos

La arquitectura comprender **varias capas** que permiten el **procesamiento, almacenamiento y análisis de grandes volúmenes de datos**. 

Cada capa tiene un papel esencial en realizar funciones específicas dentro del ciclo de vida de los datos.

1. [[1757943227 - Capa de Obtención de Datos|Capa de Obtención de Datos]] (Data Ingestion and Data Collection Layer)
2. [[1757943288 - Capa de almacenamiento e integración|Capa de almacenamiento e integración]] (Data Storage and Integration Layer)
3. [[1757943327 - Capa de procesamiento de datos|Capa de procesamiento de datos]] (Data Processing Layer)
4. [[1757943370 - Capa de visualización y consumo|Capa de visualización y consumo]] (Analysis and User Interface Layer)
5. [[1757943491 - Capa de canalización de datos|Capa de canalización de datos]] (Data Pipeline Layer)

## Bases de datos NoSQL

- Orientada a **volumen y velocidad**
- **No es imprescindible** la total **integridad ni coherencia** de la información.
- No hay una solución universal y perfecta para todo
- **Pragmatismo (datos relacionados con el caso de uso), flexibilidad y minimalismo.**
- **BASE vs [[1758545176 - ACID|ACID]]: se puede vivir con un sistema que se sabe que es completo e inexacto, bajo el supuesto que "se pondrá al día" con la verdad.

Tiene tres pilares fundamentales:
- [[1757958638 - Normalización en NoSQL|Normalización en NoSQL]]
- [[1757958668 - Escalabilidad horizontal|Escalabilidad horizontal]]
- [[1757958692 - Arquitectura Distribuida en NoSQL|Arquitectura Distribuida en NoSQL]]

### Ventajas e inconvenientes

**Ventajas**:
- Enfoque en los sistemas abiertos
- Orientación a cluster masivo y poco acoplado
- Orientación a los **datos no estructurados**
	- Ausencia de esquema
	- Relajación de la integridad y consistencia
	- Flexibilidad para adaptarse a las nuevas situaciones
- No hay lenguaje estándar para el acceso de los datos

**Inconvenientes**:
- No soportan modelos de alta fiabilidad ([[1758545176 - ACID|ACID]])
- Trasladan complejidad en el código de las aplicaciones
- No hay estándar
- Esquemas de datos complicados

## Modelos de datos

Se dividen en cuatro, donde los tres primeros son **[[1757959106 - Modelos de agregación|Modelos de agregación]]**:
- [[1757959304 - Modelo clave-valor|Modelo clave-valor]]
- [[1757959542 - Modelo orientado a documentos|Modelo orientado a documentos]]
- [[1757959685 - Modelo orientado a columnas|Modelo orientado a columnas]]
- [[1757959852 - Modelo orientado a grafos|Modelo orientado a grafos]]

