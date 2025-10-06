---
aliases:
  - Introducción a la Ciberseguridad
tags:
"References":
cssclasses:
---
# Introducción a la Ciberseguridad

## Qué es la ciberseguridad

La protección de activos (hardware, software o datos) que contenga un ordenador o un sistema informático.

Respecto a los activos, estos pueden tener un **valor subjetivo**:
- Coste monetario independiente
- Coste de reemplazo
- Coste personal

La relación de valor puede ser asimétrica entre el atacante y la víctima.

## CIA

- **Confidentiality**: solo personas o sistemas autorizados pueden acceder a los datos protegidos
- **Integrity**
- **Availability**

![[CIA-trad.jpg]]

## Vulnerabilidades, Amenazas, Riesgos y Peligros

### Vulnerabilidad

Debilidad en el sistema (especificación, diseño, implementación y procedimiento) que puede ser explotado para causar pérdidas o daños.

$\exists$ distintas vulnerabilidades:
- Autenticación débil
- Falta de control de acceso
- Errores en el programa
- Gestión inadecuada de los recursos
- Protecciones físicas inadecuadas
- Y mucho más

### Amenazas

Conjunto de circunstancias que tienen el potencial de causar daños o pérdidas. 

Pueden ser (MIGI):
- Modificación
- Interceptación
- Generación
- Interrupción

## Adversarios

Un adversario es alguien que explota una vulnerabilidad perpretando un ataque en el sistema.

## Principios de diseño

- Simplicidad:
	- Menos donde equivocarse
	- Menos inconsistencias
	- Más fácil de entender
- Restrictivo
	- Minimizar el acceso
	- Inhibir comunicaciones

### P1 - Least Privilege

Una entidad solamente debe de tener una serie de privilegios si y solo si son necesarios para completar una tarea.

### P2 - Fail-safe Defaults

La acción por defecto es denegar el acceso. Si la acción falla, el sistema sigue siendo seguro.

### P3 - Economy of Mechanism

Lo más simple posible (principio KISS); simple significa que menos cosas pueden ir mal. Crítico para interfaces e interacciones.

### P4 - Complete Mediation

Comprobar cada acceso.

### P5 - Open Design

La seguridad no debe de depender del secretismo del diseño o la implementación.

### P6 - Separation of Privilege

El privilegio o autoridad tiene que estar separado entre más de una entidad para prevenir fraude, sabotear, robo u otros malos usos.

### P7 - Least Common Machine

El mecanismo no debería ser compartido. Aislamiento de aplicaciones

### P8 - Acceptability

Los mecanismos de seguridad no deberían de añadir dificultad al acceso de un recurso.