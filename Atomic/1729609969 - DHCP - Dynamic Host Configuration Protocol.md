---
aliases:
  - DHCP - Dynamic Host Configuration Protocol
tags:
  - review
  - ip
References: 
cssclasses:
---
# DHCP - Dynamic Host Configuration Protocol

El host obtiene dinámicamente la dirección IP desde la redes del servidor cuando se conecte a la red.
- Permite desconectarse de la red y liberar la dirección IP
- Permite reutilización de la dirección IP

>[!DANGER]
>DHCP funciona a nivel de aplicación, no a nivel de red.

DHCP tiene cuatro tipo de posibles paquetes:
1. Discover: lo envía el cliente. El cliente pregunta si hay alguien que de direcciones IP (busca a un servidor DHCP). El campo $yiaddr = 0.0.0.0$ y $transaction ID = randomInt$. Lo metemos en un segmento UDP (TCP no podemos ya que inicialmente no tenemos dirección IP). 
2. Offer: lo envía el servidor. le ofrece una dirección IP al cliente que ha enviado el Discover. Esa dirección se apunta como *ofrecido*, no como aceptado. También genera un TTL para ver si la IP es aceptada o no.
3. Request: lo envía el cliente. El cliente requiere poder usar dicha IP. El $transactionID += 1$. 
4. ACK: lo envía el servidor. A partir de este momento, el cliente ya puede usar la dirección IP.

El TTL fija el máximo que puede durar una conexión. El cliente puede hacer una petición para prolongar ese período, si no el cliente perderá esa IP.



***