---
aliases:
  - Vulnerabilidades y Ataques - Ejercicios
tags:
"References":
cssclasses:
---
# Vulnerabilidades y Ataques - Ejercicios

## 5.1 Numbering and Scoring Vulnerabilities

**Problem 113**

El vector de ataque puede tener varios valores:
- Network (N): se propaga a través de la red del sistema, posiblemente a través de todo el internet. Se considera "explotable remotamente"; a nivel de protocolo.
- Adjacent (A): el sistema tiene una vulnerabilidad de protocolo, pero limitada a una topología lógica de adyacencia. Esto significa que el ataque debe ser lanzado:
	- Con una proximidad compartida (Bluetooth, NFC)
	- En la misma red lógica
- Local (L): el sistema vulnerable no está relacionado con la red; sino con el sistema. Existen dos formas:
	- El atacante explota la vulnerabilidad accediendo al sistema objetivo localmente (consola, teclado) o a través de una emulación de terminal (SSH).
	- El atacante requiere de la interacción del usuario (necesita de dos personas) para realizar el ataque (ingeniería social)
- Physical (P): el ataque requiere que el atacante toque o manipule físicamente el sistema vulnerable. La interacción puede ser breve o persistente. Se incluyen ataques por USB/Direct Memory Access (DMA).

---

**Problem 114**

`CVSS:3.1/AV:A/AC:L/PR:N/UI:N/S:C/C:H/I:N/A:H`

- Attack Vector: Adjacent
- Attack Complexity: Low
- Attack Requirements: Assume None
- Privileges Required: None
- User Interaction: None
- Scope: Changed
- Confidentiality: High
- Integrity: None
- Availability: High

---

**Problem 115**

- Como la *login page* es accesible por cualquier sistema en el internet, el atacante no requiere contacto físico, adyacente o local; ergo el vector de ataque AV es "Network"
- La complejidad del ataque como tal es "Low", ya que el atacante solo necesita introducir la contraseña del usuario en la página.
- No se requieren privilegios para explotar la vulnerabilidad.
- El ataque no requiere de ninguna interacción por parte del usuario.
- El *Scope* es desconocido, aunque se sabe que la cuenta tiene permisos de administrador; por lo que las acciones estarán limitadas a lo que dicha cuenta pueda hacer.
- No se dice nada del impacto en el triángulo CIA, pero como se sabe que el usuario tiene un perfil de administrador, el impacto es "High" en todas ellas.

`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`

## 5.2 Memory Corruption

**Problem 117**

Cuando el input supera el tamaño del buffer, es cierto que no se guarda en el buffer, sino que pasa al stack. Esto significa que hay un *data overflow* que no afecta directamente al código, pero sí a la memoria; afectando a las posiciones adyacentes al buffer.

Si el atacante controla el flujo de datos del *input*, es posible que sea capaz de hacer *data overflows* hasta conseguir sobrescribir la dirección de retorno de la función (que se encuentra en el stack) con el valor que ellos elijan, ganando control sobre el puntero de instrucciones.

---

**Problem 118**

Ambas se diseñaron para incrementar la dificultad de explotar vulnerabilidades de corrupción de memoria como *buffer overflows*, *user-after-free*...

**Address Space Layout Randomization - ASLR**
Aleatoriza las direcciones de memoria de componentes clave (heap, stack...). Consigue que las direcciones de memoria sean impredecibles para el atacante.

**Data Execution Prevention - DEP**
Marca regiones de la memoria (heap, stack...) como no ejecutables mediante el bit NX/XD del hardware. Impide la ejecución directa de código inyectado en áreas de datos.

--- 

**Problem 119**

El problema se encuentra en la línea:

```c
if (length > MAX_LENGTH)
```

Al no comprobar números negativos, un *input* como -1 pasaría estas defensas. A la hora de convertirlo, esto devolvería un *unsigned integer*, un número altamente grande $M$ que al hacer la copia en el buffer, se haría una copia de $M$ bytes en el buffer, logrando un *buffer overflow*.

---

**Problem 120**

Sí, es posible que un atacante lea y coloque nuevo el contenido del *stack canary* para evitar la detección del *buffer overflow*.

Asumiendo que un programa tiene *data overflows*, es posible para el atacante ir leyendo contenidos de la memoria hasta conseguir encontrar el *stack canary*. Una vez que conoce su dirección de memoria, puede hacer *payloads* para el desbordamiento del buffer hasta la posición del programa.

---

## 5.3 Input Validation

**Problem 121**

Los ataques de inyección se basan en insertar contenido malicioso (en este caso código o scripts) para su ejecución dentro del sistema atacado y obtener información sobre él.

Los más conocidos son inyección de SQL e inyección de comandos (por ejemplo bash). Una de las técnicas más importantes que usan los programadores es:
1. Comprobar todos los inputs que obtienen
2. Formatear todos los inputs al formato que ellos consideren. De esta manera se mitiga el riesgo.

---

**Problem 123**

Un ataque Cross-Site Scripting (XSS) ocurre cuando un atacante logra inyectar scripts maliciosos (generalmente JavaScript) en una página web legítima que otros usuarios visualizan. El navegador de la víctima no tiene forma de saber que el script no es confiable y lo ejecuta, permitiendo al atacante robar cookies de sesión, tokens o redirigir al usuario.

---

**Problem 124**

