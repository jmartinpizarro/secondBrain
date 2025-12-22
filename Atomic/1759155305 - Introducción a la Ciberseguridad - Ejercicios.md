---
aliases:
  - Introducción a la Ciberseguridad - Ejercicios
tags:
"References":
cssclasses:
---
# Introducción a la Ciberseguridad - Ejercicios

## Computer Security Concepts

**Problem 9**. Discuss similarities and differences between the concepts of *defense in depth* and *zero trust*.

*Defense in depth* usa una estrategia de seguridad a través de capas (técnicas, administrativas, físicas...) para proteger los datos. Si una capa falla, existen otras para cubrirla.

Por otro lado, *zero trust* asume que todo dispositivo/usuario debe verificarse al momento de entrar al sistema y mientras esté en él para reducir accesos inesperados.

---

## Computer Security Principles

**Problem 15**.

Por defecto, el usuario nunca debe de poder estar verificado. Al ejecutar el código de esa manera, existe la posibilidad de modificar el valor de la variable y entonces permitir accesos inesperados a la aplicación.

---

**Problem 16**.

Al hacer *access()*, es posible que se nos pida una contraseña. Sin embargo, con el resto de llamadas al sistema esto no ocurrirá: es una decisión de diseño de los sistemas UNIX que rompe con el principio de **autenticación** en el acceso a los datos.

---

**Problem 17**.

**Principle of Least Privilege (PoLP)**: los usuarios o sistemas solo requieren el mínimo de privilegios de sistema para poder realizar sus funciones.
**Separation of Privilege (SoP)**:  principio de diseño en el que el acceso a funciones o servicios críticos se divide con distintos privilegios, usuarios o componentes.

---

**Problem 18**.

Llamar de esa manera a un archivo Python puede crear una vulnerabilidad del tipo **TOCTOU** - Time-Of-Check to Time-To-Use).

Para solucionarlo, hay que crear el fichero con las *flags*  y los permisos de manera atómica, para después usar llamadas al sistema operativo `os.open()` para evitar esto.

```python
def create_config_file(path: str):
	flags = os.O_WRONLY | os.O_CREAT 
	mode = 0o600
	
	try:
		fd = os.open(file_path, flags, mode)
		with os.fdopen(fd, "w") as file:
			file.write("confidential data")
	except Exception as e:
		raise Error("Something happened")
```

---

**Problem 19**.

Afecta principalmente a la **integridad**. ¿Cómo sabemos realmente que ese dato no se ha visto afectado de manera externa por un atacante? Mecanismos deben de ser integrados para evitar que agentes externos cambien el servicio DNS a una ruta que a ellos les interese.

## Threats and Threat Modelling

**Problem 20**.

*STRIDE model*: ayuda a identificar vulnerabilidades en seis tipos
- **Spoofing**: pretender que eres alguien distinto a ti mismo
- **Tampering**: modificar algo en el disco, la red, memoria...
- **Repudiation**: ocurre algo que tú no has hecho
- **Information Disclosure**: dar información a alguien que no debería tener acceso
- **Denial of service**:
- **Elevation of privilege**: permitir a alguien realizar algo que no debería estar permitido hacer

---

**Problem 21**.

1. Sabiendo que tratamos sobre la intención, capacidad y oportunidad, podemos reducir los riesgos de manera significativa si (relacionado con la intención) podemos identificar posibles intenciones maliciosas sobre nuestra máquina: una base de datos tiene datos relevantes. Sabiendo esto, tenemos un montón de ataques que nos pueden hacer, los cuales conocemos contramedidas y podemos implementarlas.

---

**Problem 23**.

- Impacto funcional: el sistema atacado deja de funcionar correctamente, limitando los servicios que ofrece
- Impacto de información: la información del sistema se ha visto dañada, ya sea a través de MIGI (Modificación, Interceptación, Generación o Interrupción)
- Restauración: existe o no la posibilidad de restaurar el sistema a su estado original.
- Reputación de marca y riesgo legal

---

**Problem 24**.

**Ransomware**

Este tipo de ataque suele mucho más general: se ha creado por equipos grandes para un diseño y desarrollo relativamente rápido.

*TTPs*: se basa sobretodo en phishing, encriptación y extorsión a través de *data leak*.

Sus objetivos son relativamente indiferentes, aunque siempre buscan una infraestructura crítica de algún sistema.

**Cyber espionage**

Por otro lado, los equipos de desarrollo de este tipo de técnicas son mucho más pequeños, usualmente especializados, con militares o equipos de inteligencia.

*TTPs*: de manera encubierta siempre, tener acceso de manera persistente a algunas vulnerabilidades,.

Sus objetivos son mucho más precisos: empresas de investigación, militares, intel...

**Problem 27**.

- Spoofing:  el atacante se hace pasar por una entidad confiable o con privilegios. Es un ataque de tipo **activo**.
- Sniffing: interceptar y monitorizar paquetes de datos que viajan por la red. Es un ataque de tipo **pasivo**.

Las dos técnicas se usan para el ataque *Man in the Middle*.

