---
aliases:
  - Examen Ciberseguridad - Junio 2022
tags:
"References":
cssclasses:
---
# Examen Ciberseguridad - Junio 2022

**Problem 1**

El principio de *fail-safe default* se basa en no permitir el acceso al sistema o a cualidades del sistema por defecto. Esto permite que, en caso de una modificación de una variable de manera inesperada, como puede ser una excepción, un error en ejecución, un valor nulo o incluso un valor no esperado como resultado, no se permita el acceso al sistema.

De esta manera, es posible inhabilitar una posible caída al sistema por valores no esperados o por un atacante.

```python
a = is_access_allowed(user, resource);
if (a == ACCESS_ALLOWED) {
	// acceso permitido
} else {
	// por defecto, acceso denegado
}
```

---

**Problem 2**

- **ruid**: es el UID del usuario que a iniciado el proceso. Permite identificar y conocer qué usuario del sistema a lanzado el proceso en todo momento
- **euid**: es el UID que el *kernel* utiliza para comprobar permisos. Permite saber qué puede hacer realmente el proceso.
- **suid**: es una copia del *euid* que mantiene el *kernel* en todo momento. Lo usa para poder bajar permisos temporalmente si es necesario sin necesidad de ejecutar de nuevo el binario.

---

**Problem 3**

Ante todo, es importante definir que es cada cosa:
- One Time Passwords (OTP): dispositivo físico o app que genera contraseñas de un solo uso, válidas por poco tiempo o por un evento (tokens, 2FA)
- Look-up secrets: lista finita de códigos estáticos generados previamente y guardados por el usuario en el sistema

**OTP - Fortalezas y Debilidades**
Por un lado, los códigos son dinámicos y de corta vida, dificultado su reutilización como contraseñas. Sin embargo, existe una alta dependencia con el dispositivo, vulnerables al phishing en la vida real.

**Look-up secrets - Fortalezas y Debilidades**
Son simples y robustos, funcionando sin dispositivos e ideales como mecanismo de recuperación. Sin embargo, son estáticos (lo que supone un objetivo atractivo) y generan poca resistencia contra el malware (una vez obtenidos, obtenidos están).

---

**Problem 4**

1. El cliente hace `ClientHello`, iniciando la comunicación con el servidor TLS. Configura clientRandom y clientKeyRandom.
2. El servidor recoge la petición y hace `ServerHello`. Configura serverRandom y serverKeyRandom.
3. Se comparte la `PreSharedKey` configurada a partir del serverRandom y el serverKeyRandom.
4. El servidor pasa información de posible relevancia al cliente TLS: `Encrypted Extensions`, `Certificate` y `CertificateVerify`. 
5. El cliente TLS verifica con la clave pública el certificado y la prueba de firma. Finalmente acaba el intercambio de credenciales.
6. Comienza la comunicación cifrada.

---

**Problem 5**

- TCP SYN Scan: no se realiza la comunicación completa, sino que se envía el paquete SYN que busca inicializar la comunicación con el servidor. Si se recibe una respuesta SYN-ACK, el puerto de dicha máquina está abierto. Si se recibe un RST, el puerto está cerrado. Es muy rápido para escanear dispositivos y es menos detectable, pero requiere de privilegios.
- TCP Connect Scan: intenta completar la conexión de manera exitosa. Si lo hace, el puerto está abierto. Requiere menos privilegios, pero es más lento y más detectable (queda en los logs).

---

**Problem 6**

La vulnerabilidad $a$ debe ser priorizada por dos motivos esenciales:
- El vector de ataque se basa en la Red (Network), lo que hace que tenga un alcance potencialmente global. 
- Es cierto que la complejidad del ataque es alta, pero golpea el triangulo CIA en todo: confidencialidad, integridad y disponibilidad de manera total, generando un fallo máximo en el sistema.

