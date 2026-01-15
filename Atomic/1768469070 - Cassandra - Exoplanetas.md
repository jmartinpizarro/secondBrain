---
aliases:
  - Cassandra - Exoplanetas
tags:
"References":
cssclasses:
---
# Cassandra - Exoplanetas

Una agencia científica desea almacenar información sobre **exosistemas planetarios** y sus **planetas** en una base de datos **Apache Cassandra** para dar soporte a un sistema de consulta de alta disponibilidad.

El sistema **no requiere transacciones complejas ni análisis agregados**, pero debe responder de forma eficiente a un conjunto fijo de consultas.

Requisitos funcionales

Cada planeta se caracteriza por:

- nombre
- tipo (`rocky`, `gas`, `ice`)
- masa (en masas terrestres)
- si se encuentra o no en la zona habitable
- fecha de descubrimiento

Cada planeta pertenece a **un único exosistema**, identificado por su nombre.

Consultas que el sistema debe soportar

1. Obtener **todos los planetas** de un exosistema dado.  
2. Obtener **los planetas habitables de un exosistema**, ordenados por masa de forma descendente.
3. Obtener **todos los planetas de un tipo concreto**.
4. Obtener **los planetas de un exosistema descubiertos a partir de una fecha dada**.

---

1. Apache Cassandra es una base de datos no relacional orientada a OLTP, eventualmente consistente y muy veloz. Esto supone una gran velocidad para las escrituras y una velocidad también relevante para las lecturas si se modela correctamente la base de datos.
2. Con respecto a normalizar los datos (incluir todos únicamente en una sola tabla), eso no es recomendable en Cassandra. Este tipo de bases de datos no tiene aggregates ni JOIN lo que reduce las formas de modelar la base de datos. Siempre se busca hacer una tabla por query, para así optimizar el proceso.
3. A continuación se añade una script CQL para la creación de las bases de datos.

```sql
DROP KEYSPACE IF EXISTS exosystems;

CREATE KEYSPACE exosystems WITH REPLICATION = {
	'class' : 'SimpleStrategy',
	'replication_factor' : 1
}

USE exosystems;

-- datos de todos los planetas dado un exosistema dado
CREATE TABLE planets_by_system (
  system_name text,
  planet_name text,
  planet_type text,
  mass double,
  habitable boolean,
  discovered_at date,
  PRIMARY KEY ((system_name), planet_name)
);

-- obtener los planetas habitables de un exosistema, ordenados
-- por masa de manera descendente
CREATE TABLE habitable_planets_by_system (
  system_name text,
  mass double,
  planet_name text,
  planet_type text,
  discovered_at date,
  PRIMARY KEY ((system_name), mass, planet_name)
)
WITH CLUSTERING ORDER BY (mass DESC);


-- obtener todos los planetas de un tipo en concreto
CREATE TABLE planets_by_type (
  planet_type text,
  system_name text,
  planet_name text,
  mass double,
  habitable boolean,
  discovered_at date,
  PRIMARY KEY ((planet_type), system_name, planet_name)
);

-- obtener todos los planetas descubiertos a partir de una
-- fecha determinada
CREATE TABLE planets_by_system_and_date (
  system_name text,
  discovered_at date,
  planet_name text,
  planet_type text,
  mass double,
  habitable boolean,
  PRIMARY KEY ((system_name), discovered_at, planet_name)
);
```

4. A continuación se escriben las queries sobre las tablas anteriores:

```sql
-- datos de todos los planetas dados
SELECT *
FROM planets_by_system
WHERE system_name = 'TRAPPIST-1';

-- planetas habitables, ordenado por masa de manera descendente
SELECT *
FROM habitable_planets_by_system
WHERE system_name = 'TRAPPIST-1';

-- todos los planetas de un tipo
SELECT *
FROM planets_by_type
WHERE planet_type = 'rocky';

-- obtenr todos los planetas descubiertos a partir de x fecha
SELECT *
FROM planets_by_system_and_date
WHERE system_name = 'TRAPPIST-1'
AND discovered_at > '2018-01-01';
```

5. Todas las queries que no se encuentren o se puedan lograr dentro de dichas tablas supondrán un problema.
6. COLUMN CLUSTERING facilita y optimiza ORDER BY de manera física en el guardado de archivos durante su inserción; de esta manera se encuentran de manera adyacente/cercana en los registros y es más rápido realizar dichas queries.