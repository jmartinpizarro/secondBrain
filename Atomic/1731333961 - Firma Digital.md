---
aliases:
  - Firma Digital
tags:
  - review
"References":
cssclasses:
---
# Firma Digital

Transformación de un documento que permite probar su autoría e integridad.

Si se aplica correctamente, se puede aplicar a:
- Autenticación de origen
- Integridad de los datos
- No repudio al firmante

>[!DANGER]
>Firma digital no ofrece *Confidencialidad* 

## Esquemas de firma

Podemos encontrar tres tipos tipos distintos de firmas:
- Algoritmo de generación de clave
- Algoritmo de generación de firma
- Algoritmo de verificación de firma

Podemos encontrar diversas características:
- Determinista: firma mismo mensaje -> mismo resultado
- Aleatorio: firma mismo mensaje -> depende de un índice

Hay dos variantes del esquema de firma:
- *Con recuperación del mensaje*: firma en el propio mensaje transformado
- *Con apéndice o separada del mensaje*: firma en apéndice

Como norma general:
1. Se calcula el resumen del mensaje y se firma el resumen
	- *Por eficiencia*: mensajes muy largos
	- *Por seguridad*: en El Gamal y RSA
2. Los datos firmados contienen: **datos originales** y **firma generada**
3. En la *verificación*, es necesario calcular el resumen de nuevo a partir de los datos en claro.

## Esquema de firma RSA

Características:
- Determinista
- Recuperación del mensaje

La seguridad se basa en la factorización de los números enteros (mismos tamaños de clave que para el cifrado).

## Esquema de firma El Gamal

Características:
- Aleatorio
- Con apéndice

La seguridad se basa en el logaritmo discreto. Usualmente no se usa este algoritmo, sino esquemas derivados, DSA o *Digital Signature Algorithm* o [[1730132101 - Diffie Hellman Efímero - DHE|Diffie Hellman Efímero - DHE]] basado en curvas elípticas.

## Estándar XAdES

El formato XML es el lenguaje entre máquinas. Una firma XAdES es un fichero XML. 

### Sellado de tiempo

Usado para demostrar que un conjunto de datos existía previamente, habiéndose mantenido inalterado desde entonces.

>[!DANGER]
>Sello de tiempo $\neq$ Marca de tiempo

## Esquemas de firma postcuánticos

Al igual que la criptografía asimétrica, la firma se verá afectada cuando la cuántica aparezca. Se han creado varios algoritmos basados en problemas matemáticos más complejos.

- ML-DSA (CRYSTALS-Dilithium): algoritmo de firma basado en retículos (versión modular)
- SLH-DSA (Sphincs+): algoritmo basado en funciones hash
- FN-DSA (Falcon): algoritmo de firma basado en retículos (transformada de Fourier)

**Árboles de Merkle**: permiten verificar eficazmente si elementos de datos específicos forman parte de un gran conjunto de datos, o si han sido modificados.
***