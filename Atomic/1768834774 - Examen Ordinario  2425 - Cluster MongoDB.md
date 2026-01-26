---
aliases:
  - Examen Ordinario  2425 - Cluster MongoDB 
tags:
"References":
cssclasses:
---
# Examen Ordinario  2425 - Cluster MongoDB 

**Problema 1. Definir la clave de fragmentación.**

Lo único que tiene sentido para RUTAS como clave de fragmentación es {\_id}. Se podrá ordenar las rutas por identificador, reduciendo posibles hotspots en el caso de que un mismo día haya muchas rutas.

Para BILLETES, lo correcto es usar {rutaId, fechaCompra}. Al incluir rutaId como primer campo, alineamos estos documentos con la ruta correspondiente. Agrupar por rutaId optimiza las consultas por ruta e informes de ingresos. Al incluir la fecha de compra se optimizan las consultas.

Para CONDUCTORES, nos basta con {\_id}. Los datos de los conductores no están directamente en las consultas, pero mantenerlos fragmentados asegura la escalabilidad del sistema y balancea los datos entre los shards.

---

**Problema 2. Definir la estrategia de fragmentación.**

- RUTAS: la opción para usar {\_id} por hash es factible, ya que normalmente nunca hay un crecimiento de rutas exponencial o masivo. Es posible también usar las paradas para fragmentar dependiendo de la localización.
- BILLETES: {rutaId, fechaCompra}: todos los billetes de una sola ruta se encuentran relacionados; además que podemos usar rangos en las fechas de manera óptimza.
- CONDUCTORES: {\_id}

**Problema 3. Razona el diseño del cluster.**

El diseño es muy bueno. Separas RUTAS y BILLETES evita que los documentos de RUTAS crezcan descontroladamente debido al volumen de billetes. Además, se encuentran correctamente fragmentadas.

Los datos de los conductores, en una colección separada, se fragmentan y gestionan de forma independiente sin afectar las consultas principales de RUTAS y BILLETES.

