---
aliases:
  - Modelo orientado a grafos
tags:
"References":
cssclasses:
---
# Modelo orientado a grafos

El model de grafo utiliza **estructuras de grafo** para representar y almacenar los datos.
- Nodos: representan datos del dominio real
- Aristas: representan relaciones entre los datos

Datos altamente relacionados, **es útil cuando las interrelaciones de los datos son importantes** (pocos nodos, muchas aristas).

- Grafos etiquetados: se aporta semántica añadiendo metadatos a los nodos y aristas
- Grafos de propiedad etiquetados: permite asignar propiedades a otros nodos

Especialmente bueno en consultas. Difícilmente escalables. Lenguajes de alto nivel y **restricciones del modelo**:
- No se permiten aristas sin nodo origen/destino.
- Los nodos solo pueden eliminarse cuando quedan huérfanos.