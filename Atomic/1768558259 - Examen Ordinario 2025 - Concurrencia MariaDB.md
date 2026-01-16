---
aliases:
  - Examen Ordinario 2025 - Concurrencia MariaDB
tags:
"References":
cssclasses:
---
# Examen Ordinario 2025 - Concurrencia MariaDB

**1.1.**

- **S1**: REPEATABLE READ guarda el valor de la instancia, da igual las modificaciones que se realicen en la db. Por lo tanto, *books* tendrá los valores que el bucle ha generado previamente, del 1 al 10 respectivamente, con un stock de 20.
- **S2**: Se actualiza el book con id = 1 a un stock de 30, luego se realiza un commit para asegurar que la siguiente sesión vea dicho cambio.
- **S3**: Se actualiza el book con id = 1 a un stock de 25, no hay ningún conflicto porque S2 ya ha realizado un commit antes. Sin embargo, aquí no se realiza un commit todavía, por lo que los cambios todavía no se ven reflejados para el resto de sesiones.

**1.2.**

- **S1**: no se realiza ninguna acción.
- **S2**: se actualiza el stock = 40 a todos los libros con el id igual o superior a 6. No existe ningún conflicto con S3, por lo que se sigue sin ningún problema. No realiza ningún commit.
- **S3**: realiza un rollback al último commit realizado, hecho por S2 en el apartado 1.1, donde id = 1, stock = 30. Luego actualiza stock = 30 si id = 10, entrando en un conflicto con S2, que no ha realizado ningún commit. S2 tiene 50 segundos para hacer un commit, sino S3 dejará de intentar hacer el cambio.

**1.3.**

- **S1**: partiendo de la tabla inicial en 1.1, S1 cambia el stock a 10 si el id = 1, luego realiza un commit, actualizando la tabla. Se realiza una escritura sobre lo obtenido en 1.2, siendo id = 1, stock = 10, y el resto la actualización de 1.2.
- **S3**: se realiza el commit. No hay conflicto con S1. Comienza una nueva transacción, serializable mode esta vez (fuerza secuencial) y con base del commit de S1 de este apartado..
- **S2**: Hace un rollback al último commit realizado, en este caso el de S3 de este apartado. 

**1.4.**

 1. **S3**: se actualiza el stock = 0 para $4 \leq x \leq 7$. Sin commit.
 2. **S2**: Después el stock pasa a ser 50 para el id = 5. Commit; pero está bloqueada por S3. 
 3. **S1**: se borra el book_id = 1, no hay conflictos y se hace commit.
 4. **S3**: se hace commit, actualizando todo S3 -> S2 de manera secuencial.