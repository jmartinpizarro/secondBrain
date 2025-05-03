---
aliases:
  - Comunicación y sincronización entre procesos
tags:
"References":
cssclasses:
---
# Comunicación y sincronización entre procesos

Es común el uso de ***threads* o hilos** para permitir **paralelización** en la comunicación entre procesos.

Un hilo puede tener varios estados:
- Ejecutado
- Listo
- Bloqueado: por comunicación o por acceso del disco

### Condiciones de carrera

Ocurre si varios *threads* acceden a un recurso compartido sin control, de forma que el resultado depende del orden de ejecución.

Esto ocurre en una **sección crítica** (SC), un fragmento de código en el que los distintos procesos pueden acceder y modificar recursos compartidos.

##  Mecanismos de comunicación

- Ficheros: un proceso puede escribir datos y otro leerlos
- Pipes: mecanismo de comunicación y sincronización.
- Variables en memoria compartida: un proceso escribe en la memoria y otro lee la variable
- Paso de mensajes: el emisor realiza una operación *send()* y el receptor *receive()*. 

## Mecanismos de sincronización

- Señales
- Tuberías
- Semáfaros
- Mutex y variables condicionales
- Paso de mensajes


