---
aliases:
  - Direccionamiento IP
tags:
  - review
"References":
cssclasses:
sr-due: 2024-10-17
sr-interval: 1
sr-ease: 230
---
# Direccionamiento IP

Todo dispositivo que se conecte a internet tiene una dirección IP *dependiente de la conexión en ese momento*.

>[!NOTE]
>Un router tiene una dirección IP por cada red que conecta.

>[!CAUTION]
>Una dirección IP del tipo V4: $80.22.32.1$ . Todos esos números deben de ser *convertidos a binarios de 8 bits*. El rango máximo de la V4 es de $[0.0.0.0, 255.255.255.255]$

>[!BUG]
>Las direcciones IP no pueden ser únicas, es computacionalmente imposible. Para ello tenemos:
>- IP del tipo V6: una versión IP mejorada que permite más IPs
>- Direccionamiento privado: son direcciones reservadas, no se pueden usar en el internet. Dentro de cada red (con una IP), podemos usar IP que sean solamente válidas para dicha red pública.

**Máscara de red**: las direcciones IP disponibles van a ser $2^n$ donde $n$ es igual al número de ceros totales que tenemos.

Por ejemplo: $255.255.255.128 \rightarrow 255.255.255.10000000$ 
Tenemos  $2⁷$ posibles IPs, pero tenemos que reservar siempre 2:
- La de menor valor -> el ID de la red
- La de mayor valor -> dirección de broadcast

>[!NOTE]
>Cuando nos referimos a una red (usualmente LAN): **IP/Máscara**. Cuando nos referimos a una IP: **IP**.

La capa de transporte está conformada por: **los algoritmos de selección de ruta**, la tabla de envío (prefijo de red, salida, siguiente salto), el protocolo IP y el protocolo ICMP.

TTL -> Time to live. El número de saltos que quedan restantes antes de que se mate al mensaje. Si $TTL = 1$, el mensaje se borra de la red.


***