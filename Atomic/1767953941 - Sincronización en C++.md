---
aliases:
  - Sincronización en C++
tags:
"References":
cssclasses:
---
# Sincronización en C++

## Primitivas hardware

$\exists$ la necesidad de fijar un orden global en las operaciones. El modelo de consistencia puede ser insuficiente y complejo; se suele complementar con operaciones de lectura-modificación-escritura.

### Test-and-test

Secuencia atómica:

1. Lee posición de memoria en registro (se devolverá como resultado).
2. Escribe el valor 1 en la posición de memoria.

### Intercambio - swap

Secuencia atómica:

1. Intercambia los contenidos de una posición de memoria y un registro.
2. Incluye una lectura de memoria y una escritura de memoria.

### Captación y operación - fetch-and-op

Instrucción de captar y operar. Diversas operaciones: *fetch-add*, *fetch-or*, *fetch-inc*...

Secuencia atómica:
1. Lee posición de memoria en registro (devuelve este valor).
2. Escribe en posición de memoria el resultado de aplicar al valor original una operación.

### Comparar e intercambiar - compare-and-swap

Operación sobre dos variables locales y una posición de memoria.

1. Lee el valor $x$
2. Si $x$ es igual a registro $a$ -> intercambia $x$ y registro $b$

### Almacenamiento condicional - Load Linked/Store Conditional

Par de instrucciones LL/SC (Load Linked/Store Conditional).

**Funcionamiento**:
1. Si el contenido de una variable leída mediante LL se modifica antes de un SC el almacenamiento no se lleva a cabo.
2. Si entre LL y SC ocurre cambio de contexto, SC no se lleva a cabo.
3. SC devuelve un código de éxito/fracaso.

## Cerrojos

Un cerrojo es un mecanismo que asegura la exclusión mutua.

**Dos funciones de sincronización**:
- *Lock(k)*:
	- Adquiere el cerrojo.
	- Si varios intentan adquirir el cerrojo, `n-1` pasan a espera.
	- Si lleguen más procesos, pasan a espera.
- *Unlock(k)*:
	- Libera el cerrojo.
	- Permite que uno de los procesos en espera adquiera el cerrojo.

**Mecanismos de espera:**
Existen dos: 

**Espera activa**:
- El proceso queda en bucle que constantemente consulta valor de variable de control de espera (*spinlock*).

**Bloqueo**
- El proceso queda suspendido y cede el procesador a otro proceso.
- Si un proceso ejecuta *unlock* y hay procesos bloqueados se libera a uno de ellos.
- Requiere soporte de un planificador.

**Componentes**
Tres elementos de diseño:
- Método de adquisición: usado para intentar adquirir el cerrojo
- Método de espera: mecanismo para esperar hasta que se pueda adquirir el cerrojo
- Método de liberación: mecanismo para liberar uno o varios procesos en espera.

### Cerrojos simples

Variable compartida $k$ con dos valores:
$$k = \begin{cases} 1 \rightarrow \text{abierto} \\ 0 \rightarrow \text{cerrado} \end{cases}$$
*Lock(k)*
- Si $k=1$ -> espera activa mientras $k=1$
- Si $k=0$ -> $k=1$
- No se debe permitir que 2 procesos adquieran cerrojo simultáneamente.

```cpp
// Test and Set
void lock(atomic_flag & k) {
	while (k.test_and_set()) {}
}

void unlock(atomic_flag &k) {
	k.clear();
}

// Fetch and op
void lock(atomic<int> &k) {
	while (k.fetch_or(1) == 1) {}
}

void unlock(atomic<int> &k) {
	k.store(0);
}
```
```assembly
// swap
do_lock: mov eax, 1
repeat: xchg eax, _k
		cmp eax, 1
		j ¡z repeat
```

### Retardo exponencial

Objetivo:
- Reducir accesos a memoria.
- Limitar consumo de energía.

```cpp
void lock(atomic_flag &k) {
	while (k.test_and_set()) {
		perform_pause(delay);
		delay *= 2;
	}
}
```

Se incrementa exponencialmente tiempo entre invocaciones a *test_and_set()*.

### Sincronización y modificación

Se pueden mejorar prestaciones si se usa la misma variable para sincronizar y comunicar. Se evita usar variables compartidas solamente para sincronizar.

```cpp
double parcial = 0;
for (int i = iproc; i < max; i += nproc) {
	parcial += v[i];
}
suma.fetch_add(parcial);
```


>[!DANGER]
>- Implementaciones simples no fijan orden de adquisición de cerrojo.
>- Se podría dar inanición.
>**Solución** cerrojos con etiquetas

**Cerrojos con etiquetas**: dos contadores, de adquisición (número de procesos que han solicitado el cerrojo) y de liberación (número de veces que se ha liberado el cerrojo). La etiqueta -> valor de contador de adquisición.

También existen cerrojos basados en colas para mantener procesos que esperan para entrar en sección crítica.

## Barreras

Permite sincronizar varios procesos en algún punto.
- Garantiza que ningún proceso supera la barrera hasta que todos han llegado
- Usadas para sincronizar fases de un programa

### Barreras centralizadas

Contador centralizado asociado a la barrera; cuenta el número de procesos que han llegado a la barrera.

La barrera incrementa el contador, espera a que el contador llegue al número de procesos a sincronizar.

```cpp
// implementacion simple
do_barrier(barrera, n) {
	lock(carrera.cerrojo);
	
	if (barrera.contador == 0) {
		barrera.flag = 0;
	}
	
	contador_local = barrera.contador++;
	unlock(barrera.cerrojo);
	
	if (contador_local == np) {
		barrera.contador = 0;
		barrera.flag = 1;
	}
	
	else {
		while (barrera.flag == 0) {}
	}
}

// barrera inversion de sentido
do_barrera(barrera, n) {
	flag_local = !flag_local;
	
	lock(barrera.cerrojo);
	contador_local = barrera.contador++;
	unlock(barrera.cerrojo);
	
	if (contador_local == np) {
		barrera.contador = 0;
		barrera.flag = flag_local;
	}
	else {
		while (barrera.flag == flag_local) {}
	}
}
```

También existen barreras en árboles, ya que la implementación simple de barreras no es escalable.