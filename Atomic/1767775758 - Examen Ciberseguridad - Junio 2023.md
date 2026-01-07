---
aliases:
  - Examen Ciberseguridad - Junio 2023
tags:
"References":
cssclasses:
---
# Examen Ciberseguridad - Junio 2023

**Problem 1**

Después del primer comando (el umask), se obtiene unos permisos por defecto de `640`. 

1. Sí, puede. Para el usuario (propietario), los permisos son `rw-`, es decir, leer y modificar. 
2. La máscara final es `r-x`.
3. Sí, si que puede. El comando anterior solo quita permisos de escritura, no de ejecución al grupo, no al usuario.
4. No, no puede editar. *d64* tiene `rw-`, pero con la última máscara activa la intersección solo `r--`.

---

**Problem 2**

- **ruid**: es el UID real del proceso en ejecución. Permite saber a qué usuario pertenece dicho proceso.
- **euid**: es el UID que usa el *kernel* para identificar al proceso que se ha lanzado. Permite saber los permisos que va a necesitar el proceso para su ejecución.
- **suid**: es el *euid*, pero guardado temporalmente para que el *kernel* pueda subir/bajar los privilegios del programa sin volver a compilarlo/ejecutarlo.

---

**Problem 3**

Mientras que el TCP SYN es mucho más rápido, en los *logs* se puede ver de manera mucho más clara si están haciendo un escaneo a la red. Es decir, es mucho más evidente.

Si un atacante busca ser sigiloso en la red, usar TCP es mucho mejor, ya que realmente estás completando todo el protocolo TCP, haciéndolo más lento; pero pudiendo hacerte pasar por un paquete normal y corriente en vez de un escaneo más directo.

---

**Problem 4**

Es importante destacar primero el funcionamiento de UDP: es un protocolo que no requiere de un *handshake*.

Sabiendo esto, el paquete UDP se envía a un puerto alto (como 63645 por ejemplo) y normalmente cerrado por el host objetivo. Si el host está activo, al recibir un paquete enviará un mensaje ICMP *Port Unreachable*.

Esta respuesta confirma que el host existe y está accesible. Sin embargo, si no hay respuesta puede significar que:
- El host no está activo.
- Existe un firewall.
- El paquete se perdió.

---

**Problem 5**

Un sistema de identidad federado de *back-channel* funciona así:
1. S -> RP:
	1. Mensaje: solicitud de acceso a un recurso
	2. Acción RP: detecta que S no está autenticado y decide usar un IdP
2. RP -> S:
	1. Mensaje: redirección del IdP (con identificador de sesión/petición)
	2. Acción S: accede al IdP
3. S -> IdP:
	1. Mensaje: credenciales de autenticación
	2. Acción IdP: autentica al usuario S
4. IdP -> RP:
	1. Mensaje: aserción/token de seguridad (firmado)
	2. Acción RP: valida firma, integridad y vigencia del token
5. RP -> S:
	1. Mensaje: concesión de acceso al recurso
	2. Acción final: S accede como usuario autenticado

---

**Problem 6**

Attack Vector: Network. el vector de ataque es la propia red, lo que supone el valor máximo alcanzable.
Attack Complexity: Low. El ataque no es complicado como ataque, por lo que es fácil de diseñar y atacar.
Privileges Required: None. No requiere de modo root o administrador para realizar dicho ataque.
User Interaction: Required. Requiere una comunicación e interacción con el usuario para poder acceder a su objetivo.
Confidentiality, Integrity, Availability: High, High, None respectivamente

---

**Problem 7**

1. El atacante puede hacer que la autoridad de certificación emita certificados emitidos por ella suplantando entidades falsas o no. De tener un certificado emitido por dicha entidad, el atacante puede realizar otro tipos de ataques, como por ejemplo simular páginas webs o redirigir a otros sitios usando XSS para que las víctimas acudan a su sistema. El sistema, que ha ojos del navegador/kernel está firmado por una entidad confiable, no dice nada. Desde ahí, los atacantes pueden hacerse pasar por cualquier tipo de entidad para poder lograr su objetivo.
2. No, no pueden proteger frente a este ataque. CRL y OCSP solo informas de revocaciones, no detectan certificados maliciosos correctamente firmados. La única posibilidad es retirar la CA raíz del almacén de confianza o certificate transparency, pinning.