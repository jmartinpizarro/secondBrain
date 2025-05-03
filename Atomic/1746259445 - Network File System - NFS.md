---
aliases:
  - Network File System - NFS
tags:
"References":
cssclasses:
---
# Network File System - NFS

Implementación y especificación de un servicio de acceso a ficheros remotos, diseñado para trabajar en entorno heterogéneos (distintos sistemas operativos, máquinas...)

La independencia se consigue usando las RPC creadas con el protocolo XDR. 

Las diferentes máquinas **montan un directorio remoto en el sistema de ficheros local**. 

## Montado en NFS

Establece una conexión lógica entre cliente-servidor.

La máquina $A$ exporta $/usr$ y $/bin$. 
En la máquina $B$:
$mount$, $\text{maquinaA:/usr}$, $/usr$

## Protocolo NFS

Ofrece un conjunto de RPC para realizar operaciones sobre ficheros remotos. 
- Búsqueda de un fichero en un directorio
- Lectura de entradas de directorio
- Manipulación de enlaces y directorios
- Acceso a los atributos de un fichero
- Lectura y escritura de ficheros

Los servidores NFS **no almacenan estado**. **No ofrece mecanismos de control de concurrencia para asegurar una semántica UNIX**. 




