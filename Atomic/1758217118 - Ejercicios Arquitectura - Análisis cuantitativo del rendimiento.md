---
aliases:
  - Ejercicios Arquitectura - Análisis cuantitativo del rendimiento
tags:
"References":
cssclasses:
---
# Ejercicios Arquitectura - Análisis cuantitativo del rendimiento

**Problema 1**. Dos partes del programa, una es del 20% y la otra del 80%. La segunda parte se puede paralelizar con multiprocesador. Suponga que la aceleración es perfecta. **Aceleración global perfecta para 10 procesadores?**.

$$S = \frac{1}{(1-F)+\frac{F}{S_n}} = \frac{1}{(1-0.8) + \frac{0.8}{10}} = 3.57$$

**Problema 3**. Tres partes del programa, una es del 25% no paralelizada, una del 50% a memoria paralelizada y otro 25% a disco. 4 núcleos.  
- Queremos cambiar los discos a unos que requieren 1/4 de entrada/salida
- Queremos sustituir a un procesador de 32 núcleos.
$$S_n = \frac{\text{Nuevo nucleo}}{\text{Previo nucle}} = \frac{32}{4} = 8$$
$$Discos = \frac{1}{0.75 + \frac{0.25}{4}} = 1.2$$
$$Procesador = \frac{1}{0.5 + \frac{0.5}{8}} = 1.7$$
Por lo tanto cambiamos el procesador.

2. Determine para que número de núcleos se obtendría la misma aceleración de con la sustitución de discos.
$$S_n = \frac{n}{4}$$
$$1.2 = \frac{1}{0.5 + \frac{0.5}{\frac{n}{4}}} = n = 6.4$$

**Ejercicio 4**. 80% CPU, 20% de eso es coma flotante (8 CPI) y el 80% son 6 CPI. El 20% son operaciones de disco.

Se valora migración a máquina que hace un 25% de CPIs más en las instrucciones pero $f' = 2f$.

*Hay que comprobar máquina 1 y máquina 2*.

Máquina 1, tiempo viejo

$$T = 0.2 \cdot CI \cdot 8 \cdot P + 0.8 \cdot CI \cdot 6 \cdot P =$$
$$T = 1.6 \cdot CI \cdot P + 4.8 \cdot CI \cdot P =$$
$$(1.6 + 4.8) \cdot CI \cdot P$$
Máquina 2, tiempo nuevo; $P = periodo$
$$T = 0.2 \cdot 8 \cdot 1.25 \cdot CI \cdot P/2 + 0.8 \cdot 6 \cdot 1.25 \cdot PI \cdot P/2 =$$
$$T = \frac{1.6 \cdot 1.25 \cdot CI \cdot P}{2} + \frac{4.8 \cdot 1.25 \cdot CI \cdot P}{2} =$$
$$4 \cdot CI \cdot P$$
Mejora final
$$S_n = \frac{T_{viejo}}{T_{nuevo}} = \frac{6.4}{4} = 1.6$$
$$S = \frac{1}{(1-f)+\frac{f}{S_n}} =$$
$$S = \frac{1}{0.2+\frac{0.8}{1.6}} = 1.42$$

**Ejercicio 5**
![[Pasted image 20250918201105.png]]

>[!NOTE]
>Al tener los cuatro cores, cada core ejecuta una cuarta parte de los $CI$, ergo
>$$CI' = CI / 4$$

$$T_{original} = (0.75 \cdot 12 + 0.25 \cdot 4) \cdot CI \cdot P = 10 \cdot CI \cdot P$$
$$T_A = \frac{(0.75 \cdot 12 \cdot 1.1 + 0.25 \cdot 4 \cdot 1.25)}{1.5} \cdot CI \cdot P = 7.43 \cdot CI \cdot P$$
$$T_B = \frac{(0.75 \cdot 12 \cdot 0.8 + 0.25 \cdot 4)}{0.5} \cdot \frac{CI}{4} \cdot P = 4.1 \cdot CI \cdot P$$

$$S_{AN} = \frac{10}{7.43} = 1.345$$
$$S_{BN} = \frac{10}{4.1} = 2.434$$

Si el speed-up local es mayor en $B$, el global será mejor si elegimos $S_{NB}$.

