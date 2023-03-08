---
title: [JavaScript] 025: Búsqueda en profundidad primero
description: 
published: true
date: 2023-02-10T03:32:30.047Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:32:28.437Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 025: Depth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/javascript-025-depth-first-search)
{.links-list}


# JavaScript 025: Búsqueda en profundidad primero

En esta publicación, analizaremos la búsqueda en profundidad, un método para recorrer un gráfico. Dado un nodo inicial, la búsqueda primero en profundidad explora lo más lejos posible a lo largo de cada rama antes de retroceder.

## El Algoritmo

La estructura básica del algoritmo es la siguiente:

```
function depthFirstSearch(node) {
  // base case: if node is null, return
  if (node == null) {
    return;
  }

  // mark node as visited
  node.visited = true;

  // do something with node
  // ...

  // recurse on each of node's unvisited children
  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

Podemos ver que la función depthFirstSearch toma un nodo como entrada. Lo primero que hace es verificar si el nodo es nulo; si lo es, la función simplemente regresa. Si el nodo no es nulo, el nodo se marca como visitado y luego la función hace algo con el nodo. En nuestro caso, simplemente imprimiremos el nodo.

Después de eso, la función recorre cada uno de los hijos no visitados del nodo y recurre a ellos.

## Ejemplos de código

Aquí hay una implementación simple de la búsqueda en profundidad en JavaScript:

```javascript
function depthFirstSearch(node) {
  if (node == null) {
    return;
  }

  node.visited = true;
  console.log(node.value);

  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

Y aquí hay un ejemplo de cómo usarlo:

```javascript
// create a graph
// the graph is an array of nodes, each of which has an array of children
let graph = [
  {
    value: 1,
    children: [2, 3, 4]
  },
  {
    value: 2,
    children: [5, 6]
  },
  {
    value: 3,
    children: [7]
  },
  {
    value: 4,
    children: [8, 9]
  },
  {
    value: 5,
    children: []
  },
  {
    value: 6,
    children: []
  },
  {
    value: 7,
    children: []
  },
  {
    value: 8,
    children: []
  },
  {
    value: 9,
    children: []
  }
];

// choose a starting node
let startingNode = graph[0];

// do the search
depthFirstSearch(startingNode);
```

Ejecutar el código anterior debería imprimir lo siguiente:

```
1
2
5
6
3
7
4
8
9
```

## Ejercicios

Intente implementar usted mismo la búsqueda en profundidad con los siguientes ejercicios:

- [ ] Imprime los nodos de un gráfico en primer orden de profundidad
- [ ] Dado un gráfico y un nodo inicial, compruebe si el gráfico está conectado (es decir, se puede acceder a todos los nodos desde el nodo inicial)
- [ ] Encuentra el camino más corto de un nodo a otro en un gráfico

## Respuestas

Aquí están las respuestas a los ejercicios:

- [Imprimir los nodos de un gráfico en primer orden de profundidad](https://gist.github.com/karan/3d2e8d7feb892e7e88a44e0f4db5d1e6)
- [Dado un gráfico y un nodo inicial, compruebe si el gráfico está conectado (es decir, se puede acceder a todos los nodos desde el nodo inicial)] (https://gist.github.com/karan/aeef6efa0b43e57cdeba9120b18fb307)
- [Encuentra la ruta más corta de un nodo a otro en un gráfico](https://gist.github.com/karan/31517b2c6ef92e5231e0f8e9b7b1d094)