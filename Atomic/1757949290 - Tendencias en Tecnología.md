---
aliases:
  - Tendencias en Tecnología
tags:
"References":
cssclasses:
---
# Tendencias en Tecnología

**ISA** -> Instruction Set Architecture. Juego de instrucciones para una familia de procesadores. Puede durar décadas mediante evolución.
- Necesidad de planificar para evolución a largo plazo
- Aprender de la evolución de **tecnologías críticas**: lógica de circuitos integrados, DRAM de semiconductores, flash de semiconductores, discos magnéticos y redes.

## Potencia y energía: principales aspectos

**Potencia máxima**: procesador consume más potencia de la suministrada -> caída de voltaje -> mal funcionamiento

**Potencia Térmica de Diseño (TDP - Thermal Design Power)**: 
- Consumo de potencia bajo máxima carga teórica.
- Determina los requisitos de enfriamiento
- Se puede superar durante periodos cortos de tiempo
- ¿Qué pasa si el TDP se supera por más tiempo? Se baja la tasa de reloj o apagar el chip

**Energía**: la potencia es energía por unidad de tiempo. 
$$1W = \frac{1 \space \text{Julio}}{1 \space \text{segundo}}$$

**Energía dinámica**: cantidad de energía necesaria para conmutar:
$$0 \rightarrow 1 \space \text{o} \space 1 \rightarrow 0$$
$$E_d \approx \frac{1}{2} \cdot X_c \cdot V²$$

**Potencia dinámica**: depende de la frecuencia de transmisión:
$$P_d \approx \frac{1}{2} \cdot X_C \cdot V² \cdot f$$
### Tendencias a lo largo del tiempo

- Incremento del número de transistores que conmutan
- Incremento de la frecuencia de conmutación
- **Más relevante** que el decremento en carga capacitiva y voltaje
- **Efecto neto**: crecimiento en consumo de potencia y energía.

## Eficiencia energética

1. Desactivar reloj de módulos inactivos
	1. Sin ejecución de coma flotante -> desactivar unidad FP
	2. Desactivar cores no usados.
2. Escalado dinámico de Voltaje-Frecuencia (DVFS - Dynamic Voltage-Frequency Scaling)
	1. Varias frecuencias de operación -> Ahorro de energía
3. Modos de baja potencia
	1. Requiere mecanismo de reactivación
4. *Overclocking* automático
	1. Activado cuando es seguro
	2. *Ejemplo: procesador de 3.3 GHz a 3.6 GHz en ráfagas* (midiendo temperaturas)

## Efecto de potencia estática

La corriente fluye incluso si el transistor está apagado.
$$P_{estatica} \approx corriente_{estatica} \cdot Voltaje$$

La potencia estática es proporcional al número de dispositivos:
- Creciente número de transistores -> incremento de potencia.
- **Limitación de potencia**:  apagar el suministro de potencia a módulos inactivos. 

## Fiabilidad y Disponibilidad

### Fiabilidad

Probabilidad de que un dispositivo funcione adecuadamente durante un periodo dado de tiempo bajo condiciones de operación específicas. 

Distribuciones usadas para fiabilidad:
- **Exponencial**: si la tasa de errores es constante la fiabilidad sigue una distribución exponencial
- **Weibull**: la tasa de fallos es proporcional a una potencia de tiempo.

#### Sistemas Serie

Sea $R_i(t)$ la fiabilidad del componente $i$. El sistema falla cuando algún componente falla.
$$R(t) = \prod_{i=1}^{N} R_i(t)$$
#### Sistemas en paralelo

El sistema falla cuando todos los componentes fallan:
$$R(t) = 1 - R_i(t)$$

### Disponibilidad

La disponibilidad de un sistema $A(t)$ se define como la probabilidad de que el sistema esté funcionando correctamente en el instante $t$. 
- La fiabilidad considera el intervalo $[0, t]$.

- **FIT**: Failures In Time. Fallos en un periodo, expresado en $10⁹$ horas.
- **MTTF**: Mean Time to Failure. Tiempo medio hasta fallo.
- **MTTR**. Mean Time to Repair. Tiempo medio de reparación.
$$A = \frac{MTTF}{MTTF + MTTR}$$
$$FIT = \frac{10⁹}{MTTF}$$
