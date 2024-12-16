---
aliases:
  - Encaminamiento en internet. Algoritmos de encaminamiento broadcast
tags:
  - review
"References":
cssclasses:
---
# Encaminamiento en internet. Algoritmos de encaminamiento broadcast

En la práctica, los [[1731220408 - Algoritmos de encaminamiento. Estado de enlaces. Vector de distancias. Routing jerárquico|Algoritmos de encaminamiento. Estado de enlaces. Vector de distancias. Routing jerárquico]] no funcionan en un modelo escalable. Debemos de agregar routers  en regiones conocidas como *regiones autónomas*.
- Intra-AS: todos los routers dentro de la red deben de usar los mismos protocolos. Hay puertas que conectan a otras AS
- Inter-AS: las puertas se encargar de conectar las inter-AS con las Intra-AS.

Hay tablas de direccionamiento para conectar ASs usando algoritmos de encadenamiento:
- Intra-AS determina las entradas de cualquier AS
- Inter-AS e Intra-AS determina las salidas para cualquier AS

## Enrutamiento Inter-AS

Supón que en la región AS1 generamos un paquete que debe de ir a la región AS3. Debemos de buscar la manera más óptima de trasladar el paquete. Para ello podemos usar distintos protocolos:

- **RIP: Routing Information Protocol**: deprecado
- **EIGRP: Enhanced Interior Gateway Routing Protocol
- **OSPF: Open Shortest Path First**: enrutamiento de link-estado. 

## OSPF: Open Shortest Path First

Cada router tiene conocimiento total de la red, implementado el algoritmo de Dijkstra. Se usan varias métricas para ejecutar el algoritmo: retardos, ancho de banda...

Todos los mensajes del OSPF están autenticados.

### OSPF Jerárquico

Implementa dos niveles de jerarquía: el área local y la backbone. De esta manera se implementan los *routers de frontera*, reduciendo la cantidad de rutas que deben de ser almacenadas. 

## RIP: Routing Information Protocol

Incluido en las distribuciones UNIX en 1982. Ejecuta el algoritmo de vector distancia, con un máximo definido de 15 saltos.

Si no se recibe información de un vecino por 180 segundos, este se declara como muerto: todas sus vías se ven invalidadas y se avisa al resto de vecinos. 

Las tablas son manejadas por la **capa de aplicación**, donde no se paran de enviar segmentos UDP. 

## BGP: Border Gateway Protocol

Es el algoritmo por defecto de enrutamiento entre dominios, mantiene el internet conectado. Comunica las subredes que tiene a su cargo y cómo pueden acceder a ellas el resto del internet.

Tiene dos modos de ejecución:
- **eBGP**: obtiene el alcance de la sub-red de los AS vecinos
- **iBGP**: propaga el alcance de la sub-red a los AS vecinos, determinando cuales son buenas a través del propio alcance y otras políticas.

*Sesión BGP*: dos routers BGP (peer to peer) se intercambian de manera constante en una conexión TCP. De recibir un mensaje (y ser posible enviarlo), el ASx promete que enviará el mensaje y, propagando dicho mensaje a las siguientes ASs.

## Enrutamiento Broadcast

Si envíamos paquetes de todos los routers, obtenemos una red extremadamente ineficiente y colapsada.

Usamos métodos como **árbol generador**, **inundamientos** e **inundamientos controlados**. El más óptimo es el árbol generador, ya que no permite pasar mensajes a nodos de manera redundante.
***