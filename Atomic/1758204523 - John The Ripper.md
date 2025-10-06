---
aliases:
  - John The Ripper
tags:
  - ciberseguridad
  - password
References:
cssclasses:
---
# John The Ripper

La instalación se ha hecho desde el (binario en [GitHub](https://www.github.com/openwall/john)).

`john --help` -> para ver información sobre la herramienta.

## Ejemplo 1

1. Generamos un archivo con un hash sobre la palabra "hola"
```bash
mkpasswd --method=md5crypt hola > hash.txt
```
2. Rompemos el contenido del hash. 
```bash
john hash.txt
```

**OUTPUT**:
```bash
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 128/128 AVX 4x3])
Will run 16 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst, rules:Wordlist
hola             (?)
1g 0:00:00:00 DONE 2/3 (2025-09-18 16:17) 25.00g/s 96000p/s 96000c/s 96000C/s modem..Skippy
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

>[!DANGER]
>Si estudiamos el diccionario default que usa *john*, veremos que usa una serie de contraseñas. De usar ese tipo de contraseñas en nuestro archivo, serán descubiertas
>casi al momento.

## Usando un diccionario custom

1. Generamos nuestro propio diccionario
```bash
echo 'uc3m' >> dict
echo 'ludo' >> dict
```

2. Y lo usamos
```bash
john --wordlist=dict hash.txt
```

## Generar máscaras

- ?a -> una letra minúscula
- ?A -> una letra mayúscula
- ?d -> un dígito
- ?w -> una palabra del diccionario

$$mask = \text{?a?a?a}$$
Lo que podría generar secuencias de caracteres como: *aba*, *ftv*, *vmr*...


*john* es perfecto para generar cadenas de caracteres.

```bash
john --mask='?a?d' --stdout
```

```bash
john --wordlist=dict --mask='?w?d?d'
```

```bash
john --wordlist=dict --mask='?w?d?d' --stdout > passwords.txt
```



