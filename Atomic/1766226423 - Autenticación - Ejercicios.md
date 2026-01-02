---
aliases:
  - Autenticación - Ejercicios
tags:
"References":
cssclasses:
---
# Autenticación - Ejercicios

## 2.1 Authentication Methods

**Problem 29**.

Importante destacar que hay tres categorías de factores de autenticación
- Algo que conoces: contraseñas, PINs, respuestas a preguntas.
- Algo que tienes: un USB con una .pem dentro.
- Algo que eres: técnicas basadas en la biología, huellas, retina...

---

**Problem 30**.

Ataque que generaba un riesgo en el factor de autenticación de dos pasos. A efectos prácticos, se basa del robo de tu número de teléfono.

El atacante conseguía engañar al operador de tu línea telefónica para conseguir que le manden una nueva SIM a su dirección, mientras que la que tú usas se desactiva. De esta manera, muchos SMS de autenticación le llegan a él, siendo capaz de acceder a tus datos.

--- 

**Problem 31**.

Los tokens se transmiten a través del navegador del usuario (S) en lugar de una conexión directa entre servidores. Protocolo de 2 pasos.

1. IdP -> S: assertion
	1. S recibe la assertion desde el IdP por el canal front-end. Este canal es visible para S.
2.  S -> RP: assertion
	1. S usa la assertion para autenticarse al RP enviándolo por el canal front-end.

---

**Problem 32**.

Los tokens se transmiten directamente de servidor a servidor. Ofrece mayor seguridad. Se basa en un protocolo de 4 pasos.

1. IdP -> S: aref
	1. S recibe una referencia a la assertion *aref* desde IdP desde el canal front-end. No contiene ninguna información que pueda relacionarse con S. Es resistente a una fabricación sintética por el atacante
2. S -> RP: aref
	1. S envía la referencia a la assertion *aref* a RP a través del canal del front-end.
3. RP -> IdP: aref, rpcred
	1. RP envía la referencia *aref* y sus credenciales *rpcred* a IdP. Esta comunicación ocurre a través del back-end.
4. IdP -> RP: assertion
	1. IdP valida la *assertion* y las credenciales del RP, devolviéndoselas a RP por el canal back-end.

---

**Problem 33**.

Evidentemente, depende del caso. Sin embargo, se considera una buena práctica, ya que se pueden evitar otros ataques no deseados. Aunque no nos importe el acceso a los datos, un exceso de peticiones de acceso puede tirar un servidor.

Autenticando si dicho usuario puede acceder a la web o no se puede eliminar ciertos factores de riesgo que podrían afectar a nuestro sistema.

---

**Problem 34**.

Evidentemente, no hay sistemas perfectos. Como hemos visto antes, existe el SMS swapping, lo que cual es una vulnerabilidad enorme en este sistema, aunque requiere la interacción del atacante con otras personas.

Se puede añadir un grado extra de seguridad: que el 2FA sea solo a través de la propia aplicación del programa (como hace Github, por ejemplo). De esta manera, si el atacante no tiene tus credenciales es casi virtualmente imposible que sea capaz de acceder.

---

**Problem 35**.

- One Time Password - OTP: se generan códigos temporales, usualmente de seis dígitos, basados en un secreto compartido, el tiempo y otros factores. Llaveros RSA.
	- *Seguridad del canal*: el usuario debe copiar el código al canal primario, lo cual hace sujeto a phishing.
	- *Dependencia conectividad*: ninguna, los tokens en hardware funcionan sin cobertura
	- *Vulnerabilidad*: pérdida física del token o desincronización del reloj interno
- Out of Band - OOB: utilizan un canal de comunicación separado e independiente del canal primario. Notificaciones push en una app móvil, SMS...
	- *Seguridad del canal*: alta, ya que es independiente del medio primario
	- *Dependencia conectividad*: alta, sin cobertura o red es imposible que lleguen dichas notificaciones.
	- *Vulnerabilidad*: SIM swapping

## 2.2 Password Security

**Problem 38**.

1. No me importa
2. No se, me da bastante igual calcular esto
3. Se puede hacer un simple código en un lenguaje de generación genérico en el que intente todas las contraseñas posibles para todos los dígitos posibles (asume que el rango es $[0, 9]$). Sabiendo que tenemos un total de cuatro dígitos, se deben primero de precomputar (o no, es una opción) todas las combinaciones posibles; para luego ir manualmente una por una insertando y probando.

---

**Problem 40**.

