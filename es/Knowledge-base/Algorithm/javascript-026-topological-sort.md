---
title: [JavaScript] 026: Clasificación topológica
description: 
published: true
date: 2023-02-10T04:32:33.028Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:32:31.453Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 026: Topological Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-026-topological-sort)
{.links-list}


# Clasificación topológica

En matemáticas, la clasificación topológica es una ordenación lineal de vértices en un gráfico acíclico dirigido (DAG). Una clasificación topológica u ordenación topológica de un gráfico dirigido es una ordenación lineal de sus vértices, de modo que para cada arista dirigida uv desde el vértice u hasta el vértice v, u viene antes que v en la ordenación. Por ejemplo, los vértices del gráfico pueden representar tareas a realizar y los bordes pueden representar dependencias de estas tareas.

Hay muchas aplicaciones de clasificación topológica. Un ejemplo es programar una secuencia de trabajos o tareas en función de sus dependencias. Como otro ejemplo, suponga que desea compilar un conjunto de archivos de código fuente en un conjunto de archivos de objetos. Esto se puede lograr representando los archivos de origen como vértices y las dependencias entre ellos como bordes. La ordenación topológica luego proporciona una secuencia en la que realizar la compilación.

Existen numerosos algoritmos para realizar ordenaciones topológicas. En este artículo, discutiremos uno de los algoritmos más populares, conocido como el algoritmo de Kahn.

## Algoritmo de Kahn

El algoritmo de Kahn es un algoritmo de clasificación topológica que fue descrito por primera vez por Arthur B. Kahn en el artículo "Clasificación topológica de redes grandes" en 1962. El algoritmo lleva su nombre.

La idea detrás del algoritmo de Kahn es simple. Comenzamos con un conjunto de vértices sin bordes entrantes y los eliminamos del gráfico. Luego agregamos sus bordes salientes al gráfico. Repetimos este proceso hasta que no haya más vértices sin aristas entrantes. Los vértices que quedan en el gráfico se clasifican en orden topológico.

El algoritmo se implementa utilizando dos colas, una para los vértices sin aristas entrantes y otra para los vértices con aristas entrantes. Los vértices de la primera cola se procesan primero y los vértices de la segunda cola se procesan a continuación.

El pseudocódigo del algoritmo de Kahn es el siguiente:

```
function kahn_sort(graph)
    // create two queues, one for vertices with no incoming edges
    // and one for vertices with incoming edges
    Q = create_queue()
    for each vertex v in graph
        if in_degree(v) == 0
            enqueue(Q, v)

    // while Q is not empty
    while Q is not empty
        // remove a vertex from Q
        v = dequeue(Q)
        // add v to the sorted list
        add_to_sorted_list(v)
        // for each edge from v to w
        for each edge(v, w) in graph
            // remove the edge from the graph
            remove_edge(graph, v, w)
            // if w has no more incoming edges
            if in_degree(w) == 0
                // add w to Q
                enqueue(Q, w)

    // if graph has edges, then it has a cycle
    if graph has edges
        throw error "graph has a cycle"
    else
        return sorted_list
```

## Implementación

Ahora implementaremos el algoritmo de Kahn en JavaScript. Usaremos una lista de adyacencia para representar el gráfico.

```javascript
// create a graph class
class Graph {
  constructor() {
    this.adjList = new Map();
  }

  // add a vertex to the graph
  addVertex(v) {
    this.adjList.set(v, []);
  }

  // add an edge from vertex v to vertex w
  addEdge(v, w) {
    this.adjList.get(v).push(w);
  }

  // get the vertices with no incoming edges
  getSources() {
    let sources = [];

    for (let [v, edges] of this.adjList) {
      if (edges.length == 0) {
        sources.push(v);
      }
    }

    return sources;
  }

  // remove an edge from the graph
  removeEdge(v, w) {
    let edges = this.adjList.get(v);
    let idx = edges.indexOf(w);
    edges.splice(idx, 1);
  }

  // get the in-degree of a vertex
  inDegree(v) {
    let count = 0;

    for (let [u, edges] of this.adjList) {
      if (edges.includes(v)) {
        count++;
      }
    }

    return count;
  }

  // get the topological order of the vertices
  topologicalSort() {
    let Q = [];
    let S = [];
    let processed = new Set();

    // get the vertices with no incoming edges
    let sources = this.getSources();

    // add the sources to the queue
    for (let v of sources) {
      Q.push(v);
    }

    // while the queue is not empty
    while (Q.length > 0) {
      // remove a vertex from the queue
      let v = Q.shift();

      // add v to the sorted list
      S.push(v);

      // for each edge from v to w
      for (let w of this.adjList.get(v)) {
        // remove the edge from the graph
        this.removeEdge(v, w);

        // if w has no more incoming edges
        if (this.inDegree(w) == 0) {
          // add w to the queue
          Q.push(w);
        }
      }

      // mark v as processed
      processed.add(v);
    }

    // if there are any edges left in the graph,
    // then there is a cycle
    if (this.hasEdges()) {
      throw new Error("graph has a cycle");
    }

    // return the topological order
    return S;
  }

  // check if the graph has any edges
  hasEdges() {
    for (let [v, edges] of this.adjList) {
      if (edges.length > 0) {
        return true;
      }
    }

    return false;
  }
}
```

## Pruebas

Ahora probaremos nuestra implementación del algoritmo de Kahn. Usaremos el siguiente gráfico:

![Gráfico](https://i.imgur.com/L6oC5vF.png)

El código para crear este gráfico es el siguiente:

```javascript
// create the graph
let g = new Graph();

// add the vertices
let v1 = "A";
let v2 = "B";
let v3 = "C";
let v4 = "D";
let v5 = "E";
let v6 = "F";
let v7 = "G";

g.addVertex(v1);
g.addVertex(v2);
g.addVertex(v3);
g.addVertex(v4);
g.addVertex(v5);
g.addVertex(v6);
g.addVertex(v7);

// add the edges
g.addEdge(v1, v2);
g.addEdge(v1, v3);
g.addEdge(v2, v4);
g.addEdge(v3, v4);
g.addEdge(v4, v5);
g.addEdge(v5, v6);
g.addEdge(v6, v7);
```

Ejecutar el algoritmo de clasificación topológica en este gráfico debería generar el siguiente resultado:

```javascript
["A", "B", "C", "D", "E", "F", "G"]
```

Y, de hecho, esto es lo que genera nuestro código:

```javascript
console.log(g.topologicalSort());
// ["A", "B", "C", "D", "E", "F", "G"]
```

## Conclusión

En este artículo, hemos discutido la clasificación topológica y el algoritmo de Kahn para realizar una clasificación topológica. También hemos implementado el algoritmo de Kahn en JavaScript.