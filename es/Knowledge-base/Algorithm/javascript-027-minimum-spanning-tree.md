---
title: [JavaScript] 027: árbol de expansión mínimo
description: 
published: true
date: 2023-02-10T05:33:08.375Z
tags: 
editor: markdown
dateCreated: 2023-02-10T05:33:06.785Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 027: Minimum Spanning Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-027-minimum-spanning-tree)
{.links-list}


# Árbol de expansión mínimo

En informática, un árbol de expansión mínimo (MST) o árbol de expansión de peso mínimo es un subconjunto de los bordes de un gráfico ponderado no dirigido que conecta todos los vértices, sin ningún ciclo y con el peso de borde total mínimo posible.

Hay muchas aplicaciones para los árboles de expansión mínimos. Por ejemplo, en una red de carreteras o líneas de comunicación, se puede utilizar un árbol de expansión mínimo para encontrar la forma más económica de conectar todos los nodos entre sí. Otro ejemplo es el análisis de conglomerados, donde se puede usar un árbol de expansión mínimo para encontrar grupos de objetos similares.

## Algoritmo de Kruskal

El algoritmo de Kruskal es un algoritmo codicioso que encuentra un árbol de expansión mínimo para un gráfico ponderado conectado. Comienza con los bordes con los pesos más pequeños y agrega bordes hasta llegar a un árbol.

El algoritmo funciona de la siguiente manera:

1. Ordene los bordes por peso de menor a mayor.

2. Comience con el borde con el menor peso. Si el borde no crea un ciclo, agréguelo al árbol.

3. Repita el paso 2 hasta que no haya más bordes para agregar.

La complejidad temporal del algoritmo de Kruskal es O(E log V), donde E es el número de aristas y V es el número de vértices.

## Algoritmo de Prim

El algoritmo de Prim es un algoritmo codicioso que encuentra un árbol de expansión mínimo para un gráfico ponderado conectado. Comienza con un vértice y agrega los bordes más baratos hasta llegar a un árbol.

El algoritmo funciona de la siguiente manera:

1. Comienza con un vértice.

2. Encuentra la arista más barata del vértice a otro vértice.

3. Agregue el borde al árbol.

4. Repita el paso 2 hasta que no haya más bordes para agregar.

La complejidad temporal del algoritmo de Prim es O(E log V), donde E es el número de aristas y V es el número de vértices.

## Ejemplo de código

La siguiente es una implementación de JavaScript del algoritmo de Kruskal.

```javascript
function kruskals(edges) {
  // sort edges by weight
  edges.sort((a, b) => a.weight - b.weight);

  // make a set for each vertex
  const sets = [];
  for (let i = 0; i < edges.length; i++) {
    sets.push(new Set([i]));
  }

  // list of edges in the MST
  const mst = [];

  // for each edge, check if it creates a cycle
  for (const edge of edges) {
    const [u, v] = edge.vertices;

    // if the edge doesn't create a cycle, add it to the MST
    if (!sets[u].has(v)) {
      mst.push(edge);

      // union the two sets
      const setU = sets[u];
      const setV = sets[v];
      for (const vertex of setV) {
        setU.add(vertex);
        sets[vertex] = setU;
      }
    }
  }

  return mst;
}
```

## Ejercicio

1. Use el algoritmo de Kruskal para encontrar el árbol de expansión mínimo para el siguiente gráfico:

    ![](https://i.imgur.com/lVqnqj7.png)

2. Use el algoritmo de Prim para encontrar el árbol de expansión mínimo para el siguiente gráfico:

    ![](https://i.imgur.com/kzFcNcu.png)

## Respuestas

1. El árbol de expansión mínimo para el gráfico se muestra a continuación. El peso total del árbol es 9.

    ![](https://i.imgur.com/zM0FtqD.png)

2. El árbol de expansión mínimo para el gráfico se muestra a continuación. El peso total del árbol es 10.

    ![](https://i.imgur.com/kzFcNcu.png)