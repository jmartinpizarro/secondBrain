---
aliases:
  - Programación lineal entera
tags:
  - review
  - programacionLineal
References: 
cssclasses:
---
# Programación lineal entera

Dadas unas restricciones de integridad (las variables deben de $\in N$), el problema deja de ser polinómicamente complejo y se convierte en exponencialmente complejo. Lo que debemos hacer es **ramificar**.

Tomaremos los números enteros más próximos a nuestras variables $x_i$, haremos dos franjas en nuestra *región factible*. La franja que consta entre los dos enteros, conformada por *infinitos números decimales*,  no estamos eliminando ninguna solución.

$$F \supset F_1 \cup F_2$$
Entonces $z_F \leq z_{\text{F}_1}$. Para resolver este problema usaremos el algoritmo de *ramificación y acotación en profundidad*.

## Ramificación y acotación en profundidad

1. Resolvemos el problema relajado (rezamos porque la solución $\in N$). Si $x^* \in N, \text{HALT}$
2. Ramificar sobre una variable creando dos regiones: $F \supset F_1 \cup F_2$. *¿Qué variable debemos elegir?* Aquella que no sea entera.
3. Calcular $z_{\text{F}_1}$ y $z_{\text{F}_2}$. Nodos terminales:
	1. $F_i \neq 0$
	2. $x_{\text{F}_i} \in N$ , si este valor es el más grande (maximizar) que hemos encontrado, nos lo guardamos $z_{\text{F}_i} > B$. Eso es un nodo terminal
	3. Si $z_{\text{F}_i} \leq Nodo Terminal$
***