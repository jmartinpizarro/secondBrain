---
aliases:
  - Ciberseguridad - Lab2
tags:
"References":
cssclasses:
---
# Ciberseguridad - Lab2

## Manejar usuarios y grupos en Linux

Es importante conocer el fichero `/etc/passwd` (ver [[1758200728 - Ciberseguridad - Lab1|Ciberseguridad - Lab1]]).

Para añadir un usuario se usa el comando `useradd` (en sudo o *root*) tal que:
$$\text{useradd user0}$$
Las flags varían dependiendo de los campos:
- $\text{--create-home}$: crea un directorio en `/home`.
- $\text{--password}$: permite insertar una contraseña para el usuario

Cada vez que sea crea un usuario se crea el **grupo primario de dicho usuario**. Puedes ver los grupos en `etc/group`

Para ver todos los grupos a los que pertenece un usuario:
$$groups \space \text{<nameUser>}$$

### Creación de grupos

1. Sin ninguna flash
```bash
group add programadores
```

2. Con alguna flag
```bash
   group add --gid=3333 programadores
   ```

Este grupo comienza inicialmente vacío. Para añadir usuarios a un grupo:

```bash
usermod -aG programadores user0
```

## Permisos

### Máscaras

Las máscaras dicen las acciones (lectura, escritura, ejecución) que puede hacer cualquier usuario cuando se crea por defecto un archivo/fichero.

```bash
umask
```


### chmod

Permite modificar permisos de los archivos. Existen varias variante:
- **Octal**: `chmod 664 file.txt`, donde para cada dígito es (usuarios, grupos, otros)
- **ugoa**: `chmod g+w, o+w prueba.txt` (estamos modificando grupos y otros) , especificas una de las clases (usuarios, grupos, otros) y especificas qué permiso quieres añadir/quitar.