---
aliases:
  - Máquinas de vectores de soporte - SVMs
tags:
"References":
cssclasses:
---
# Máquinas de vectores de soporte - SVMs

Establecen fronteras entre las distintas clases en el espacio de instancias. Basadas en funciones matemáticas, generan una especie de hiperplanos. ¿Qué hiperplano es el mejor?
**Aquel con mayor margen**.

![[Pasted image 20250330195714.png]]

Las SVMs construyen el hiperplano de separación, de manera que ocupe la posición donde el margen entre las dos clases es máximo. Eso da lugar a la frontera con **mejor capacidad de generalización.**

Las instancias $x_i$ en los límites de los márgenes se consideran **vectores de soporte**.

Este problema de optimización se puede resolver eficientemente mediante programación cuadrática.

Existen varios tipos de máquina:
- Modelo lineal:
	- Datos son separables linealmente: hard margin
	- Datos no son separables linealmente: soft margin
- Modelo no lineal 

### Soft Margin

Si las clases se solapan, **pueden existir instancias inclasificables linealmente**. Esto se arregla permitiendo que haya variables de holgura que no se puedan clasificar.

![[Captura de pantalla 2025-03-30 a las 20.00.42.png]]

Para ello, se añade un parámetro $C$ que controla el peso que le demos a un objetivo u a otro, permitiendo controlar el overfitting.

### SVMs no lineales

Las Máquinas de Vectores de Soporte (SVMs) no lineales son una extensión del algoritmo SVM que permite clasificar datos que no son linealmente separables. En lugar de buscar un hiperplano lineal, las SVMs no lineales utilizan funciones kernel para mapear los datos a un espacio de mayor dimensión donde pueden ser separados linealmente.

**Funciones Kernel**

Las funciones kernel son funciones que calculan el producto punto entre dos vectores en el espacio de características sin tener que calcular explícitamente la transformación de los datos. Algunas funciones kernel comunes incluyen:

- **Kernel Polinómico**: Permite crear límites de decisión no lineales de grado d.
- **Kernel Gaussiano (RBF)**: Crea límites de decisión no lineales que pueden ser muy complejos.
- **Kernel Sigmoide**: Similar a una red neuronal de una sola capa.

**Ventajas de las SVMs No Lineales**

- Pueden clasificar datos que no son linealmente separables.
- Son robustas al sobreajuste.
- Funcionan bien con datos de alta dimensión.

**Desventajas de las SVMs No Lineales**

- Pueden ser computacionalmente costosas.
- La elección de la función kernel y los hiperparámetros puede ser difícil.

**Aplicaciones de las SVMs No Lineales**

Las SVMs no lineales se utilizan en una amplia variedad de aplicaciones, incluyendo:

- Reconocimiento de imágenes
- Reconocimiento de voz
- Bioinformática
- Procesamiento del lenguaje natural