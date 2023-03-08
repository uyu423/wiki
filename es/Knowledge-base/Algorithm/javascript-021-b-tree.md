---
title: [JavaScript] 021: Árbol B
description: 
published: true
date: 2023-02-09T23:32:52.868Z
tags: 
editor: markdown
dateCreated: 2023-02-09T23:32:51.277Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 021: B-Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-021-b-tree)
{.links-list}


# JavaScript 021: Árbol B

Un árbol B es una estructura de datos de árbol autoequilibrada que mantiene datos ordenados y permite búsquedas, inserciones y eliminaciones en tiempo logarítmico. El árbol B es una generalización de un árbol de búsqueda binario en el que un nodo puede tener más de dos hijos.

## Concepto

Un árbol B es una estructura de datos de árbol que mantiene los datos ordenados y permite búsquedas, inserciones y eliminaciones en tiempo logarítmico. Un árbol B es una generalización de un árbol de búsqueda binario en el que un nodo puede tener más de dos hijos. La ventaja de un árbol B sobre un árbol de búsqueda binario es que requiere menos accesos al disco para operaciones como la inserción y la eliminación.

Un árbol B de orden m es un árbol en el que cada nodo tiene como máximo m hijos. El nodo raíz tiene al menos dos hijos. Un árbol B está equilibrado si la diferencia en el número de hijos de dos nodos cualesquiera es como máximo 1.

La altura de un árbol B es el número de niveles en el árbol. La altura de un árbol es la longitud del camino más largo desde la raíz hasta una hoja.

Un árbol B de orden m puede tener una altura máxima de m.

## Ejemplos de código

Aquí hay una implementación simple de un árbol B en JavaScript.

```javascript
class Node {
  constructor(keys, children) {
    this.keys = keys;
    this.children = children;
  }
}

class BTree {
  constructor(order) {
    this.order = order;
    this.root = null;
  }
  
  insert(key) {
    if (this.root === null) {
      this.root = new Node([key], []);
    } else {
      this._insert(key, this.root);
    }
  }
  
  _insert(key, node) {
    if (node.keys.length < this.order - 1) {
      this._insertKey(key, node);
    } else {
      const medianIndex = Math.floor((this.order - 1) / 2);
      const median = node.keys[medianIndex];
      const leftKeys = node.keys.slice(0, medianIndex);
      const rightKeys = node.keys.slice(medianIndex + 1);
      const leftChildren = node.children.slice(0, medianIndex + 1);
      const rightChildren = node.children.slice(medianIndex + 1);
      const newNode = new Node([median], [
        new Node(leftKeys, leftChildren),
        new Node(rightKeys, rightChildren)
      ]);
      if (key < median) {
        this._insert(key, newNode.children[0]);
      } else {
        this._insert(key, newNode.children[1]);
      }
      this.root = newNode;
    }
  }
  
  _insertKey(key, node) {
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    node.keys = [
      ...node.keys.slice(0, i),
      key,
      ...node.keys.slice(i)
    ];
    node.children = [
      ...node.children.slice(0, i + 1),
      new Node([], []),
      ...node.children.slice(i + 1)
    ];
  }
  
  search(key) {
    return this._search(key, this.root);
  }
  
  _search(key, node) {
    if (node === null) {
      return false;
    }
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    if (i < node.keys.length && key === node.keys[i]) {
      return true;
    }
    return this._search(key, node.children[i]);
  }
}
```

## Ejercicios

1. Implemente la operación de eliminación para un árbol B.

2. Implemente la operación de búsqueda de rango para un árbol B. La búsqueda de rango debe tomar dos claves, un límite inferior y un límite superior, y devolver todas las claves del árbol que se encuentran entre los dos límites.

## Respuestas

1.

```javascript
class BTree {
  delete(key) {
    if (this.root === null) {
      return;
    }
    this._delete(key, this.root);
  }
  
  _delete(key, node) {
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    if (i < node.keys.length && key === node.keys[i]) {
      if (node.children[i].keys.length >= this.order) {
        const predecessor = this._getPredecessor(node.children[i]);
        node.keys[i] = predecessor;
        this._delete(predecessor, node.children[i]);
      } else if (node.children[i + 1].keys.length >= this.order) {
        const successor = this._getSuccessor(node.children[i + 1]);
        node.keys[i] = successor;
        this._delete(successor, node.children[i + 1]);
      } else {
        this._merge(node, i);
        this._delete(key, node.children[i]);
      }
    } else {
      this._delete(key, node.children[i]);
    }
  }
  
  _getPredecessor(node) {
    let current = node;
    while (current.children.length !== 0) {
      current = current.children[current.children.length - 1];
    }
    return current.keys[current.keys.length - 1];
  }
  
  _getSuccessor(node) {
    let current = node;
    while (current.children.length !== 0) {
      current = current.children[0];
    }
    return current.keys[0];
  }
  
  _merge(node, i) {
    const left = node.children[i];
    const right = node.children[i + 1];
    const key = node.keys[i];
    left.keys = [...left.keys, key, ...right.keys];
    left.children = [...left.children, ...right.children];
    node.keys = node.keys.filter((k, index) => index !== i);
    node.children = node.children.filter((child, index) => index !== i + 1);
  }
}
```

2.

```javascript
class BTree {
  rangeSearch(lowerBound, upperBound) {
    if (this.root === null) {
      return [];
    }
    return this._rangeSearch(lowerBound, upperBound, this.root);
  }
  
  _rangeSearch(lowerBound, upperBound, node) {
    let i = 0;
    while (i < node.keys.length && lowerBound > node.keys[i]) {
      i++;
    }
    let results = [];
    while (i < node.keys.length && upperBound >= node.keys[i]) {
      if (node.children.length === 0) {
        results.push(node.keys[i]);
      } else {
        results = [...results, ...this._rangeSearch(lowerBound, upperBound, node.children[i])];
      }
      i++;
    }
    if (node.children.length > 0) {
      results = [...results, ...this._rangeSearch(lowerBound, upperBound, node.children[i])];
    }
    return results;
  }
}
```