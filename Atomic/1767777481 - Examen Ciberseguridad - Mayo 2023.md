---
aliases:
  - Examen Ciberseguridad - Mayo 2023
tags:
"References":
cssclasses:
---
# Examen Ciberseguridad - Mayo 2023

**Problem 1**

Un atacante que obtiene la **clave privada de la CA ACME-CA** puede explotar esa capacidad así:

1. **Uso de la clave robada (Atacante)**  
    El atacante utiliza la **clave privada de ACME-CA** para **firmar certificados falsos** (por ejemplo, para `www.banco.com`).  
    **Objetivo:** crear certificados que los navegadores consideren **válidos y de confianza**.
    
2. **Suplantación de servicios (Atacante)**  
    Emplea esos certificados en servidores controlados por él o en ataques **Man-in-the-Middle**.  
    **Objetivo:** hacerse pasar por sitios legítimos usando HTTPS sin alertas.
    
3. **Engaño al cliente (Víctimas/Navegador)**  
    Los navegadores aceptan la cadena de confianza porque ACME-CA está en el almacén raíz.  
    **Objetivo:** establecer conexiones cifradas creyendo que el sitio es auténtico.
    
4. **Explotación de la confianza (Atacante)**  
    Intercepta o modifica comunicaciones, roba credenciales o inyecta contenido.  
    **Objetivo:** comprometer la **confidencialidad, integridad y autenticidad** de las comunicaciones.
    
5. **Persistencia del ataque (Atacante)**  
    El ataque continúa mientras la clave no sea revocada y la CA siga siendo confiable.  
    **Objetivo:** mantener el impacto a gran escala y de forma silenciosa.
    

---

**Problem 2**

- **XSS almacenado**: el código se guarda en el servidor, se ejecuta cada vez que otro usuario carga la página. Es más peligroso, ya que no quiere una interacción especial por parte de la víctima.
- **XSS reflejado**: el código no se almacena, se refleja en la respuesta HTTP. Se requiere que la víctima haga clic en un enlace manipulado.

---

**Problem 3**

El principio de mediación completa establece que todo acceso a un recurso debe ser verificado, siempre, por el mecanismo de control de acceso, sin excepciones, ni reutilización de decisiones previas.

En un servidor web, cada solicitud HTTP a un recurso protegido:
- La autenticación del usuario.
- La autorización para dicho recurso

---

**Problem 4**

No, no es una buena idea. EL IP source routing permite que el emisor del paquete decida la ruta que seguirá a través de la red, en vez de dejar la decisión a los routers.

Un atacante puede enviar paquetes con source routing forzado para que:
- Eviten firewalls o sistemas de filtrado
- Redirijan las respuestas a un host controlado por el atacante
- Faciliten ataques de suplantación de IP spoofing y Man in the Middle.

--- 

**Problem 5**

A través de *iframes*. Fuerzas al gestor de contraseñas a rellenar credenciales en formularios invisibles y luego robarlas con JavaScript.

1. La víctima visita una página suplantada o modificada por el atacante (con HTML ocultos).
2. Dentro de cada iframe hay un formulario
3. El gestor de contraseñas hace autofill si su política lo permite.
4. JavaScript lee los valores y los filtra.

Si todo HTTPS está bien configurado y no hay XSS no se puede, pero de haber XSS sí que es posible la inserción de estos *iframes* para su uso maligno.