El *salt* es un campo generador aleatorio durante la creación de la contraseña antes de pasarla por una función hash. Su principal propósito no es ocultar la contraseña, sino individualizar el resultado del hash.

De esta manera, no solo se debe de tener la contraseña y el algoritmo del hash para conseguir el resultado final, sino que también hay que encontrar un parámetro generado previamente aleatoriamente (está guardado en algún sitio).

Somos capaces de evitar las *rainbow tables* y los diccionarios de contraseñas, evitando que si una contraseña ha sido descubierta y hasheada el atacante pueda acceder sin problema.

---

**Problem 41**.

- Fuerza bruta
- Phishing moderno: a través de mensajes o páginas de login falsas
- Data leakage de bases de datos que contengan dichas contraseñas.

---

**Problem 42**.

1. El bloqueo de cuentas produce una vulnerabilidad inherente en el servicio:
	1. Ataques de denegación de servicio (DoS)
	2. Errores humanos
	3. Automatización maliciosa
2. No, no lo es. Por defecto, el principio *Fail-safe Defaults* establece que, en caso de fallo o error el sistema debe pasar a un estado que mantenga la seguridad sin comprometer la disponibilidad de manera innecesaria. En este caso, no se devuelve a un estado por defecto, sino que es la respuesta activa a un evento sospechoso.
3. Sí, viola el principio de disponibilidad.

---

**Problem 43**.

Pueden usar un **origin-spoofing** basado en iframes invisibles. El gestor de contraseñas realiza un auto-fill a cualquier cosa que corresponda con un tag determinada dentro de un dominio determinado.

Si el atacante es capaz de replicar este estructura, el gestor de contraseñas verá dicho iframe y lo rellenará pensando que es el formulario correcto. El contenido de este iframe luego puede enviarse a una base de datos para cualquier tipo de uso. 

---

**Problem 44**.

Inicialmente, se puede pensar que sí es seguro. Sin embargo, si se tiene en cuenta el tamaño de la seed $2^{16}$, esta no es demasiado grande. Para cada seed, se puede precomputar el número total de combinaciones posibles ($62^{10}$) y usar una tabla arcoiris con el contenido total de manera secuencial para intentar conseguir dicha contraseña.

---

**Problem 45**.

1. La seguridad se ve en peligro si una de esas webs se ve atacada y sus datos robados. Los datos de los usuarios y las contraseñas (aunque no la web) son obtenidas por el atacante y es posible su uso de manera maliciosa.
2. Pueden ocurrir mismos *hashes* para distintas contraseñas, lo que reduce el espacio de ataque y búsqueda de contraseñas; ya que se ha eliminado el *salt* de la ecuación. Todo esto debilita el proceso seguro de contraseñas.

---

## 2.3 Cryptographic Authentication Protocols

**Problem 47**.

Antes de todo, debemos de entender qué es un **challenge response protocol**. El servidor distribuido manda un pequeño **challenge** que solo se puede solucionar (autenticar) con un secreto compartido (contraseña del usuario). Solo si se soluciona correctamente se proporciona acceso al usuario a los recursos protegidos.

---

**Problem 48**.

Existen dos procesos:
1. Registro del usuario
	1. El usuario genera una clave pública y privida
	2. El usuario envía la clave pública al servidor
	3. El servidor la guarda con otros datos: usuario, contraseña...
2. Autenticación
	1. El usuario reconoce su identidad
	2. El servidor envía un challenge nuevo para que lo resuelva
	3. El usuario lo firma (resuelve) con su clave privada
	4. El servidor verifica la firma con la clave pública.
	5. Si es válido, el usuario es autenticado.

**La clave privada NUNCA se envía por la red**

---

**Problem 52**.

Kerberos usa dos tickets para separar la autenticación del acceso al servicio, limitando un posible ataque.

1. Ticket-Granting Ticket: autentica una sola vez. Evita que se vuelvan a entrar las mismas contraseñas y previene la exposición de credenciales de larga duración.
2. Service Ticket: acceso a un servicio específico. Se devuelve encriptada la clave secreta del servicio, de corta duración.

---

**Problem 53**.

1. El atacante no puede recrear la identidad de Alicia porque el servidor de autenticación cifra la clave de sesión usando la clave privada de Alicia, derivada de su contraseña. Sin saber la contraseña, el atacante no puede generar una petición válida al TGS.
2. El atacante necesita la contraseña para descifrar el token de sesión, cosa que no puede hacer sin la contraseña de Alicia.