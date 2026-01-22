---
aliases:
  - Ejercicio Arquitectura de Datos - Gestión de Inventario de Bibliotecas Públicas
tags:
"References":
cssclasses:
---
# Ejercicio Arquitectura de Datos - Gestión de Inventario de Bibliotecas Públicas

**2. Diseño de agregados**

Para hacer este tipo de ejercicios, conviene distinguir el tipo de operación por caso de uso: algunas puede ser únicamente de escritura/lectura, otras combinar lectura y escritura y otras solamente de escritura.

En la implementación, la elección entre embeber o referenciar dependerá de la frecuencia de acceso y actualización, así como del tamaño y crecimiento de los datos.

- **Agregado_LibroInventario**:
	- Entidades que comprende: Libro, Inventario, Biblioteca
	- Raíz: Libro
	- Perímetro: gestiona inventario y disponibilidad de ejemplares en cada sucursal.
- **Agregado_Usuario**:
	- Entidades: Usuario, Reserva, Préstamo
	- Raíz: Usuario
	- Perímetro: abarca el historial de préstamos, reservas y penalizaciones, incluyendo la información de las multas.
- **Agregado_RecursoDigital**:
	- Entidades: RecursoDigital, PŕestamoDigital, Usuario
	- Raíz: Recurso Digital
	- Perímetro: gestiona préstamos y descargas de recursos digitales. Cada recurso puede tener múltiples préstamos registrados sin afectar la información general del usuario.