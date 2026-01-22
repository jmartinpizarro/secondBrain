---
aliases:
  - Ejercicio Arquitectura de Datos - Diseño de cluster en MongoDB
tags:
"References":
cssclasses:
---
# Ejercicio Arquitectura de Datos - Diseño de cluster en MongoDB

**Problema 1. En base al enunciado previo:**
**A. Definir la clave de fragmentación.
B. Definir la estrategia de fragmentación.
C. Consideraciones sobre tu propuesta de diseño.**

---

a. 

Como clave de fragmentación de la colección RESERVAS se define {hotelId, fechaReserva} para agrupar las reservas por el hotel y la fecha de reserva, optimizando las consultas donde reservas por hotel en un período específico.

Para HABITACIONES, la clave de fragmentación es {hotelId}, ya que es la más importante para las consultas generales relacionados con las habitaciones del hotel

---

b.

La estrategia de fragmentación en RESERVAS es por rango en fechaReserva para agrupar las reservas en períodos de tiempo. Además, se recomienda pre-splitting para fechas de alta demanda (períodos vacacionales) para evitar que los shards se sobrecarguen con muchas reservas al mismo tiempo.

En HABITACIONES se define por hash en hotelId para distribuir uniformemente los hoteles entre los shards y evitar hotspots en hoteles grandes con muchas consultas de disponibilidad.

---

c.

Algunas consultas como "habitaciones disponibles en un rango de fechas" no serán tan eficientes. En grandes volúmenes de datos, es necesario configurar zonas de sharding para agrupar reservas recientes y habitaciones más demandas en los mismos shards.

---

**Problema 2. Dado el enunciado:**
**A. Definir la clave de fragmentación.
B. Definir la estrategia de fragmentación.
C. Consideraciones sobre tu propuesta de diseño.**

---

a. 

Se nos dice que existen varios casos de uso: 
- Optimizar rutas de entrega
- Priorizar pedidos en proceso
- Generar reportes de períodos de tiempo.
- Consultas frecuentes de análisis de promociones y reposición de stock.

Es necesario agrupar pedidos por distribución geográfica para facilitar el seguimiento logístico; además de distribuir dichas escrituras para evitar hotspots.

Por ende:
- PEDIDOS: {codigoPostal, mesAnio}
- PRODUCTOS: {categoriaProducto, promocionActiva}

---

b. 

La estrategia de fragmentación para los pedidos es usar intervalos para {codigoPostal, mesAnio}, con la posibilidad de implementar algo con clientId para poder hacer consultas más eficientes relacionadas con un usuario en concreto.

Por otro lado, para PRODUCTOS se debe de usar solamente {categoriaProducto}, ya que con eso se evitan los hotspots (usando promocionActiva los shards se llenaría rápidamente).

---

c. 

Las operaciones cruzadas entre PEDIDOS y PRODUCTOS no pueden compartir una clave clara debido a sus diferencias conceptuales.

---

**Problema 3. En base al enunciado previo:**
**A. Definir la clave de fragmentación.
B. Definir la estrategia de fragmentación.
C. Consideraciones sobre tu propuesta de diseño.**

---

a. 

Para PEDIDOS, se busca consultas los pedidos realizados por el cliente, además de ver el importe total de los pedidos por cliente en un período de tiempos. Es evidente que la clave de fragmentación es {clientId, fechaCreacion}.

Para PRODUCTOS, usar como clave {productId} es vital, ya que va a existir una cardinalidad muy alta y muchas consultas se van a hacer respecto a eso.

---

b. 

Para la estrategia de fragmentación; PEDIDOS seguirá una fragmentación basada en intervalos por rango de {clientId, fechaCreacion}, ya que se usa en muchísimas consultas. 

Se recomienda pre-splitting en clientes con gran volumen de pedidos o durante períodos de alta actividad. Es posible asignar zonas de sharding si se requiere, como clientes VIP o pedidos de períodos promocionales.

Por otro lado, para PRODUCTOS bastará con {productId}, siendo necesario para poder analizar las tendencias de ventas por categorías que se nos pide sin tener hotspots. Es posible tener pre-splitting para productos con alta demanda.

---

c.

Es posible que si un cliente tiene muchas compras, se genere un hotspot. 

---

**Problema 4. En base al enunciado previo:**
**A. Definir la clave de fragmentación.
B. Definir la estrategia de fragmentación.
C. Consideraciones sobre tu propuesta de diseño.

---

a. 

Para empezar, las claves de fragmentación son correctas:
- Evitan hotspots y derivados
- Organizan y optimizan la base de datos de manera correcta para las consultas
- Se hace pre-splitting para los meses de alta actividad.

b. 

Por otro lado, existen problemas derivados de este modelo:
- ¿Qué pasa si de repente hay un incremento de actividad en las compras, aumentando el tamaño de la base de datos de manera inesperada? Asumiendo que el pre-splitting no es dinámico, esto puede generar una sobrecarga inesperada. Aunque no se puede hacer nada al respecto, es recomendable tener en cuenta esto a la hora de controlar las promociones. 
- Por otro lado, no se optimizan las operaciones cruzadas en consultas (la fragmentación no incluye campos comunes entre PEDIDOS y PRODUCTOS). Esto implica que los datos estarán en shards distintos, lo que significa que MongoDB deberá de hacer consultas distribuidas. Se puede embeber parcialmente la información de productos en los pedidos.