---
aliases:
  - Hierarchical Clusterization
tags:
"References":
cssclasses:
---
# Hierarchical Clusterization

Basados en dendrogramas, realizando una búsqueda aglomerativa hacia arriba. Esto quiere decir que generamos un árbol desde las hojas, comparando la similitud de las instancias.

## Algoritmo

1. *Calcular* la matriz de distancias entre las parejas de instancias.
2. *Formar* un nuevo cluster con los dos clusters (inicialmente instancias individuales) más cercanos.
3. *Sustituir* los dos clústers por el nuevo cluster y *actualizar* la matriz de distancias.
4. Repetir (1) hasta que solo quede un clúster (nodo raíz).

>[!NOTE]
>No solo se generan grupos, sino además una jerarquía entre ellos con una medida de distancia.

Para calcular la distancia existen muchas formas:
- min()
- max()
- Media
- Distancia entre centroides
- Método de Ward (función objetivo): minimiza la varianza total de las agrupaciones y es mucho más robusto al ruido.

La principal **desventaja** de este método es la alta complejidad temporal $O(n^3)$, lo que hace que para grandes datasets sea totalmente impracticable. Otra desventaja importante es  la sensibilidad a los datos anómalos y al ruido.

>[!NOTE]
>Detectar saltos grandes entre las alturas la fusión indica que se están fusionando clusters que están muy lejos entre ellos. En este momento se puede detener el algoritmo.



