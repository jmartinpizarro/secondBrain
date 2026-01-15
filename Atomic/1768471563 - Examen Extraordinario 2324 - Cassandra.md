---
aliases:
  - Examen Extraordinario 2324 - Cassandra
tags:
"References":
cssclasses:
---
# Examen Extraordinario 2324 - Cassandra

Se requiere diseñar una solución en Apache Cassandra para persistir y gestionar eficientemente la interacción de usuarios con portales temáticos. Cada portal temático posee atributos como nombre, año de creación, país, URL y contiene varios temas y artículos. Para cada tema se desea guardar detalles significativos, mientras que de cada artículo digital se debe registrar el título, los autores y palabras clave para la indexación en motores de búsqueda.

Los usuarios se registran proporcionando datos personales y temas de interés. Pueden interactuar con los contenidos dejando comentarios en los artículos. Cada comentario incluye un título, cuerpo de texto, calificación y la fecha de creación. Los usuarios pueden marcar con 'me gusta' artículos y comentarios. También se desea almacenar las interacciones de 'me gusta', incluyendo la fecha en que se realizan.

Los casos de uso identificados para el diseño inicial incluyen:

- CU 1. Recuperar todos los artículos de un portal específico, filtrados por año de publicación, y ordenar estos resultados de forma ascendente por año.
- CU 2. Consultar todos los artículos de un autor específico, ordenados ascendente por año de publicación.
- CU 3. Consulta de todos los usuarios que han marcado 'me gusta' en un artículo específico.
- CU 4. Identificar a los usuarios que han dado 'me gusta' a artículos que coinciden con sus temas de interés.

Detalla las tablas y describe su estructura, incluyendo las claves de partición y claves de clustering adecuadas para optimizar las consultas de acuerdo con los casos de uso anteriormente indicados. Explica el porqué de tus decisiones.


```sql
-- CU 1: recover all articles of an specific portal
CREATE TABLE articles_by_portal_year (
	portal_name text,
	publish_year int,
	article_id uuid,
	title text,
	authors list<text>,
	tags set<text>,
	country text,
	url text,
	PRIMARY KEY ((portal_name, publish_year), article_id)
);

-- CU 2: get every article from an specific author, ascendant ordering
-- by published date
CREATE TABLE articles_by_author (
	author_name text,
	publish_year int,
	article_id uuid,
	portal_name text,
	title text,
	tags set<text>,
	PRIMARY KEY ((author_name), publish_year, article_id)
);

-- CU 3: get all users that have liked an article
CREATE TABLE likes_by_article (
	article_id uuid,
	like_date date,
	user_id uuid,
	user_name text,
	PRIMARY KEY (article_id, like_date, user_id)
);

-- CU 4
CREATE TABLE likes_by_interest (
	user_id uuid,
	interest text,
	article_id uuid,
	like_date date,
	PRIMARY KEY ((user_id, interest), like_date, article_id)
) WITH CLUSTERING ORDER BY (like_date DESC);
```