El programa tiene una *format string vulnerability*. Los *formatting* se encuentran en el *stack* o en el *heap* (depende del compilador), donde se contiene la información necesaria para convertir contenido del ordenador a *human-readable information*. 

El código puede no tener acceso a una parte del *stack*, o que sencillamente dicho transformador no exista. Esto hace que el kernel envía una señal *SIGSEGV* que típicamente hace que el proceso finalice.

---

**Problem 125**

¿Qué ocurre si el parámetro `username` es controlado por el atacante? El código como está ahora permite una inserción de *queries*, lo que permite una SQL injection.

Para evitar esto, es tan fácil como añadir comprobadores del tipo de dato y formateadores del input para modificar con `trim()` o `replace(', )`, eliminando comillas o espacios que puedan permitir esta vulnerabilidad.

---

**Problem 126**

Contiene un XSS en la última línea del código, *item* puede ser modificado y actuar como una script. Se puede ejecutar una script para obtener las cookies y enviarlas a una base de datos controlada por el atacante.

## 5.4 Denial of Service

**Problem 127**

El TCP SYN es el paquete inicial que se manda para inicializar la conexión cliente-servidor a través del protocolo TCP. El servidor tiene un buffer (disco, almacenamiento...) donde almacena las paquetes que todavía no ha procesado, procesándolos a un tiempo $t_S$.

Si el cliente, en este caso un atacante, envía paquetes en cada $t_C$ segundos, donde $t_C < t_S$, el cliente es capaz de llenar el buffer del sistema del servidor, sobrecargándolo poco a poco.

Esto hace que, pasado un tiempo, el sistema se llene de peticiones, volviéndose más lento y finalmente deteniéndose por un *crash* en el sistema, muy seguramente por un OOM (Out of Memory).

---

**Problem 128**

NTP (Network Time Protocol), DNS (Domain Name System) y Memcached son servicios que permiten que una solicitud pequeña genere respuestas muy grandes hacia la víctima, amplificando el tráfico de ataque.

---

**Problem 129**

La mayoría de ataques DoS utilizan direcciones IP de origen falsificadas (spoofed) por:
- Ocultar la identidad del atacante: evita que sistemas de mitigación eliminen el ataque antes de que se ejecute
- Existen servicios reflectores que envían las respuestas a la IP falsificada (la víctima) para que se sobresature.
- Evitan mecanismos de defensa simples
- Maximizan el impacto de ataque; sin recibir respuestas de vuelta.

---

**Problem 130 - Reflective DDoS** 

*Reflective DDoS - Reflective Distributed Denial-of-service* es un ataque que sobrecarga al sistema objetivo con tráfico de internet malicioso, haciéndolo lento o que haga un *crash*, denegando a los usuarios legítimos su servicio.

1. El atacante envía muchas solicitudes pequeñas a servidores públicos usando UDP.
2. En cada solicitud, falsifica la IP de origen para que sea la de la víctima
3. Los servidores responden automáticamente a la IP (falsa) que hizo la solicitud.
4. La víctima recibe un volumen masivo de tráfico, causando la denegación de servicio.

---

**Problem 131 - Amplification DDoS**

Similar al anterior, pero con matices.

1. El atacante envía paquetes muy pequeños a servidores públicos que usan UDP.
2. Suplanta la IP de origen con la IP de la víctima.
3. Los servidores responden con paquetes grandes dirigidos a la víctima
4. La diferencia tamaño respuesta / solicitud produce amplificación
5. La víctima queda saturada por el tráfico amplificado.

## 5.5 Miscellanea

**Problem 136**

*Ping of Death (PoD)* es un ataque clásico que explota fallos en la implementación del protocolo IP/ICMP relacionados con el manejo incorrecto de los paquetes fragmentados.

El tamaño máximo de un paquete IP es de **65.535 bytes**. El atacante envía paquetes ICMP (ping) fragmentados que, al ser reensamblados superan dicho tamaño máximo. Los sistemas operativos antiguos no validan correctamente el tamaño total tras el reensamblado, lo que provoca desbordamiento de buffer o errores de memoria en el kernel.

---

**Problem 138**

Las contraseñas *hard-coded* (que no se pueden modificar fácilmente) introducen riesgos críticos de seguridad:
- Imposibilidad de rotación de credenciales: la contraseña no puede cambiarse sin recompilar o redistribuir el producto.
- Si la contraseña se descubre (ingeniería inversa, ataques, errores humanos) el sistema queda vulnerable a ataques.
- Pérdida de confidencialidad, integridad y disponibilidad; control remoto; persistencia del atacante...

Para solucionarlo:
- Eliminar la contraseña *hard-coded* del código fuente, permitiendo la rotación de claves basadas en temporalidad (cada 12 horas se cambia la contraseña).
- Obligar el cambio de credenciales tras la compilación del sistema para evitar contraseñas por defecto (ataques a Raspberries).

---

**Problem 141**

Usar el nombre del usuario como *token* es una idea cuanto menos aberrante en términos de seguridad. No solo se encuentra en formato legible, sino que cualquier filtración de una base de datos que contenga dicho nombre de usuario permite acceder a los contenidos de dicha web.

Un ejemplo mucho mejor sería generar tokens JWT de inicio de sesión con persistencia temporal (entre 1 día y 7 días) basados en un *challenge* de las contraseñas públicas-privadas del usuario. Este token por sí solo no se puede obtener en ningún sitio salvo en el navegador (cookies), lo que reduce mucho las posibilidades de ataque.