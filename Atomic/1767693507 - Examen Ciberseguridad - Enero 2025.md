---
aliases:
  - Examen Ciberseguridad - Enero 2025
tags:
"References":
cssclasses:
---
# Examen Ciberseguridad - Enero 2025

**Problem 1**

Un ataque Cross-Site Scripting (XSS) se basa en la inyección de código malicioso en ciertas URLs de algunos servidores para que se ejecuten en víctimas. Usualmente, se busca recoger contenidos del *localStorage* o de las *cookies* del navegador, donde se guardan los datos de acceso como los tokens del usuario.

Supongamos, por ejemplo el siguiente caso:

1. Se tiene la url `https://www.example.com/buscar?q=NOMBRE_DEL_USUARIO`
2. Esta url permite la inserción de contenido malicioso tal que: `https://www.example.com/buscar?q=<script>alert(cookies.access())</script>`
3. Se ha recogido e imprimido como alerta las cookies del usuario

---

**Problem 2**

| Sujeto \ Objeto | accounts  | cv.txt    | exam      | solutions |
| --------------- | --------- | --------- | --------- | --------- |
| **alice**       | **R W A** | **R W A** | **R W A** | **R W A** |
| **bob**         | **R W A** | **R W A** | **R W A** | **R W A** |
| **charlie**     | **R W A** | **R W A** | **R W A** | **R W A** |

---

**Problem 3**

Nos encontramos ante un caso de inyección SQL, algo que claramente es nocivo para la seguridad de la base de datos. Si una variable tiene contenidos que puedan ser ejecutados como comandos en la base de datos y está formateado como tal, es posible su ejecución dentro del sistema.

Si **username** tiene el valor alice' OR '1'='1, hemos terminado la string de manera artificial y somos capaces de modificar la script.

---

**Problem 4**

- El cliente recibe el **certificado del servidor** durante el TLS handshake.  
    Esto es necesario para conocer la **clave pública del servidor** y poder autenticarlo.
    
- El cliente verifica la **firma digital del certificado** usando la clave pública de la CA emisora.  
    Esto garantiza que el certificado **no ha sido falsificado**.
    
- El cliente valida la **cadena de certificación**, comprobando que el certificado del servidor enlaza con una **CA raíz de confianza**.  
    Esto evita confiar en certificados emitidos por entidades no confiables.
    
- El cliente comprueba la **validez temporal** del certificado (`Not Before` y `Not After`).  
    Esto evita el uso de certificados **caducados o aún no válidos**.
    
- El cliente verifica que el **nombre del servidor** (hostname) coincide con el indicado en el certificado (CN o SAN).  
    Esto previene ataques **Man-in-the-Middle**.
    
- El cliente comprueba si el certificado ha sido **revocado** (mediante CRL u OCSP).  
    Esto permite rechazar certificados comprometidos antes de su expiración.
    
- El cliente verifica que el certificado permite su uso para **autenticación de servidor TLS** (Key Usage / Extended Key Usage).  
    Esto impide utilizar certificados para fines no autorizados.
    
- Si todas las comprobaciones son correctas, el cliente **confía en el certificado**, continúa el handshake y se establecen las **claves simétricas** para cifrar la comunicación.

---

**Problem 5**

El **principio de Separación de Privilegios** establece que un sistema no debe otorgar todos los privilegios a un único componente, sino repartirlos entre varios, de modo que para realizar una acción sensible sean necesarios **múltiples permisos o roles**.  Esto reduce el impacto de fallos o compromisos de seguridad.  
**Ejemplo:** en sistemas Linux, un servidor web (como _Apache_ o _Nginx_) se ejecuta como usuario no privilegiado, mientras que solo procesos separados y controlados pueden realizar acciones con privilegios elevados (como abrir puertos privilegiados o acceder a archivos críticos).

---

**Problem 6**

**1. Idea que persigue este funcionamiento del bot**

El bot **verifica la firma digital** de cada comando recibido usando una **clave pública embebida**, asegurándose de que **solo el operador legítimo**, poseedor de la clave privada correspondiente, pueda enviar órdenes válidas.  
Esto garantiza **autenticidad e integridad** de los comandos y evita que terceros envíen instrucciones maliciosas al bot.

**2. Dificultades para los defensores**

- Los defensores **no pueden emitir comandos válidos** sin la clave privada del atacante.
    
- Aunque se secuestre o simule el canal C2, los bots **rechazarán órdenes no firmadas**.
    
- Obliga a **comprometer la clave privada** o modificar el binario del bot, lo que aumenta el coste y la complejidad del _takedown_.