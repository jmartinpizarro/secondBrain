---
aliases:
  - Repaso Ciberseguridad 2
tags:
"References":
cssclasses:
---
# Repaso Ciberseguridad 2

**Problema 1. (2 puntos)**

**Describa el principio de seguridad conocido como mediación completa (complete mediation). Explique en qué consiste y proporcione un ejemplo realista que ilustre su aplicación en un sistema actual.**

El principio de mediación completa se refiere a que todo acceso a recurso debe de ser mediado, controlado y verificado por el componente de acceso de control, sin tener en cuenta información previa de la petición de acceso. 

Un ejemplo realista es el acceso a una web HTTP:
- Se realiza una petición HTTPS para el acceso al *web server*.
- Se realiza una autenticación por parte del usuario con un token.

---

**Problema 2. (2 puntos)**

**Suponga que un atacante ha obtenido acceso a la clave privada utilizada por una Autoridad de Certificación (CA) para firmar certificados. Describa paso a paso cómo podría explotar esta situación, indicando qué se consigue en cada fase del ataque.**

1. El atacante es capaz, por ejemplo, de firmas certificados de manera maliciosa. De esta manera, firma un certificado falso, suplantando la identidad de una entidad normal. El certificado, que difiere ligeramente del original, está firmado por la CA y por tanto no parece ser malicioso.
2. El cliente accede a una URL con con inyección XSS. Automáticamente, se le redirige a la página maliciosa del atacante. El certificado, firmado por la CA auténtica, es confiado por el cliente.
3. El cliente introduce datos importantes, que son enviados a la base de datos del atacante para su posterior uso.

---

**Problema 3. (1,5 puntos)**

**Explique el propósito de los identificadores de usuario real (RUID), efectivo (EUID) y guardado (SUID) en procesos Linux. Indique para qué sirve cada uno y por qué son necesarios desde el punto de vista de la seguridad.**

- **RUID**: identificador real del proceso, que permite identificar qué usuaria lo ha lanzado.
- **EUID**: identificador que usa el *kernel* para identificar el proceso y otorgarlo los permisos necesarios para su ejecución.
- **SUID**: identificado que replica el EUID, pero guardado por el *kernel* para subir/bajar permisos temporalmente para el proceso sin necesidad de volver a ejecutar el programa.

---

**Problema 4. (1,5 puntos)**

**Describa cómo funciona un ataque de denegación de servicio basado en TCP SYN flooding. Explique por qué este ataque puede llegar a colapsar los recursos de la víctima.**

Un servidor tiene un buffer donde las peticiones se van almacenando y procesando, actúa como una cola. Esa cola se va llenando y vaciando dependiendo de la demanda. Al enviar paquetes SYN, el servidor comienza a procesar las solicitudes. Sin embargo, si el factor de envío es mayor que la capacidad de procesado, la cola se comienza a llenar.

El sistema comienza a reducir su estabilidad y rendimiento hasta que finalmente puede llegar a fallar. Si la cola se llena, definitivamente fallará.

---

**Problema 5. (1,5 puntos)**

**Explique en qué consisten las capabilities en Linux. Indique qué ataques ayudan a prevenir y qué principio fundamental de seguridad subyace a su diseño.**

Las *capabilities* buscan dividir los privilegios del usuario *root* en permisos finos, independientes y atómicos, de manera que cada proceso solamente requiera de un mínimo de permisos necesarios para realizar su tarea.

Siguen el principio de mínimo privilegio, en el cual solo se requiere de lo mínimo para realizar dicha acción.

---

**Problema 6. (1,5 puntos)**

**Describa dos técnicas diferentes de descubrimiento de hosts en una red. Explique brevemente el funcionamiento de cada una y sus limitaciones.**

**ICMP Echo Request (ping):**  
Se envían paquetes ICMP Echo Request a una dirección IP. Si el host responde con un Echo Reply, se considera activo. Su principal limitación es que muchos sistemas y cortafuegos bloquean ICMP, lo que puede producir falsos negativos.

**ARP scan:**  
En redes locales, se envían peticiones ARP preguntando por la dirección MAC asociada a una IP. Si se recibe respuesta, el host está activo. Es muy fiable en redes locales, pero no funciona fuera del dominio de broadcast.

---

**Problema 7. (1,5 puntos)**

**Considere las siguientes dos vulnerabilidades representadas por sus vectores CVSS:**

**a) CVSS:3.0/AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H**  
**b) CVSS:3.0/AV:A/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N**

**Discuta cuál de las dos considera más prioritaria desde el punto de vista del riesgo y justifique su respuesta.**

---

**Problema 8. (2 puntos)**

**Explique el funcionamiento de un sistema de identidad federada basado en autenticación mediante canal trasero (back-channel). Identifique las entidades participantes y describa los mensajes intercambiados.**

---

**Problema 9. (1,5 puntos)**

**Explique cómo funciona un ataque contra gestores de contraseñas basado en el mecanismo de autocompletado (autofill). Indique si este ataque es posible cuando la página web utiliza HTTPS y justifique su respuesta.**

---

**Problema 10. (1,5 puntos)**

**Explique las similitudes y diferencias entre los ataques de inyección de comandos (command injection) y los ataques de inyección SQL (SQL injection). Indique qué tienen en común y en qué se diferencian.**

