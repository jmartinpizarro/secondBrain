---
aliases:
  - Examen Ordinario 2025 - MongoDB
tags:
"References":
cssclasses:
---
# Examen Ordinario 2025 - MongoDB

Una aplicación tipo marketplace de compraventa (similar a Wallapop) gestiona usuarios, anuncios, favoritos, chats, mensajes y fotos de anuncios.
Los casos de uso principales son:
	A. Detalle de anuncio. En la vista Detalle de anuncio se muestran los datos del anuncio, sus fotos, la información básica del vendedor y el número de veces que ha sido marcado como favorito.
	B. Chat. En la funcionalidad de Chat, un usuario puede:
		1. ver la lista de sus conversaciones activas (interlocutor, anuncio asociado, último
		mensaje y fecha de última actividad), y
		2. acceder a los mensajes de una conversación de forma paginada.
Considera las siguientes restricciones:
	• Un anuncio puede tener hasta 10 fotos.
	• Un anuncio puede acumular decenas de miles de favoritos.
	• Un chat puede acumular decenas de miles de mensajes, con inserciones frecuentes.
	• En el listado de conversaciones no se deben cargar todos los mensajes, sino solo información
	resumida.
	• Se deben evitar documentos que crezcan sin límite y actualizaciones masivas de documentos
muy grandes.

**APARTADO 1. (1,5 p)**
Diseña el modelo de datos en MongoDB centrándote en la definición de agregados. Identifica los agregados que consideres necesarios, indicando para cada uno:
	• la raíz del agregado,
	• su perímetro,
	• qué información se embebe y cuál se referencia,
y justifica las decisiones adoptadas en función de los casos de uso y las restricciones.

**APARTADO 2. (1 p)**
En base a tu diseño de modelo de datos (apartado 1), propón un diseño de fragmentación para la distribución de datos en un clúster, para ello:
A. Define la clave de fragmentación y por qué es adecuada.
B. Define la estrategia de fragmentación y justifícala.

---

**Apartado 1**

Un agregado es un objeto que se introduce en una colección. Por el momento, no nos importa definir la colección, solamente los agregados.

a. **AGREGADO_ANUNCIO**: que contiene la información como los datos del anuncio, las fotos (límite de 10), información básica del vendedor (embebida, puesto que es un resumen de unos datos más extensos así que no nos hace mucho daño) y el número de veces que ha sido marcado como favorito (referenciado, puede modificarse muchas veces). La raíz del agregado es ANUNCIO.
b. **AGREGADO_CONVERSACIÓN**: contiene información como el interlocutor y el receptor (asumiendo que es el resumen del vendedor y del otro usuario, podría hacerse referenciado), el anuncio asociado debe ir referenciado, con el último mensaje y fecha de última actividad (embebidos, se modificarán continuamente). La raíz es 
c. **AGREGADO_MENSAJE**: contiene información del mensaje (como unidad), por lo que contiene el usuario, la date y timestamp en la que se envió, además de un identificador numérico que marca la conversación a la que pertenece. 

---

**Apartado 2**

- **Mensajes**: sí que nos interesa fragmentar, ya que podemos tener colecciones con cientos de GB o TB, no va a caber correctamente en una sola máquina. La clave de fragmentación está compuesta por  `{conversationId, createdAt}`. Nos permite agrupar mensajes por conversación y createdAt para paginación/ordenación. $\exists$ riesgo de *hotspot* si hay muchas escrituras para una conversación si se generan muchas escrituras.
- **Conversaciones**: opcional fragmentar, `{conversationId}`. Hash para distribución uniforme. Puede requerir alta eficiencia para consultas donde se quieren cargar todos los chats de un único usuario.
- **Anuncios**: se usa un hash `{selledId}` para repartir la carga entre los nodos, aunque solo si hay muchísimo volumen. De no haberlo, se podría usar replicación y no fragmentación.
