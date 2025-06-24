---
aliases:
  - Servicios Web
tags:
"References":
cssclasses:
---
# Servicios Web

## Paradigma de servicios web

### Generación 1

1. El navegador web pide una página web indicando su identificador URI en la misma petición.
2. El servidor web busca el fichero almacenado que se corresponde con la URI pedida y lo envía como respuesta.

Se utiliza el protocolo HTTP para la transferencia de contenido.

### Generación 2

Más tarde se añade la posibilidad de enviar datos al servidor (POST o GET) a través de formularios.

- En el servidor: ejecución del programa al que se la pasa los datos del formulario y cuya salida se envía al cliente.
- En el cliente: páginas web, imágenes, videos para su ejecución en el cliente.

**Servlet**: se deriva de *applet*. Es un programa que se ejecuta en un servidor web. Permite generar páginas webs dinámicas a partir de los parámetros de la petición. Es un objeto Java que implementa o hereda una interfaz *javax.servlet.Servlet* para algún protocolo específico.

También aparece la **arquitectura de tres capas**:
- Capa de datos: donde se puede encontrar la capa de datos.
- Capa de aplicación: el propio servidor, donde se implementa toda la lógica.
- Capa de presentación: la parte del cliente.

### Tercera generación: servicios web

Es un conjunto de protocolos y estándares que sirven para intercambiar datos entre aplicaciones en redes de ordenadores, con diferentes sistemas operativos, lenguajes de programación o arquitecturas.

Protocolos usados:

- HTTP: transporte usado
- XML: describe los tipos de mensajes
- SOAP: empaqueta información y la transmite entre cliente-servidor
- WSDL: descripción de un servicio
- UDDI: lista de servicios disponibles

#### Arquitectura SOA: Service Oriented Architecture

Arquitectura en la que el software se expone como servicio, que es invocado utilizando un protocolo estándar de comunicación

Permite que diferentes aplicaciones puedan interoperar entre ellas a través de módulos independientes. 

---

Permite **paso de cortafuegos, interoperabilidad y compatibilidad**.

No es bueno porque **no dispone de servicios de apoyo, tiene un rendimiento más bajo (requiere una conversión a XML) y existen potenciales problemas de seguridad**.


