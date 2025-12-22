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

Los tokens se transmiten a través del navegador del usuario (S) en lugar de una conexión directa entre servidores.

1. Solicitud de acceso: el navegador solicita acceso a un servicio protegido. Prepara una petición a la parte confiante para autenticarse
2. Redirección al IdP: el navegador del suscriptor sigue automáticamente la redirección hacia el IdP.
3. Autenticación del suscriptor: el IdP verifica la identidad de S. Si es existo, se devuelve una aserción firmada digitalmente que contiene los atributos permitidos.
4. Entrega aserción
5. Validación aserción
6. Acceso concedido

---

**Problem 32**.

Los tokens se transmiten directamente de servidor a servidor. Ofrece mayor seguridad.

1. Solicitud de acceso
2. Autenticación y generación del Artefacto
3. Presentación del Artefacto
4. Intercambio en el Canal Trasero
5. Entrega de la aserción
6. Confirmación y acceso

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