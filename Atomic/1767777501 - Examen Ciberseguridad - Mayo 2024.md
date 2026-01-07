---
aliases:
  - Examen Ciberseguridad - Mayo 2024
tags:
"References":
cssclasses:
---
# Examen Ciberseguridad - Mayo 2024

**Problem 1**

El principio de *fail-safe defaults* establece que, ante un fallo o ausencia de decisión explícita, el sistema debe denegar el acceso por defecto, no permitirlo.

El ejemplo más claro es un firewall, donde debe de denegar todos los accesos por defecto a no ser que esté explícitamente autorizado.

---

**Problem 2**

1. El pinning de certificados consiste en que el cliente almacena o conoce de antemano un certificado, clave pública o hash esperado de un servidor. Es algo parecido a comparar las hashes de ciertos archivos al descargarlo.
2. Previene ataques como Man-in-the-Middle, certificados fraudulentos o suplantación del servidor incluso cuando el certificado es válido.
3. Existen varios problemas:
	1. De disponibilidad: si el certificado cambia y el pin no se actualiza, el servicio queda inaccesible.
	2. Difícil gestión: rotación de claves y certificado más compleja
	3. Costoso y frágil de mantener

---

**Problem 5**

1. Si los usuarios de dichos sistemas no la cambian, y están conectados a la red (también es posible hacerlo físicamente), es posible acceder al root de la máquina con la complejidad de un ataque, a efectos prácticos, casi nulo, ya que solo hace falta inyectar dicho usuario y contraseña.
2. Si la contraseña/usuario no se ha cambiado, se puede acceder al sistema admin y cambiarlo manualmente con una contraseña que no sea la anterior. De no saber la nueva contraseña, la única solución rápida y efectiva es resetear el sistema.
3. A la hora de inicializar por primera vez el dispositivo, que se requiera la creación de un usuario y contraseña nuevos para el nuevo usuario.

---

**Problem 4**

TCP SYN y TCP normal.

---

**Problem 5**

Añadir aleatoriedad a los hashes.