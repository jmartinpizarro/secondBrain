---
aliases:
  - Examen Ciberseguridad - Enero 2024
tags:
"References":
cssclasses:
---
# Examen Ciberseguridad - Enero 2024

**Problem 1**

El principal problema de este fragmento de código es que, por defecto, permite el acceso al servicio. Esto rompe el principio de *fail-safe defaults*. Si la función `is_access_allowed()` devuelve otra cosa que no sea `ACCESS_DENIED`, como un fallo en memoria, una excepción o incluso un valor nulo, se permitirá el acceso al sistema; lo que puede generar caídas en el sistema o accesos maliciosos.

Para arreglarlo, es necesario cumplir el principio *fail-safe default*.

```python
a = is_access_allowed(user, resource);
if (a == ACCESS_ALLOWED) {
	// acceso permitido
} else {
	// por defecto, acceso denegado
}
```

---

**Problem 2**

El campo *salt* define el *salt* usado a la hora de crear un hash para una contraseña. Un *hash* es siempre determinista, tal que mismo input mismo output. Esto no es vulnerabilidad, pero sí que aumenta las posibilidades de poder encontrar el *hash* con mayor velocidad (un choque, por ejemplo).

Añadiendo un *salt* a cada contraseña, introducimos el factor de la aleatoriedad en la ecuación. Proporciona una capa extra de seguridad que, correctamente guardada, reduce el riesgo de colisión entre *hashes*.

---

**Problem 3**

Sabemos que existen dos tipos de permisos, para archivos (666) y para directorios (777), en este problema. Sabemos que se introduce una nueva mask del tipo 022.

Esto hace que se reduzcan los permisos de ambos campos quedando en:
- Archivos: 644: `rw-r--r--`
- Directorios: 755: `rwxr-xr-x`

---

**Problem 4**

Los ataques XSS (Cross-Site Scripting) se basan en la inserción de código malicioso como scripts para la posterior ejecución en el navegador de una víctima. Este tipo de ataque busca recoger las cookies u otros datos guardados en el *localStorage* del navegador. De esta manera, se puede acceder a los tokens de sesión de los usuarios y usarlos para acceder a sus cuentas.

1. El atacante inyecta código JavaScript en una entrada (url, formulario)
2. El servidor **devuelve dicho contenido tal cual** en la página web

`https://ejemplo.com/buscar?q=<script>alert("XSS")</script>`
`Resultados para: <b><script>alert('XSS')</script></b>`

---

**Problem 5**

Los *root store* se consideran las entidades más importantes, o entidades *root*, aquellas que solo se certifican a ellas mismas y al resto. Este tipo de entidades son empresas con gran confianza internacional que son capaces de firmar otros certificados a entidades más pequeñas o secundarias; todo esto para preservar la cadena de confianza de la emisión de certificados.

Se encargan de garantizar la confidencialidad e integridad de las comunicaciones, permitiendo la autenticación entre cliente-servidor.

Sin embargo, pueden verse comprometidas y afectar tal que:
- Emiten certificados falsos para cualquier dominio
- Rompen la seguridad global de HTTPS

---

**Problem 6**

- Attack Vector (AV): Adjacent. Esto significa que para que el ataque pueda lanzarse, ambos sistemas deben de estar adyacentes en la misma topología de red. 
- Attack Complexity (AC): Low. Esto significa un riesgo grande, ya que el ataque no requiere de gran complejidad para poder ser ejecutado
- Privileges Required (PR): None. No requiere de privilegios de ningún tipo, por lo que el ataque puede ser ejecutado por cualquier persona
- User Interaction (UI): None. No se requiere interacción atacante-usuario.
- Scope (S): Changed. Al ejecutar el ataque, la vulnerabilidad no se mantiene en un solo componente, sino que además extiende a otros componentes.
- Confidential, Integrity, Availability: High, None, High

---

**Problem 7**

1. Reinfectar un sistema es contraproducente por varios motivos, pero el principal es que tener varias instancias del mismo malware puede generar errores inesperados en el sistema. Además, reinfectar sistemas implica un tiempo de búsqueda que aumenta el tiempo que tarda en propagarse por la red. Además, implica un mayor tráfico lo que implica una mayor posibilidad de identificación del ataque.
2. Existen dos formas para detectar si el sistema ya ha sido infectado o no:
	1. **Fingerprints de puertos/servicios**: el nuevo malware se introduce en los puertos o servicios y busca respuestas características
	2. **Respuestas a protocolos con contenidos específicos**: se envían paquetes a los que se espera una respuesta determinada. Dependiendo de la respuesta, se lanza el malware o no.
3. Los defensores pueden:
	1. **Detectar firmas** que el malware usa para poder generar defensas contra él
	2. **Crear honeypots** a los que atraer el malware y poder investigarlo más detenidamente, muy seguramente siendo capaz de detectar las firmas del malware.
	3. Se puede conseguir una **detección temprana** del malware si se identifican los fingerprints o las firmas a tiempo.

