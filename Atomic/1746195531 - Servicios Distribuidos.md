---
aliases:
  - Servicios Distribuidos
tags:
"References":
cssclasses:
---
# Servicios Distribuidos

## Sincronización en sistemas distribuidos

Más compleja que los centralizados, ya que usan *algoritmos distribuidos* (con las siguientes propiedades):

- Información relevante se distribuye entre varios procesos en computadores distintos
- Los procesos toman las decisiones solo en base a la información local
- Debe evitarse un punto único de fallo
- **No existe un reloj común**

## Modelos síncronos y asíncronos

### Sistemas distribuidos asíncronos

- No hay reloj común
- No hacen ninguna suposición sobre las velocidades relativas de los procesos
- Canales fiables pero no existe un límite a la entrega de mensajes
- La comunicación entre procesos es la única forma de sincronización

### Sistemas síncronos

- Hay una perfecta sincronización
- Hay límites en las latencias de las comunicaciones
- Los sistemas del mundo real no son síncronos 

## Organización de tiempo en sistemas distribuidos

### Observador de eventos

Existe un observador que se encarga de visualizar los eventos (interacciones) entre dos procesos. 

>[!DANGER]
>No funciona, ya que los eventos pueden llegar desordenados.

Se propone añadir marcas de tiempos:
- En el observador: igualmente nos llegarían eventos desordenados.
- En los procesos: para ello, debería de existir un único reloj global disponible entre procesos.

### Relojes

#### Relojes físicos

Para ordenar dos eventos de un proceso basta con asignarles una marca de tiempo $MT$.

Sin embargo, dos relojes en dos computadores distintos dan dos medidas distintas: **necesidad de sincronizar los relojes físicos de un sistema distribuido**:
- Algoritmo de Cristian
- Algoritmo de Berkeley
- Network Time Protocol

#### Algoritmo de Cristian

1. El cliente realiza una petición para obtener el tiempo
2. El servidor responde con el tiempo de su reloj $T_S$.
3. El cliente actualiza su reloj a tiempo $T_S + \frac{T_F - T_I}{2}$

#### Algoritmo de Berkeley

1. El servidor de tiempo realiza un muestreo periódico de todas las máquinas para pedirles el tiempo.
2. Calcula el tiempo promedio y le indica a todas las máquinas que avancen/disminuyan su reloj a la nueva hora.

#### Network Time Protocol - NTP

Sirve para sincronizar máquinas en Internet con el UTC. Existen 3 modos de sincronización:

- *multicast*: para redes LAN de alta velocidad
- *RPC*: similar al algoritmo de Cristian
- *simétrico*: entre pares de procesos

Se usan servidores localizados con mensajes UDP.
#### Relojes lógicos

En ausencia de un reloj global fiable, la **relación causa-efecto** es la única posibilidad de ordenar eventos.

**Relación causalidad potencial**, Lamport:
1. Si dos eventos ocurren en el mismo proceso $\pi(1,..., N)$, entonces ocurrieron en el mismo orden en el que se observaron.
2. Si un proceso hace *send(m)* y otro *receive(m)*, entonces *send* se produjo antes que *receive*.
Entonces se define que: **dos eventos son concurrentes si no se puede deducir entre ellos una relación de causalidad potencial**.

#### Algoritmo de Lamport

1. Cada proceso $P$ mantiene una variable entera $RL_P$ (reloj lógico).
2. Cuando un proceso $P$ genera un evento, $RL_P = RL_P + 1$.
3. Cuando un proceso envía un mensaje $m$ a otro le añade el valor de su reloj $t$.
4. Cuando un proceso $Q$ recibe un mensaje $m$ con un valor tiempo $t$, el proceso actualiza su reloj tal que $RL_q = max(RL_q,t) + 1$
#### Relojes vectoriales

Todo proceso lleva asociado un vector de enteros $RV$.
$RV_i[a]$ es el valor del reloj vectorial del proceso $i$ cuando ejecuta el evento $a$.

1. Inicialmente $RV_i = 0; \space \forall i$
2. Cuando un proceso genera un evento: $$RV_i[i] = RV_i[i] + 1$$
3. Todos los mensajes llevan el $RV$ del envío.
4. Cuando un proceso $j$ recibe un mensaje con $RV_i$: $$RV_j = max(RV_j, RV_i)$$ $$RV_j[j] = RV_j[j] + 1$$
## Exclusión mutua distribuida

- Algoritmo centralizado
- Algoritmo distribuido
- Anillo con testigo
- Algoritmo basado en quorum

### Algoritmo centralizado

Existe un proceso coordinador. Pero este proceso **puede fallar/ser bloqueado**, bloqueando al resto de clientes. Se soluciona con:
- Uso de temporizadores
- Cerrojo se libera transcurrido cierto tiempo

### Anillo con testigo

Los procesos se ordenan conceptualmente como un anillo, donde circula un ***testigo***. Cuando un proceso quiere entrar en el anillo, debe de esperar a recoger el testigo. 

### Algoritmo de quorum

No se solicita permiso de todos los procesos, solamente del subconjunto.

### Algoritmos de elección

Útil en aplicaciones donde es necesaria la existencia de un coordinador. El algoritmo se ejecuta **cuando falla el coordinador**.

- Algoritmo del matón
- Algoritmo basado en anillo

>[!NOTE]
>La elección es única aunque el algoritmo se inicie de forma concurrente en varios procesos.

#### Algoritmo del matón

Utiliza *timeouts* $T$ para detectar fallos. Existen tres tipos de mensajes:
- coordinador: anuncio a todos los procesos con IDs menores
- elección: enviado a procesos con IDs mayores
- OK: respuesta a la elección