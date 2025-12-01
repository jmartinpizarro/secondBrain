---
aliases:
  - Concurrencia en C++
tags:
"References":
cssclasses:
---
# Concurrencia en C++

## Visión general de la biblioteca

- Hilos
- Acceso a datos compartidos
- Esperas de tiempo
- Tareas asíncronas

### Hilos

Representado por objetos de tipo `std::thread` o `std::jthread` -> representado por un hilo del sistema operativo.

Dos hilos pueden acceder a un objeto compartido -> posibilidad de **carreras de datos**.

### Acceso a datos compartidos

La función `lock()` permite adquirir a la vez varios *mutex*. 
- Adquiere todos o ninguno
- Si está bloqueado libera todos.

Existe `unique_lock()`. Se liberan automáticamente cuando se sale <- estándar de C++

### Esperas de tiempo

**Acceso al reloj**
```cpp
using namespace std::chrono;
auto t1 = high_resolution_clock::now();
```

**Diferencia de tiempos**
```cpp
auto dif = duration_cast<nanoseconds>()
std::println("Dif - {}", dif);
std::println("{}", dif.count());
```

**Especificación de una espera**
```cpp
using namespace std::literals;
std::this_thread::sleep_for(500ms);
```

#### Variables de condición

Mecanismo para sincronizar hilos en acceso a recursos compartidos.
- `wait()`: espera un mutex
- `notify_one()`: despierta a un hilo en espera
- `notify_all()`: despierta a todos los hilos en espera

### Tareas asíncronas

Permite el lanzamiento simple de la ejecución de una tarea:
- En otro hilo de ejecución
- Como una tarea diferida

Un **futuro** es un objeto que permite que un hilo pueda devolver un valor a la sección de código que lo invocó.

Se usa las **promesas** para pasar un valor de un hilo a otro a través del acceso a un futuro mediante `f.get()`.

>[!NOTE]
>Si el valor esperado no se encuentra disponible cuando se necesita, se bloquea hasta que se obtiene dicho valor.


## Clase thread

La abstracción de hilo representada mediante la clase `thread` -> se corresponde uno-a-uno con los hilos del sistema operativo.

Todos los hilos de una aplicación se ejecutan en el mismo espacio de direcciones.

Cada hilo tiene su propia pila.

**Peligros**:
- Pasar un puntero o una referencia no constante a otro hilo.
- Paso de referencia a través de captura de expresiones lambda

**thread** representa un enlace a un hilo del sistema.

### Hilo vacío

Se crea un hilo sin tarea de ejecución asociada; útil en combinación con el constructor en movimiento -> **se puede mover una tarea de ejecución de un hilo a otro**.

