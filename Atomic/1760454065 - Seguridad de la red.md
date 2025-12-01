---
aliases:
  - Seguridad de la red
tags:
  - protocolosRed
References:
cssclasses:
---
# Seguridad de la red

## Fundamentos de seguridad de la red

Posibles problemas (MIGI):
- **Modificación**
- **Interceptación**
- **Generación**
- **Interrupción**

Casi todas las comunicaciones se basan en [[1728882855 - TCP]]. Sin embargo, la seguridad de este protocolo es casi nula:
- Algunos errores se pueden resolver
- Otros no

Inicialmente, todos los campos del TCP no están encriptados y no hay autenticación alguna. **Connectionless**: no existe ningún contexto entre dos datagramas.

### Ataques clásicos

- **Interceptación de contraseñas**: los protocolos que no implementan un canal seguro son sujetos a interceptación.
- **ARP spoofing**: ataque LAN. Se busca asociar la IP del atacante con la MAC del atacado para poder conseguir que el tráfico enviado del emisor llegue también al atacante. Fácil de realizar por la propia definición del protocolo ARP.
- **Ataque TCP SYN**: inundamiento con SYN. Nos basamos en el protocolo TCP para mandar muchos SYN, ya que el servidor debe de mantener las peticiones abiertas hasta por 75 segundos. La cola se llena y no se reciben más peticiones -> Ataque DoS. 
- **IP spoofing**: similar al ARP spoofing. El atacante busca enviar datos desde una IP que no es la suya.
- **Ataque smurf**
- **IP source routing**
- **Ataques RIP**
- **Ataques ICMP**
- **Ataques de amplificación UDP**:  conocidos como ataques DRDoS, una forma de ataque DDoS. El atacante envía a un servidor una falsa petición con la IP de la víctima. Se envía un número arbitrario de bytes.

### Defensas
- Tratar TCP/IP como un canal inseguro
- Implementar seguridad End-to-End para las aplicaciones
	- [[1730133054 - Protocolo TLS|Protocolo TLS]]
	- VPNs
- Filtrado de red y [[1759244707 - Control de acceso|Control de acceso]].

## Escaneo de redes

### Descubrimiento de hosts o redes

A partir de una dirección de red (conjunto de direcciones IP), descubrir cuántos de los hosts que viven ahí están vivos y corriendo.

#### Usando DNS

Comandos como `nslookup, host, dig`:
- *nslookup*: simples *look-ups* de DNS
- *host*: más detalles que *nslookup*
- *dig*: incluso más información

También se usan *ICMP pings, TCP SYN pings* y *TCP ACK pings*. Muchos de ellos no funcionan o están bloqueados.

### Descubrimiento de puertos

Descubrir puertos -> obtener información sobre los servicios que se están ejecutando en host remoto.
- Descubrir servicios
- Descubrir dispositivos conectados
- Introducir *malware*

#### Técnicas

- TCP SYN (stealth) scan:
	- Envía paquete TCP con la flag SYN
	- Host remoto envía SYN+ACK -> ya tenemos nueva info. RST -> significa que no hay nadie
	- Si no llega nada, está filtrado por un firewall, host down...
## Seguridad web