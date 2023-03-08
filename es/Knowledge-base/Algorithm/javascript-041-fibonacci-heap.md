---
title: [JavaScript] 041: Montón de Fibonacci
description: 
published: true
date: 2023-02-10T19:32:29.879Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:32:28.111Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 041: Fibonacci Heap***English** document is available*](/en/Knowledge-base/Algorithm/javascript-041-fibonacci-heap)
{.links-list}


# Montón de Fibonacci

En informática, un montón de Fibonacci es una estructura de datos para operaciones de cola de prioridad, que consta de una colección de árboles ordenados por montón. Tiene un mejor tiempo de ejecución amortizado que muchas otras estructuras de datos de cola de prioridad, incluido el montón binario y el montón binomial. Michael L. Fredman y Robert E. Tarjan desarrollaron montones de Fibonacci en 1984 y los publicaron en una revista científica en 1987.

Un montón de Fibonacci es una colección de árboles ordenados por montones mínimos. Cada nodo tiene un valor asociado, llamado clave. La propiedad min-heap es la siguiente: el valor de un nodo es al menos el valor de sus hijos. Es decir, la raíz del montón tiene la clave mínima.

La estructura de datos del montón de Fibonacci admite dos operaciones: insertar y extraer-min. Ambas operaciones tienen una complejidad de tiempo en el peor de los casos de O (log n).

## Ejemplos de código

### Insertar

Para insertar una nueva clave en el montón de Fibonacci, simplemente creamos un nuevo nodo con la clave y lo insertamos en la lista raíz. Este nuevo nodo se ordena automáticamente en el montón con respecto a los otros nodos en la lista raíz, por lo que no es necesario realizar más operaciones en el montón.

```javascript
function insert(key) {
    // create a new node with the given key
    var node = new Node(key);
    
    // insert the new node into the root list
    if (this.root == null) {
        this.root = node;
    } else {
        node.next = this.root;
        this.root.prev = node;
        this.root = node;
    }
    
    // update the size of the heap
    this.size++;
}
```

### Extraer-Mín.

Para extraer la clave mínima del montón de Fibonacci, simplemente eliminamos el nodo mínimo de la lista raíz y lo devolvemos. Dado que la lista raíz ahora puede estar vacía, necesitamos encontrar el nuevo nodo mínimo y convertirlo en la raíz. También necesitamos consolidar el montón vinculando por pares los árboles del mismo grado.

```javascript
function extractMin() {
    // if the heap is empty, return null
    if (this.root == null) {
        return null;
    }
    
    // remove the minimum node from the root list
    var minNode = this.root;
    if (this.root.next == this.root) {
        this.root = null;
    } else {
        this.root.prev.next = this.root.next;
        this.root.next.prev = this.root.prev;
        this.root = this.root.next;
    }
    
    // update the size of the heap
    this.size--;
    
    // if the heap is now empty, return the minimum node
    if (this.root == null) {
        return minNode;
    }
    
    // create a new array for the root list
    var roots = [];
    
    // find the new minimum node and add the other nodes to the array
    var current = this.root;
    do {
        roots.push(current);
        current = current.next;
    } while (current != this.root);
    
    // consolidate the heap by pairwise-linking the trees of the same degree
    this.consolidate(roots);
    
    // return the minimum node
    return minNode;
}
```

## Ejercicios

1. Implemente la estructura de datos del montón de Fibonacci en su lenguaje de programación favorito.

2. Utilice la estructura de datos del montón de Fibonacci para implementar una cola de prioridad.

3. Utilice la estructura de datos del montón de Fibonacci para resolver el problema de la ruta más corta en un gráfico.