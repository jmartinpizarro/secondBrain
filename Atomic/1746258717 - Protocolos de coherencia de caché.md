---
aliases:
  - Protocolos de coherencia de caché
tags:
"References":
cssclasses:
---
# Protocolos de coherencia de caché

Permitir el uso de caché en los clientes manteniendo coherente la información de acuerdo a la semántica de coutilización que define un sistema de ficheros.

Aspectos del diseño a considerar:
- Granularidad del protocolo: tamaño de la unidad sobre la que se mantiene la coherencia
- Mecanismo de validación: determinar si un dato es consistente o no. 
	- La validación comienza en el lado del **cliente**. La frecuencia varia: en cada acceso, al abrir el fichero, periódicamente.
	- La validación comienza en el lado del **servidor**. Rompe el modelo cliente/servidor.
- Mecanismos de actualización: 
	- **Actualización de copias**: excesivo tráfico en la red. Inviable en sistemas de ficheros
	- **Invalidación de copias**: se invalidan las copias y los futuros accesos se realizan sobre una copia consistente. Mensajes más cortos, menos sobrecarga de red.
- Localización de las copias en los cachés de los clientes:
	- Directorios centralizados: posible cuello de botella.
	- Directorios distribuidos.

