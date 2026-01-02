---
aliases:
  - Network Security - Ejercicios
tags:
References:
cssclasses:
---
# Network Security - Ejercicios

## 4.1 Network Threats

**Problem 82 (Threats to network communications) Write down a table with four
rows, one for each category of threat actions to network communications (intercep-
tion, modification, fabrication, and interruption). Provide for each threat category
the security property that is affected (confidentiality, integrity, availability, etc.) and
one countermeasure that can be applied to network communications to mitigate the
threat**

- Interceptación: un ataque de este tipo consiste en el que un mensaje de $A$ a $B$ es accedido por $C$.  Afecta a la **confidencialidad**. **Contramedidas**: cifrado del mensaje; autenticación en la comunicación (canal confidencial y autenticado).
- Modificación: el emisor $A$ manda un mensaje $M$ al receptor $B$, pero el atacante $C$ es capaz de modificarlo a $M'$. Afecta a la **integridad**. **Contramedidas**: uso de MAC y de la [[1731333961 - Firma Digital|Firma Digital]].
- Fabricación: un adversario $C$ envía un mensaje $M$ al receptor $B$ haciéndose pasar por $A$. Afecta a la **autenticación**. **Contramedidas**: añades mecanismo robusto de autenticación (MAC o firmas).
- Interrupción: se detiene el servicio de las comunicaciones. Afecta a la **disponibilidad**. **Contramedidas**: filtrado de tráfico. 

---

**Problem 84**

El ataque de secuestro de sesión TCP por desincronización durante el establecimiento aprovecha la predicción de números de secuencia para que el atacante se haga pasar por el cliente antes de que la conexión TCP quede correctamente sincronizada.

Se requieren de tres actores:
- Cliente legítimo
- Servidor
- Atacante: no necesita ver el tráfico (interceptar la comunicación); solo necesita predecir el ISN.

Se basa en:
1. El atacante inicia un intento de conexión TCP simulando ser el cliente
2. El servidor responde con un SYN-ACK dirigido al cliente real.
3. El atacante adivina el número de secuencia del servidor y envía un ACK falso.
4. El cliente nunca confirmó realmente dicha conexión, pero el atacante ya está conectado.

---

**Problem 86**

- Capa de red: IPsec. Transparencia para las aplicaciones, protección generalizada y una autenticación a nivel de host/red.
- Capa de transporte: TLS. Seguridad extremo a extremo: protege los datos desde el proceso cliente hasta el proceso servidor; autenticación flexible con certificados, claves públicas...
- Capa de aplicación: HTTPS, ssh. Control semántico con seguridad de extremo a extremo.

## 4.2 Network Scanning

**Problem 87**

1. Descubrir activos y servicios desconocidos
2. Detecta vulnerabilidades y malas configuraciones
3. Verifica controles de seguridad: confirma que firewalls funcionan como se espera.

---

**Problem 88**

El IP ID del zombie actúa como un contador global para inferir si el zombie fue inducido a enviar un paquete adicional. 

Al haber incrementos adicional en +2, se puede asumir que dicho puerto está abierto. Si el puerto está cerrado, el zombie no respondería y no habría incremento.

## 4.3 Firewall

**Problem 94**

Los firewalls de filtrado sin estado y de inspección con estado difieren en qué información consideran al tomar decisiones y en qué tan precisas son esas decisiones:
- **Stateless packet filtering**: examina cada paquete de manera independiente. Decide permitir o bloquear basándose en:
	- IP origen/destino
	- Puerto origen/destino
	- Protocolo
	- Flags simples
- **Stateful inspection firewall**: mantiene una tabla de estado de las conexiones activas; comprueba los paquetes que:
	- Pertenecen a una conexión establecida
	- Siguen el flujo correcto del protocolo

Mientras que los stateful requieren de mayor consumo de recursos, se obtiene una mayor seguridad y precisión; reduciendo los posibles ataques de spoofing.

## 4.4 Transport Layer Security

**Problem 102**

1. El navegador se conecta al servidor y recibe su certificado digital
2. El navegador verifica la validez básica del certificado:
	- No está experado
	- Dominio del certificado coincida con el dominio visitado
	- No está revocado
