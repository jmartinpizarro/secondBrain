Se basa en **encontrar soluciones óptimas en un coste (temporal) polinómico**.

Una tarea de programación lineal está en forma de **CANÓNICA** sí y solo sí se dan tres condiciones:
- La *función objetivo* es de maximización
- Todas las *restricciones* son de la forma $\leq$
- Todas las *variables de decisión* (incógnitas) son no negativas: $x_1, x_2, ..., x_n \geq 0$

Dado un sistema genérico lineal tal que:
$$a_{11}x_1 + a_{12}x_2 + ... + a_{1n}x_n \leq b_1$$
$$a_{21}x_1 + a_{22}x_2 + ... + a_{2n}x_n \leq b_2$$
$$\text {. . . }$$
$$a_{m1}x_1 + a_{m2}x_2 + ... + a_{mn}x_n \leq b_m$$

Podemos simplificar su representación tal que:
$$Ax \leq b$$
$\text {A = matriz de coeficientes tecnológicos, x = vector de coeficientes de la ecuación y b = vector de recursos}$
Sabiendo que queremos **maximizar o minimizar** y que dicha ecuación tendrá cómo forma:
$$\text{max z} = C^T X$$
$C^T = \text {vector de coeficientes de la función objetivo y X = vector de coeficientes de decisión}$

>[!info]
>En la práctica, hay dos métodos para resolver estos problemas: **representación gráfica** y **método de curvas de isobeneficios o isocostes**.


>[!warning]
>Si en un ejercicio una variable de decisión acaba siendo menor que 0, ese ejercicio puntúa 0.

| NOMBRES ECUACIONES LINEALES | SIGNIFICADO            | INTERPRETACIÓN GRÁFICA               | PROGRAMACIÓN LINEAL          |
| --------------------------- | ---------------------- | ------------------------------------ | ---------------------------- |
| S. Compatible Determinado   | 1 solución             | ![[ProgL1.png]] | SOLUCIÓN ÓPTIMA ÚNICA        |
| S. Compatible Indeterminado | $\infty$ soluciones    | ![[ProgL2.png]] | SOLUCIONES ÓPTIMAS INFINITAS |
| S. Incompatible             | $\emptyset$ soluciones | ![[ProgL3.png]] | REGIÓN FACTIBLE VACÍA        |
Cuando el isobeneficio es infinito (la región no está cerrada), nos referimos a ella cómo **Región Factible No Acotada**.