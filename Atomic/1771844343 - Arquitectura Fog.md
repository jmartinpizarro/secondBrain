---
aliases:
  - Arquitectura Fog
tags:
"References":
cssclasses:
---
# Arquitectura Fog

El objetivo es mejorar la eficiencia y reducir la cantidad de datos que deben transportarte a la nube para su procesamiento, análisis y almacenamiento. A menudo se hace para mejorar la eficiencia, aunque también puede utilizarse por razones de seguridad.

Ya no es necesario enviar todos los datos a una fuente lejana, sino que se envían al sistema FOG (nodos de niebla), dispositivos locales capaces de llevar a acabo estas tareas de manera más cercana al lugar de generación de los datos. Esto conlleva varios beneficios:
- Menor latencia
- Mejora en la seguridad
- Ahorro en el ancho de banda de red

FOG no busca reemplazar a la nube, sino complementarla. Al asumir tareas de análisis de datos, libera recursos en la nube para tareas más intensivas y asegura una mayor disponibilidad de recursos en general.

Pero también tiene ciertas desventajas:
- Mayor complejidad de red
- Desafíos de mantenimiento
- Mayor consumo de energía

### Nodos físicos y virtuales

Dispositivos generadores de datos y pueden abarcar un amplio espectro tecnológico.

### Nodos de niebla

Los nodos de niebla son dispositivos independientes que recogen la información generada. Los nodos de niebla se dividen en tres categorías:
- Dispositivos de niebla: almacenan los datos
- Servidores de niebla: procesan los datos
- Puertas de enlace: redirigen la información entre los dispositivos y servidores de niebla

### Servicios de supervisión

Incluyen interfaces de programación de aplicaciones que realizan un seguimiento del rendimiento del sistema y la disponibilidad de recursos. Los sistemas de supervisión garantizan que todos los dispositivos finales y los nodos de niebla estén activos y que la comunicación no se interrumpa.

A veces esperar a que un nodo se libere puede ser más costoso que acceder a un servidor en la nube.
