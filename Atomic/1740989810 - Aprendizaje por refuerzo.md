---
aliases:
  - Aprendizaje por refuerzo
tags:
  - review
"References":
cssclasses:
---
# Aprendizaje por refuerzo

El agente tiene que aprender un modelo (*policy*) o estrategia $\pi$ para saber qué acción tomar en cada situación $S$.

El agente aprende la estrategia a través de la exploración y el ensayo y error. 

No puede ser un problema supervisado, ya que sería costoso crear una tabla con $\pi$ para cada situación.

## Propiedad de Markov

La política $\pi$ sólo va a depender del estado presente.
$$\pi(s_t) = a_t$$
Los estados $s$ deben de contener toda la información necesaria para que la probabilidad de pasar a otro estado $s'$ sea independiente de la manera en la que se ha llegado a $s$, para forzar la propiedad de Markov.

### Proceso de decisión de Markov - MDP

Un MDP se define como una tupla tal que:
$$<S, A, T, R, \gamma>$$
donde:
- $S$ es un conjunto de estados discretos
- $A$ es un conjunto de acciones discretas
- $T: S \times A \rightarrow P(S)$. Donde un miembro de $P(S)$ es una distribución de la probabilidad sobre un conjunto $S$, es decir, transforma estados en probabilidades. Se dice que: $T(s, a, s')$ es la probabilidad de que se realice una acción en un estado para llegar a una estado nuevo.
- $R: S \times A \rightarrow \mathbb{R}$, que para cada estado-acción proporciona un refuerzo (valor real). Se dice que $R(s,a,s')$ es el refuerzo recibido tras ejecutar la acción $a$ desde el estado $s$ para llegar a $s'$.
- $\gamma$ es el **factor de descuento**. Su rango es $[0, 1]$. El agente usa el factor de descuento para ajustar la importancia de las recompensas a lo largo del tiempo. Una forma es decirle al agente que busque obtener la recompensa más positiva cuanto antes.

## Retorno con descuento

Denotado como $G_t$, en el tiempo $t$, estando en el estado $s_t$, después de realizar la acción $a_t$, se calcula como:
$$G_t = r_{t+1} + \gamma \cdot r_{t+2} + \gamma^2 \cdot r_{t+3} + \gamma^3 \cdot r_{t+4} + \text{...} = \sum_{k=t+1}^T \gamma^{k-t-1} \cdot r_k$$
Si:
- $\gamma = 1$ tendremos la suma de todas las recompensas
- $\gamma = 0$ tendremos la recompensa inmediata

Un agente da importancia a recompensas inmediatas y futuras dependiendo de tareas. En algunas tareas, las recompensas futuras priman sobre las recompensas inmediatas. 

## Objetivo

Buscamos encontrar la **política máxima $\pi^*$**, es decir, queremos maximizar la recompensa máxima en un estado $S_t$ al realizar una acción $a$.

**Política $\pi$**
Define el comportamiento del agente en el entorno. Existen dos tipos:
- Determinista: el agente realiza una acción determinada si se encuentra en un estado en concreto
- Estocástica: la elección de la acción a realizar se basa en una tabla de probabilidades.

La política puede ir cambiando a medida que el agente adquiera más experiencia con el proceso.

$\pi(a | s)$: probabilidad de usar la acción $a$ en un estado $s$.
$$\sum_a \pi(a|s) = 1$$
## Ecuación de Bellman

Nos permite calcular el valor de un estado $s$ asumiendo que tenemos constancia de los valores de otros estados $s'$.
$$V(S_t) = r_{t+1} + \gamma \cdot V(S_{t+1})$$

## Ventajas e inconvenientes del método clásico

**Ventajas**
- Resuelve el problema de forma óptima.

**Inconvenientes**
- Necesita observabilidad completa del estado.
- Muy costoso computacionalmente.
- Se necesita conocimiento del modelo.

## Otros métodos

**Método de MonteCarlo**
- **Métodos basados en el modelo.**
	- Se conoce la dinámica del entorno. 
	- Aplicamos algoritmos de programación dinámica.
- **Métodos libre de modelo.**
	- No necesita conocer la dinámica del entorno, se estima a partir de la experiencia.
	- Aprende a partir de episodios. 

Es posible que siguiendo alguna política, no se visiten nodos que serían esenciales para la obtención de una solución final. 
- Usar políticas estocásticas o*greedy*
- Generar varias búsquedas iniciales dependiendo de los posibles nodos (búsqueda paralela).

Se basa en exploración y explotación.