---
aliases:
  - Certificados e Intraestructuras de Clave Pública
tags:
  - review
"References":
cssclasses:
---
# Certificados e Intraestructuras de Clave Pública

El certificado de clave pública incluye:
- Identidad del sujeto A
- Clave pública de A
- Algoritmo de la clave pública
- Identidad del emisor AC
- Período de validez ($T_1, \space T_2$)
- Número de serie
- Firma digital sobre lo anterior emitida por AC con el algoritmo de firma S y su clave privada $K_{V, AC}$
- Algoritmo de firma
- Hash: cuando firmamos, no firmamos todo esto; sino que firmamos el hash de todo lo anterior.
- Extensiones

Dados dos emisores, $A$ y $B$, si $A$ quiere enviar un mensaje firmado, $B$ lo recibirá en el siguiente formato:
$$M, S(K_{V, A}, M), C_A$$
donde $S$ es la firma del emisor $A$.

## Infraestructura de Clave Pública PKI

Define la estructura de los certificados X.509 y de las listas de certificados revocados. 

A efectos prácticos; define un **modelo jerárquico** de Autoridades de Certificación y Autoridades Relacionadas, definiendo el conjunto de protocolos operacionales y gestión.

![[PKI.png]]

- *CA Raíz*: emite un certificado a sí misma y a sus autoridades subordinadas de primer nivel. Es el máximo exponente y en teoría, son seguras de confiar.
- *CA subordinadas L1*: emiten el certificado a sus autoridades subordinadas de segundo nivel. Es el paso intermedio.
- *CA subordinadas L2*: emiten certificados a usuarios finales, ayudadas por autoridades de registro.

Este árbol se comunica a través de una *cadena de certificación*, donde los niveles más bajos van comprobando recursivamente si el certificado generador superior es válido (y seguro) o no.

## Certificado X.509

Estándar del certificado, conformado por:
- Versión actual: 3
- Número de serie: identifica de manera única al certificado dentro del ámbito de la AC (identidad del emisor)
- Emisor: quién genera el certificado
- Período de validez: `[No válido antes, No válido después]`
- Sujeto: sujeto propietario del certificado
- Clave pública: información de la clave pública contenida en el certificado y algoritmo de clave pública.

Existen *varios tipos de certificados*:
- Persona física
- Persona jurídica
- Componente
- Firma de código

## Validación de estado de un certificado

Se han desarrollado dos protocolos (entre otros) para lograr una validación correcta y sin errores:
- Certificados Revocados - Certificate Revocation List - CRL: 
	- Actualización periódica
	- Generan un período de incertidumbre hasta *nextUpdate*. Solución: período de precaución.
	- Generan problemas de consumo de ancho de bandas. Soluciones: over-issued CRLs, Delta CRLs, CRLs segmentadas, CRLs segmentadas.
- Método de consulta OCSP - Online Certificate Status Protocol - Es usado por el CRL:
	- Facilita la consulta mediante un protocolo sencillo y muy pequeño (tamaño)
	- Pueden proporcionar el estado actualizado en todo momento

La **lista de certificados revocados** las emite la identidad emisora (AC). Los certificados expirados no se expiden en la lista. 

## Almacenamiento de claves

Dos métodos:
- Software
	- Repositorio de claves en la web
	- Fichero específico protegido
- Hardware
	- Tarjeta Inteligente
	- Token USB
	- Chip TPM
	- HSM

## Certificate Pinning vs Certificate Transparency

**Certificate Pinning**: mecanismo de seguridad en el que se asocia a un host con su certificado X.509 o su clave pública 

Cuando un cliente conoce el certificado o la clave, asocia esa información a un host durante un tiempo $t$. Durante ese tiempo, si el certificado o la clave difiere de la previamente mencionada, se rechaza la comunicación.

Sin embargo, tiene sus desventajas dado malas prácticas o abusos. Se ha creado un nuevo mecanismo:

**Certificate Transparency**: marco que permite registrar logs, monitorizar, y auditar los certificados de clave pública emitidos de forma transparente.
1. Cada certificado emitido se añade a un registro público, incluyendo una cadena de certificación correcta (verificada) hasta una autoridad raíz en la que se confía.
2. Un host puede consultar qué certificados han sido emitidos a su nombre, y denunciar los que no son auténticos
3. Los certificados de los hosts incluyen extensiones que referencian el registro y permiten a los clientes verificar que el certificado está realmente asociado a ese host.

## Modelo descentralizado

No existe una autoridad de certificación y cada usuario certifica las claves de los usuarios en los que confía. Se puede establecer una cadena de confianza de $n$ saltos. Destaca la **rápida implementación, sencillez y menos costes**.

Sin embargo, **no es escalable y tiene la necesidad de transmitir una clave pública por un canal seguro antes de certificarla**.
***