3. El navegador comprueba la cadena de confianza
4. La CA raíz debe de estar en el almacén de confianza del navegador/SO
5. Si toda la cadena es válida, el navegador confía en el servidor

---

**Problem 103**

1. Se crea un certificado firmado por la CA, pero a una entidad falsa/maliciosa (por ejemplo `*google`). Se te da una clave pública, y el certificado se firma por la CA (recordemos que solo necesidad la clave privada de la CA para hacer esto). Luego, podemos hacer un servidor *on-path*: el servidor que enruta a un dominio determinado enrute a tu dominio, no al otro (envenenamiento de DNS). Cuando se inicia el TLS. nuestro ataque enviará el certificado malicioso a la máquina.
2. No se puede. Los CRLs revocan, pero el daño ya está hecho. El OCSP actúa de similar manera, pero obtenemos el mismo error: el daño ya está hecho.

---

**Problem 104**

Usa ambas.
- Criptografía asimétrica: se utiliza durante el handshake inicial; autenticando al servidor y se establece un secreto compartido.
- Criptografía simétrica: se utiliza una vez finalizado el handshake. El secreto compartido se deriva a claves simétricas con los que se cifran y autentican todos los datos de la sesión.

---

**Problem 105**

Puede proporcionar *forward secrecy*; pero depende del método de intercambio de claves usado.

Si se usa intercambios de claves efímeros como [[1730132101 - Diffie Hellman Efímero - DHE|Diffie Hellman Efímero - DHE]] o basado en curvas elípticas. Cada sesión genera claves temporales nuevas, por lo que no se depende de la clave privada del servidor a largo plazo.

Por otro lado, con *RSA key exchange* esto no ocurre: se necesita cifrar la premaster secret con la clave pública del servidor, pudiendo descifrar sesiones grabadas.

En [[1730133054 - Protocolo TLS|Protocolo TLS]] 1.3 es obligatorio el forward secrecy.

---

**Problem 106**

La principal diferencia entre DoH (DNS-over-HTTPS) y DoT (DNS-over-TLS) es cómo de visible es el tráfico de DNS y ver quién puede controlarlo o bloquearlo.

**DNS-over-TLS (DoT)**
Encripta las *queries* de DNS en un puerto dedicado (853, previniendo que los observadores lean o modifiquen el tráfico DNS. El destino es todavía visible, pero su contenido está oculto.

**DNS-over-HTTPS (DoH)**
Envía las *queries* de DNS en un puerto dedicado (443). El tráfico es totalmente indistinguible del tráfico normal de web a los observadores. 

Ambos, DoT y DoH protegen la confidencialidad usando TLS. DoT es más transparente y fácil de manejar a nivel de red, pero más fácil de bloquear; mientras que DoH ofrece mayor privacidad con el coste de reducir control en la red y poder de centralización.

---

**Problem 108**

1. Sí, TLS lo impide, ya que es una comunicación *end-to-end* entre ambas partes.
2. Un ataque XSS se basa en la inserción de código malicioso o *scripts* en una web o servidor. TLS no controla esto, ya que puede insertarse código a través de una comunicación segura.
3. Sí, TLS lo impide, ya que hacer un *Man-in-the-Middle* con TLS es mucho más complicado.
4. Un *SQL injection* no es controlado por TLS (mismos motivos que en el punto 2).
5. Tampoco lo puede evitar.
6. De nuevo, es un *Man-in-the-Middle*. Aunque posible, requiere de muchos más factores que lo hacen muchísimo más complicado (ergo TLS lo impide).

---

**Problem 109**

*Certificate pinning* es una técnica de seguridad usada para proteger comunicaciones cliente-servidor restringiendo qué certificados digitales o claves públicas son válidos en un dominio determinado.

1. Selección: durante su desarrollo, el certificado del servidor, una clave pública o un hash se inscribe en la aplicación del cliente.
2. Verificación de handshake: cuando la aplicación hace una conexión, el servidor presenta su certificado.
3. Comparación: se compara el que se tiene actualmente con el que recibe de nuevo por parte del servidor
4. Si son iguales, la conexión continúa.

Esto previene *man-in-the-middle* a través de certificados falsos.

El principal problema es que no tiene un mecanismo para responder de manera rápida con problemas de certificación. 