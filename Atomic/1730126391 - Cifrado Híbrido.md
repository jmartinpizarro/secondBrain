---
aliases:
  - Cifrado Híbrido
tags:
  - review
  - AES
  - "#RSA"
References: 
cssclasses:
---
# Cifrado Híbrido

Combinamos los [[Cifradores simétricos de bloque y modos de operación de cifrado]] y el [[1729420141 - Cifrado Asimétrico|Cifrado Asimétrico]]. 
Utilizamos los criptosistemas de cifrado asimétrico para distribuir las claves secretas, y cifrar el mensaje con criptosistemas de cifrado simétricos.
1. El texto en claro M se cifra simétricamente (e.g., AES) con una clave de sesión $K(S)$ que se genera en ese momento de forma aleatoria
2. La clave de sesión $K(S)$ se cifra asimétricamente (e.g., RSA) con la clave pública $K(U, B)$ del destinatario
3. El destinatario descifra primero la clave de sesión $K(S)$, luego con ésta, descifra el mensaje cifrado
***