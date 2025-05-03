---
aliases:
  - Paso de mensajes
tags:
"References":
cssclasses:
---
# Paso de mensajes

Dos operaciones básicas:
- *send()*
- *receive()*

Existen unos factores a tener en cuenta:
- Longitud del mensaje: fija o variable
- Flujo de datos: bidireccional o unidireccional
- Nombrado: comunicación directa o indirecta
- Sincronización
- Almacenamiento: existen estructuras intermedias en la comunicación.
- Fiabilidad
- Representación de datos, serialización. 

## Nombrado

### Comunicación directa

- *send(P, m)*: enviar un mensaje $m$ al proceso $P$
- *receive(Q, m)*: recibir un mensaje $m$ del proceso $Q$
- *receive(ANY, m)*

### Comunicación indirecta

Los datos se envían a estructuras intermedias: 
- Colas: múltiples emisores y receptores.
- Puertos: se asocian a un proceso. 

## Esquemas de comunicación (middleware)

Utilizados en mecanismos de comunicación basados en llamadas a procedimientos remotos o invocación de métodos remotos.

- XDR
- CDR
- Protocol Buffers

Para más información, ver [[1746195531 - Servicios Distribuidos|Servicios Distribuidos]].

## MPI - Message Passing Interface

Interfaz estándar de paso de mensajes para el desarrollo de aplicaciones paralelas que se ejecutan en ordenadores que no comparten memoria.

- Portabilidad
- Eficiencia
- Funcionalidad

Todos los procesos ejecutan el mismo programa, todas las EDAs y variables son locales con respecto a cada proceso.

