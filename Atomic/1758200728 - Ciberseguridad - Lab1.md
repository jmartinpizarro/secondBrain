---
aliases:
  - Ciberseguridad - Lab1
tags:
"References":
cssclasses:
---
# Ciberseguridad - Lab1

**UID**: identificador entero positivo de todos los **sujetos** que tienen la capacidad de ejecutar procesos en un sistema.

Se almacenan todos estos identificadores en el archivo `etc/passwd`. 

Sigue un formato separado por `:` tal que:
$$\text{nombre : x : UID\_SUJETO : GID\_GRUPO : INFORMACION : DIRECTORIO\_HOME : shell}$$
$$\text{donde x es la contraseña}$$

Si el $UID == GID$, ese usuario puede pertenecer a otros grupos, conocidos como **grupos suplementarios**. 

Las contraseñas están transformadas en *hashes*, que se pueden encontrar en `etc/shadow`:

$$\text{user : \$ hash \$ \$ salt \$ hash : ...}$$

Usaremos para romper contraseñas [[1758204523 - John The Ripper|John The Ripper]].

