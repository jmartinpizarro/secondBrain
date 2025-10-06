---
aliases:
  - Autenticación en ciberseguridad
tags:
"References":
cssclasses:
---
# Autenticación en ciberseguridad

## Autenticación de usuario

**Autenticación**: el proceso de confirmar una identidad.

### Autenticación vs Identificación

**Identificación**: el acto de asertir en quién es una persona.
**Autenticación**: el acto de comprobar una identidad asertida. 

## Autentificadores

- **Memorized Secrets**
- **Look-up secrets**
- **Out of band secrets**
- **Single-factor OTP device**
- **Multi-factor OTP device**
- **Single-factor crypto software**
- **Multi-factor crypto software**
- [[1758639814 - Biometrics|Biometrics]]

### Ataques a los autenticadores

- Se puede revelar, adivinar, observar o interceptar mientras se entra el dato, revelado por el usuario a través de *phishing* o *social engineering*,
- Puede ser perdido, dañado, robado o clonado.
- Puede ser clonado.

## Gestores de contraseñas

Guarda todas las bases de datos en una DB que las protege con una contraseña maestra.

**Ventajas**:
- Mejora la seguridad
- Usabilidad para teléfonos móviles
**Desventajas**:
- Seguridad: si se rompe la contraseña maestra, se rompe todo
- Usabilidad: ¿de verdad se integran bien?
