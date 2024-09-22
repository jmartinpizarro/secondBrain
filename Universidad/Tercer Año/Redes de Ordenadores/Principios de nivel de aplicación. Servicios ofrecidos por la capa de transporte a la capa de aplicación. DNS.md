
Podemos identificar dos tipos de nivel de aplicación
- **Servidor**: siempre operativo. Tiene una IP fija.
- **Cliente**: el usuario contacta con el cliente, y el cliente con el servidor. Puede no estar siempre operativo. Puede tener una IP dinámica. No se comunican entre clientes.

También existe las arquitecturas **Peer to Peer** (Torrent). Entre sus características se encuentran:
- Los clientes son servidores
- Entre ellos mismos se envían y reciben información.
- *Peer 1* pide permiso a *Peer 2*, para que *Peer 2* de un servicio al *Peer 1*.
- Cambian de IP, manejo complicado.

# Comunicación: el proceso

Cuando te conectas al internet no te conectas tú, sino que se conectan dos procesos.

**Process**: programa que corre en un host

En el mismo host, varios procesos se pueden comunicar (comunicación de inter-procesos). Pero *si es un host distinto*, estos procesos se comunican a través de mensajes. Esto se hace usando **sockets**

## Sockets

El proceso envía o recibe mensajes desde un socket. El socket está entre la capa de aplicación y de transportes. A partir de ahí se procesa y/o generan las cabeceras necesarias.

Para recibir un mensaje, el proceso tiene que tener un *identificador* y *las direcciones IP* (ID del proceso). Incluye tanto la dirección IP y los puertos asociados con el proceso y el host.

## Protocolos de aplicación

Establece ciertas características como:
- **Tipos de mensajes intercambiados**: request, response
- **Sintaxis del mensaje**: campos en los mensajes
- **Semántica del mensaje**
- **Reglas** para cómo y cuando el proceso envía y responde a los mensajes.
- **Protocolos abiertos** y **propietarios**

# Servicios ofrecidos por la capa transporte
## ¿Cómo seleccionar nuestro servicio de transporte?

Dependiendo de:
- Integridad de los datos: algunas apps necesitan el 100% de los datos, otras no hace falta
- tiempo: algunas apps como Gmail no priorizan el tiempo de llegada, otras como el gaming, sí.
- Rendimiento
- Security: encriptación, integridad de los datos.


Sabiendo esto, podremos elegir uno de los siguientes servicios:
- TCP:
	- Transporte confiable
	- Control de flujo
	- Control de congestión
	- No se encarga de tiempos, rendimiento o seguridad
	- Orientado a conexiones cliente-servidor.
- UDP:
	- No es muy confiable en lo que respecta a enviar datos. Si recibe una respuesta afirmativa por parte del receptor, le envía toda la información de golpe (es muy rápido).
	- No se encarga de la confiabilidad, flujo de control, control de congestión, tiempos, rendimiento, seguridad...

>[!question]- UDP es nefasto, ¿por qué existe?
>Porque a veces interesa que la conexión sea muy rápida. En llamadas telefónicas, gaming, interesa la velocidad. Con TCP, la imagen puede congelarse (por pérdidas de datos), lo cual no es deseable en estos ámbitos.

## Seguridad en TCP

El problema del TCP Vanilla es que no hay encriptación. Las contraseñas que se han enviado al socket son texto plano sin cifrar.

Con **TLS** o Transport Layer Security, se generar conexiones encriptadas que aseguran la integridad de los datos y hay una autenticación en el otro extremo.

# DNS

El DNS actúa como un traductor de nombres de dominio a IPs. Especialmente importante en webs y alias de los emails. 

Son bases de datos que guardan la información de cada servidor y cada dirección IP. Hay 13 servidores raíz físicos en todo el mundo.

**¡Los servidores DNS están jerarquizados en forma de árbol!**

¿Cómo sabemos la dirección IP? Supón $www.ejemplo.com$. 
1. El cliente hace una query al nodo raíz para encontrar el servidor DNS $.com$ 
2. El cliente hace una query al nodo $.com$ para encontrar $ejemplo.com$
3. El cliente comprueba la dirección IP de $ejemplo.com$ y devuelve el resultado.

## Servidores autorizados

Dos tipos:
- Servidores Top-Level Domain (TLD): responsables de $.com \space .edu \space ...$ y todas las terminaciones de países $.es \space .fr \space .uk$...
- Servidores DNS Autorizados: mantenidos por organizaciones, se encargar de proveer de las direcciones IP.
# Archivos DNS

Se pueden guardan en caché usando el TTL (Time to Live), que también se envía en protocolos. 

Hay varios tipos de archivos, siempre manejando dos parámetros `name` y `value`:
- type=A: manejan el hostname y la IP.
- type=NS: manejan el domain y el hostname del servidor autorizado
- type=CNAME: manejan el nombre canónico (alias).
- type=MX: maneja el servidor de email asociado al nombre 