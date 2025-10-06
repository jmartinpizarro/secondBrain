---
aliases:
  - Control de acceso
tags:
"References":
cssclasses:
---
# Control de acceso

## Acceso de control y políticas

**Protección**: separación de procesos en un sistema para restringir acceso a recursos.

### Políticas DAC (de Control de Acceso)

Cada objeto en el sistema tiene un dueño.
Existe una política determinada por el usuario de un objeto.

Una política de acceso a través de todo el sistema se puede representar a través de una **Matriz de Acceso de Control** (usuario-objeto) que se puede implementar como:
- Access Control List (ACL)
- Capabilities

## Políticas MAC

Se centran en la protección de objetos altamente sensitivos. Se tiene acceso si hay una serie de reglas explícitas que lo habiliten.

Sujetos y objetos tienen etiquetas sensibles que reflejan su nivel de confianza -> el acceso se basa en dichas etiquetas.

Las etiquetas suelen basarse en una estructura.
## Implementación en Linux

### Security Calculation -  Cálculo de seguridad

Cada vez que un sujeto $S$ realiza un acceso al objeto $O$ en modo de acceso $M$, se realiza un cálculo de seguridad para ver si puede acceder o no.

Toma las credenciales del sujeto y del objeto, además del modo, y a través de una serie de reglas comprueba si se puede acceder (no tiene que ver con Políticas MAC).

- **Objetos**: entidades del sistema que pueden actuar directamente en programas del espacio de usuario: procesos, ficheros, sockets, colas, semáforos...

Los objetos tiene una serie de credenciales que dependen del tipo del objeto. Existe el **object ownership**: de entre todas las credenciales hay un subset para saber quién es dueño de este objeto.

- **Sujeto**: entidades que pueden actuar sobre objetos. La mayoría de objetos son inactivos excepto los procesos.
- **Acciones**: lo que un sujeto realiza sobre un objeto: leer escribir, crear, *fork*, señales...

### Credenciales de procesos

A parte del *UID*, existe el **EUID** (Effective User ID) -> investigar porque me dio pereza copiar.

### Sistema de permisos

Una forma limitada del ACL donde los sujetos están agrupados en:
- **owner**
- **groups**
- **everyone else**

Y hay tres tipos de permisos:
- **leer**
- **escribir**
- **ejecutar**

