---
aliases:
  - Introducción a la Ciberseguridad - Ejercicios
tags:
"References":
cssclasses:
---
# Introducción a la Ciberseguridad - Ejercicios

**Problem 9**. Discuss similarities and differences between the concepts of *defense in depth* and *zero trust*.

*Defense in depth* usa una estrategia de seguridad a través de capas (técnicas, administrativas, físicas...) para proteger los datos. Si una capa falla, existen otras para cubrirla.

Por otro lado, *zero trust* asume que todo dispositivo/usuario debe verificarse al momento de entrar al sistema y mientras esté en él para reducir accesos inesperados.

---

**Problem 15**.

Por defecto, el usuario nunca debe de poder estar verificado. Al ejecutar el código de esa manera, existe la posibilidad de modificar el valor de la variable y entonces permitir accesos inesperados a la aplicación.

---

**Problem 16**.

Al hacer *access()*, es posible que se nos pida una contraseña. Sin embargo, con el resto de llamadas al sistema esto no ocurrirá: es una decisión de diseño de los sistemas UNIX que rompe con el principio de **autenticación** en el acceso a los datos.

