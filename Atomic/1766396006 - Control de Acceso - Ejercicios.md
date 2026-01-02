---
aliases:
  - Control de Acceso - Ejercicios
tags:
"References":
cssclasses:
---
# Control de Acceso - Ejercicios

**Problem 54**.

Ambos son controles de acceso en los que se especifica quién puede hacer qué (leer, escribir, ejecutar), controlados por el sistema operativo o el *kernel* de seguridad.

- Discretionary Access Control (DAC):
	- El acceso está controlado por el dueño del recurso.
	- Los dueños pueden añadir, quitar o modificar permisos.
	- Implementados usando ACLs o permisos de UNIX.
	- **Permisos pueden ser propagados de manera no intencionada**
- Mandatory Access Control (MAC):
	- Política para todo el sistema controlada por una autoridad central.
	- Usuarios y objetos tienen *tags* de seguridad (ex. niveles de clasificación)
	- No pueden romper el resto de reglas

---

**Problem 55**.

1. El principio de seguridad simple permite que cualquier usuario que tenga mayor nivel que un objeto (archivo) pueda ver su contenido sin ningún problema. Esto permite que solo los usuarios con suficiente nivel en la jerarquía pueden ver datos clasificados.
2. Por otra parte, solamente se puede escribir en ficheros que tenga un mínimo nivel de seguridad respecto a $C(s)$. Esto se hace para evitar que los ficheros se filtren por canales no seguros con menor seguridad (escribir información confidencial en archivos con muy pocos permisos).

---

**Problem 57**.

**Escenario de Tranquilidad Fuerte**
Servidor de bases de datos de inteligencia militar - altamente clasificado. Los niveles de seguridad de los archivos se configuran en el momento de arranque y no se pueden cambiar mientras el sistema está en funcionamiento. Evita cualquier posibilidad de errores de reclasificación accidental o ataques.

Preferida en sistemas de alta seguridad.

**Escenario de Tranquilidad Débil**
Sistema de gestión documental gubernamental que sigue el Principio de la Marca de Agua Alta. Un proceso comienza con un nivel de seguridad bajo. A medida que el proceso lee archivos, el sistema eleva automáticamente el nivel de seguridad del proceso a Confidencial para reflejar el nivel de los datos que está manejando. Se debe de mantener las condiciones descritas en el **Problem 55**.

Preferida en entornos dinámicos/operativos; mayor flexibilidad, permite implementar el principio del menor privilegio...

---

**Problem 58**

>[!DANGER]  **TODO: Problem 58** - ACM Matrix Exercise

---

**Problem 59**

El control de acceso se gestiona a través de dos mecanismos: **bits de permiso de UNIX** y las **listas de control de acceso (ACL)**.

- Bits de permiso: modelo fijo y tripartido, cada objeto tiene 9 bits (rwxrwxrwx) que se dividen en varias categorías: propietario, grupo y otros. Eficiente en almacenamiento, simple y buena en rendimiento; pero falta flexibilidad.
- Listas de control de acceso (ACL): mecanismo flexible y variable que extiende el modelo tradicional. Permite asociar un objeto a una lista de entradas, donde cada una especifica permiso para un usuario o un grupo concreto. 

Cuando queremos rapidez y simplicidad, tenemos que usar los bits de permiso. Sin embargo, cuando queremos una política de seguridad minuciosa buscamos las ACL.

---

**Problem 60**

Si un usuario tiene permiso para leer un archivo, cualquier programa ejecutado por ese usuario también tiene permiso para leerlo. 

1. El usuario A tiene un archivo con información sensible llamado `nomina.txt`
2. El atacante B crea un programa con forma de juego que le envía al usuario A.
3. El usuario A ejecuta el programa. El programa parece ser legítimo, pero por atrás se ejecuta un código que intenta abrir `nominas.txt` para acceder al contenido.

---

**Problem 61**

Ambos procesos saben que solo un proceso puede acceder a un fichero al mismo tiempo - actúa como limitación bloqueante.

$$bloqueo = \begin{cases}  1 & \text{archivo está siendo accedido} \\ 0 & \text{en caso contrario}\end{cases}$$

El proceso B es capaz de leer el contenido binario y convertirlo a un ASCII. Entonces, el proceso A va a leer bit a bit el contenido del fichero `secrets.txt`. Cuando lo lea, bloquea el otro fichero; lo que envía un 1 al proceso B. Más tarde, el proceso A puede enviar un 0 para ir codificando el mensaje, mientras que el proceso B lo recibe y luego lo descifra.

**Problem 63**

No son equivalentes, aunque pueden usarse para implementar una versión simplificada de dicho sistema. Sin embargo, no hay flexibilidad y existe la falta de herencia.

*Ejemplo: si quieres que el director de IT tenga permisos de Técnico e Ingeniero, tendrás que meter al usuario en tres grupos distintos.*

## Linux Access Control

---

**Problem 66**

```
1. rwxrwxr-x
2. rwxr--r--
3. r--r-----
4. rwxr-xr-x
5. rwxrw-r-x
6. r-x--x--x
7. -w-r----x
8. -----xrwx
```

Se convierte a:

```
1. chmod u=rwx, g=rwx, o=rx 
2. chmod u=rwx, g=r, o=r
3. chmod u=r, g=r, o=
4. chmod u=rwx, g=rx, o=rx
5. chmod u=rwx, g=rw, o=rx
6. chmod u=rx, g=x, o=x
7. chmod u=w, g=r, o=x
8. chmod u=, g=x, o=rwx
```

---

**Problem 67**

```
1. rwxrwxrwx
2. --x--x--x
3. r---w---x
```

Se convierte a:

```
1. chmod 777 archivo
2. chmod 111 archivo
3. chmod 421 archivo
```

---

**Problem 68**

```
1. 022 -> u=, g=w, o=w
2. 011 -> u=, g=x, o=x
3. 541 -> u=rx, g=r, o=x
4. 777 -> u=rwx, g=rwx, o=rwx
```

---

**Problem 69**

1. Lee el fichero.
2. No puede eliminar el fichero.
3. Por defecto, se elimina el permiso de escritura a `staff`, por lo que no podría modificar el contenido.

---

**Problem 70**

1. Sí, si que puede. Inicialmente la *mask* pasa de 666 a 640 (666 - 027). El usuario tiene permisos totales menos de ejecución, que más tarde se le dan.
2. Sí, ya que solo requiere r-x.
3. Sí, ya que solo hemos añadido permisos a los grupos, no hemos modificado a los usuarios.
4. No, ya que jpc:rw- y la máscara era r-x, por lo que la unión r--

---

**Problem 71**

Esta metodología se basa en las *files capabilities*, donde un comando no requiere ser usado por *root*, sino que en teoría puede tener ciertos permisos a ciertas capacidades (*capabilities*) que no requieren la totalidad del root.

---

**Problem 72**

- **ruid**: el UID del usuario que inició el proceso. Permite identificar el dueño real del proceso.
- **euid**: *effective UID*. El UID que el *kernel* usa para comprobar permisos. Determina qué puede hacer realmente el proceso.
- **suid**: *saved set-UID*. Copia del euid en el kernel; permite bajar privilegios temporalmente y recuperarlos después sin ejecutar de nuevo el binario.

---

**Problem 73**

Proteger archivos de otros usuarios en directorios compartidos, incluso cuando todos tienen permiso de escritura.

Cuando se añade un *sticky bit*, solo se puede renombrar o borrar un archivo:
- El propietario del archivo
- El propietario del directorio
- root

---

