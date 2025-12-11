---
aliases:
  - Consistencia de memoria en C++
tags:
"References":
cssclasses:
---
# Consistencia de memoria en C++

Permite la construcción de **estructuras de datos libres de cerrojos**:
- Tipos atómicos
- Mecanismos de sincronización de bajo nivel

**Objeto**: es una región de almacenamiento
**Posición de memoria**: es un objeto de un tipo escalar (aritméticos, punteros - de tamaño acotado) o una secuencia de campos de bits adyacentes (dato miembro entero con tamaño explícito en bits).

Un objeto se almacena en una o varias posiciones de memoria.

**Reglas**
- Dos hilos pueden acceder a posiciones de memoria distintas de forma simultánea
- Dos hilos pueden acceder a la misma posición de memoria de forma simultánea si ambos accesos son de lectura.
- Si dos hilos intentan acceder de forma simultánea a la misma posición de memoria y alguno de los accesos es de escritura existe una condición de carrera potencial.

## Operaciones atómicas

Son operaciones indivisibles.

- Si un hilo realiza una lectura atómica de una variable y otra una escritura atómica de la misma variable y no hay más hilos accediendo.
- Si alguna de las operaciones no es atómica el comportamiento no está definido.

El tipo genérico es `atomic<T>` permite definir variables atómicas para el tipo `T`, donde `T` es:
- Un tipo integral
- De coma flotante
- Puntero
- Boolean
- Tipos definidos por el usuario que cumplan ciertas restricciones.
Todos los atómicos tienen un miembro **is_lock_free()**: determina si está libre de cerrojos.
Además existe un tipo **atomic_flag**: el único que garantiza ser libre de cerrojos.

**atomic_flag**
- Dos estados posibles: activado o desactivado
- Siempre es libre de cerrojos.
- Inicialización por defecto o desactivado
- **Operaciones básicas**:
	- Desactivar
	- Activar y comprobar valor previo

### Implementación de spin lock (mutex ineficiente)

```cpp

class spinlock_mutex{

public:
	spinlock_mutex() = default;
	
	void lock() {
		while (f.test_and_set()) {}
	}
	
	void unlock() {
		f.clear();
	}

private:
	std::atomic_flag f;
}

```

Cerrojo que no hace uso del servicio del SO (no hay mutex). **Útil si los bloqueos van a durar muy poco tiempo y se quiere evitar problemas de cambio de contexto**.

