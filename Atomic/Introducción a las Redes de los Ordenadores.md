# Información Básica

**LAN**: conjunto de dispositivos que están conectados a una misma red local.
**ISP**: Internet Service Providers. Operadoras en español (e.j. Telefónica)
**Dirección MAC**: identificador único de una tarjeta de red. Identifica inequívocamente al dispositivo. Forma de seis pares de números hex. separados por  `.`

Internet se divide en varias capas. Aunque no hay una jerarquía exacta, sí que siguen un *orden de implementación*.  Estas son:
1. Nivel 1: Físico 
2. Nivel 2: Enlace
3. Nivel 3: Red
4. Nivel 4: Transporte
5. Nivel 5: Aplicación

> [!warning]
> El **nivel físico** no se ve en detalle en este curso, mientras que **el nivel de red** es especialmente importante.

>[!info]
>Siempre entra en el examen un ejercicio de direccionamiento de IP con creación de `n` subredes.

---
# Protocolos

Sistema de reglas que permite a dos o más entidades (*hosts*) comunicarse y transmitir información entre ellas.
#protocolosRed 

---
# Router y enrutamiento (routing)

El **router** se encarga de recibir un mensaje y decidir por qué salida tiene que salir ese mensaje (usando algoritmos de redirección).
El **enrutamiento** es el mecanismo que se encarga de seleccionar la mejor ruta para los mensajes que vayan a un destino fijado.

---
# Switches
El switch permite, de manera lógica (antiguamente era física), seleccionar una forma de interconexión para conectar equipos en red formando una LAN.
#LAN 

---
# Diferencia entre CONMUTACIÓN DE PAQUETES Y CIRCUITOS

**Conmutación de paquetes**: el mensaje se trocea en pequeños mensajes (paquetes) y al ser enrutados, pueden seguir rutas distintas.
**Conmutación de circuitos**: el mensaje se trocea igualmente (esto es opcional), pero todos siguen la misma ruta.

>[!info]- Ventajas del almacenamiento de conmutación de paquetes
>- Mejora de tiempo, disminuyendo los [[Retardos]]
>- Almacenamiento óptimo
>- Mejor manejo de errores

>[!error]- Desventajas del almacenamiento de conmutación de paquetes
>- Necesidad de ordenar el mensaje al llevar a su destino

---
>[!faq]- ¿Cómo se conectan miles de operadoras (ISP) entre ellas?
>Se generan varias ISP`x`que se conectan con algunas operadoras. Estas mismas ISP`x`se conectan entre ellas.
