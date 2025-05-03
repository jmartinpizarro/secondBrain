---
aliases:
  - Sistemas de ficheros distribuidos
tags:
"References":
cssclasses:
---
# Sistemas de ficheros distribuidos

Software de sistemas que establece una correspondencia lógica entre los ficheros y los directorios y los dispositivos de almacenamiento.

Funciones:
- Organización, almacenamiento, recuperación, gestión de nombres, coutilización y protección de ficheros.
- Ofrece un mecanismo de abstracción que oculta todos los detalles relacionados con el almacenamiento y distribución de la información, así como el funcionamiento de los mismos.

## Sistemas de ficheros

Exporta una jerarquía de ficheros y directorios con un conjunto de restricciones y métodos de acceso.
- Ofrece una semántica e interfaz de usuario
- Coordina el acceso a datos desde varias peticiones
- Gestiona la utilización de discos
- Gestiona y mantiene la integridad de los datos

**Operaciones:**
- Crear
- Montar
- Desmontar

### Ficheros y directorios

- Ficheros: datos y atributos
- Directorio: relaciona nombres con ficheros
- Metadatos: información almacenada por los sistemas de ficheros para la gestión de ficheros y directorios.

## Requisitos de un sistemas de ficheros

- Transparencia
	- Mismas operaciones para acceso locales y remotos
	- Imagen única del sistema de ficheros
- Eficiencia: un SFD tiene sobrecargas adicionales
- Tolerancia a fallos: replicación, funcionamiento degradado.
- Escalabilidad
- Consistencia
- Actualizaciones concurrentes
- Seguridad

Se introduce el uso del protocolo [[1746259445 - Network File System - NFS|Network File System - NFS]] para mayor heterogeneidad. 
## Componentes de un SFD

Modelo cliente-servidor. 
- Servicios del sistema de ficheros: operaciones proporcionadas por los clientes
- Servidores del sistema de ficheros: procesos de usuario o del sistema que ofrecen los servicios correspondientes y responden a las peticiones de los clientes.

## Servicio de directorio

Se encarga de la **traducción** de nombres de usuario a identificadores de ficheros únicos (UFID).

**Directorio**: relaciona de forma única nombres de fichero con UFID.

Dos opciones:
- Los directorios son objetos independientes gestionados por un servidor de directorios (SD).
- Los directorios son ficheros especiales. Servidor de ficheros y de directorios combinado.

Operaciones:
- lookUp(dir, name) -> fileId
- addName(dir, name, fileId)
- removeName(dir, name)
- getNames(dir)

## Métodos de acceso remoto

- Modelo carga/descarga: transferencias completas del fichero servidor->cliente.
- Modelo de servicios distribuidos: el servidor proporciona todas las operaciones sobre el fichero.
- Empleo de caché en el cliente: combina los dos modelos anteriores.

### Caché en bloques

El uso de la caché mejora el rendimiento, especialmente en las operaciones de lectura y en las de escritura. 

Se encuentra en:
- Caché en cliente:
	- Reducen los accesos al disco
- Caché en servidor:
	- Reducen tráfico por red
	- Reducen la carga de los servidores
	- Puede estar en discos locales o en la memoria principal

>[!DANGER] Coherencia de caché
>El uso de la caché introduce este problema: surge cuando se coutiliza un fichero en escritura, lo que genera una inconsistencia entre versiones.

Existen soluciones, pero la más lógica es el **empleo de [[1746258717 - Protocolos de coherencia de caché|Protocolos de coherencia de caché]]**.
### Tolerancia a fallos

- Servidores **con estado**: cuando se abre un fichero, el servidor almacena información y da al cliente un identificador único a utilizar en posteriores llamadas. Cuando se cierra un fichero se libera la información.
- Servidores **sin estado**

**Ventajas de con/sin estado**:
1. Con estado:
	- Mensajes más cortos
	- Mejor rendimiento 
	- Facilita lectura adelantada
2. Sin estado:
	- Más tolerante a fallos
	- No se gasta memoria en el servidor

## Sistemas de ficheros paralelos

- Múltiples nodos E/S, incrementa el ancho de banda.
- Fichero distribuido entre diferentes nodos de E/S.
	- Acceso paralelo: 
		- A diferentes ficheros
		- Al mismo fichero
- Interfaces de E/S paralela
- Optimizaciones 
	- E/S colectiva
	- Acceso a datos no contiguos.
