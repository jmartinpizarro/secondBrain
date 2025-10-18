---
aliases:
  - Riesgos de control
tags:
"References":
cssclasses:
---
# Riesgos de control

Se produce en una instrucción de alteración del PC.

**Terminología**:
- Bifurcación tomada: si se modifica el PC.
- Bifurcación no tomada: si no se modifica el PC.

>[!DANGER]
>La segmentación asume que la bifurcación no se tomará.

Si se toma la bifurcación -> actualización de PC al final de ID.

- Cálculo de dirección efectiva. Sumador de *ID*
- Evaluación de condición. Comparador de *ID*

## Alternativas

- **Tiempos de compilación**: prefijadas durante toda la ejecución del programa
	- El software puede intentar minimizar su impacto si conocer el comportamiento de hardware
	- El compilador puede hacer este trabajo
- **Alternativas en tiempo de ejecución**: comportamiento variable durante la ejecución del programa.
	- Intentan predecir qué hará el software.

## Soluciones estáticas

1. **Congelación del *pipeline***: si la instrucción actual es una bifurcación -> parar o eliminar del pipeline instrucciones posteriores hasta que se conozca el destino. El destino de la bifurcación se conoce en la etapa *ID*
2. **Predicción prefijada**
	1. **Siempre no tomado**: no se modifica el estado del procesador hasta que se tiene la confirmación de que la bifurcación no se toma. Si se toma, las instrucciones siguientes se retiran del pipeline y se capa la instrucción en el destino del salto.
	2. **Siempre tomado**: se empieza a calcular el destino se comienza a captar instrucciones del destino. En pipeline de 5 etapas no aporta ventajas.
3. **Bifurcación con retraso**: asumir que se va a ejecutar 1 o $n$ instrucciones después del salto posteriores a la propia instrucción de bifurcación.

En muchos casos en compilador necesita saber qué va a hacer para reducir el impacto

## Rendimiento y predicción prefijada

$$S=aceleracion=\frac{profundidad_{pipeline}}{1+frecuencia_{bifurc} \cdot penalz_{bifurc}}$$