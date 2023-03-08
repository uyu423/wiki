---
title: [JavaScript] 024: Búsqueda en amplitud
description: 
published: true
date: 2023-02-10T02:32:40.298Z
tags: 
editor: markdown
dateCreated: 2023-02-10T02:32:38.692Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 024: Breadth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/javascript-024-breadth-first-search)
{.links-list}


# JavaScript 024: Búsqueda en amplitud

En esta publicación, analizaremos la búsqueda en amplitud (BFS) y cómo implementarla en JavaScript. La búsqueda primero en amplitud es un algoritmo que se utiliza para recorrer un árbol o un gráfico. Comienza en el nodo raíz y explora todos los nodos vecinos en la profundidad actual antes de pasar a los nodos en el siguiente nivel de profundidad.

Podemos implementar BFS en JavaScript usando una cola. Una cola es una estructura de datos que nos permite almacenar datos en una forma de primero en entrar, primero en salir (FIFO). Es decir, los datos que se insertan primero en la cola son los primeros datos que se eliminan de la cola.

Podemos usar una matriz para implementar una cola. Para poner datos en cola, podemos usar el método push() de la matriz para agregar datos al final de la matriz. Para sacar datos de la cola, podemos usar el método shift() de la matriz para eliminar datos desde el principio de la matriz.

Aquí hay un ejemplo de una cola implementada usando una matriz:

```javascript
var queue = [];

// enqueue data
queue.push(1);
queue.push(2);
queue.push(3);

// dequeue data
var data = queue.shift(); // data = 1
```

Ahora que sabemos cómo implementar una cola, veamos cómo podemos usarla para implementar BFS.

## Pseudocódigo BFS

El pseudocódigo para el algoritmo BFS es el siguiente:

```
function BFS(root) {
    
    // create a queue and enqueue the root node
    var queue = [];
    queue.push(root);
    
    // while the queue is not empty
    while (queue.length > 0) {
        
        // dequeue a node from the queue
        var node = queue.shift();
        
        // if the node is not null
        if (node != null) {
            
            // process the node
            console.log(node.data);
            
            // enqueue the node's children
            queue.push(node.left);
            queue.push(node.right);
        }
    }
}
```

## Ejemplo de código BFS

Aquí hay un ejemplo de código del algoritmo BFS implementado en JavaScript:

```javascript
// Node class
function Node(data) {
    this.data = data;
    this.left = null;
    this.right = null;
}

// Binary Search Tree class
function BinarySearchTree() {
    this.root = null;
}

// insert method
BinarySearchTree.prototype.insert = function(data) {
    var newNode = new Node(data);
    
    if (this.root === null) {
        this.root = newNode;
    } else {
        this.insertNode(this.root, newNode);
    }
}

// insertNode method
BinarySearchTree.prototype.insertNode = function(node, newNode) {
    if (newNode.data < node.data) {
        if (node.left === null) {
            node.left = newNode;
        } else {
            this.insertNode(node.left, newNode);
        }
    } else {
        if (node.right === null) {
            node.right = newNode;
        } else {
            this.insertNode(node.right, newNode);
        }
    }
}

// inorderTraverse method
BinarySearchTree.prototype.inorderTraverse = function(callback) {
    this.inorderTraverseNode(this.root, callback);
}

// inorderTraverseNode method
BinarySearchTree.prototype.inorderTraverseNode = function(node, callback) {
    if (node != null) {
        this.inorderTraverseNode(node.left, callback);
        callback(node.data);
        this.inorderTraverseNode(node.right, callback);
    }
}

// BFS method
BinarySearchTree.prototype.BFS = function() {
    
    // create a queue and enqueue the root node
    var queue = [];
    queue.push(this.root);
    
    // while the queue is not empty
    while (queue.length > 0) {
        
        // dequeue a node from the queue
        var node = queue.shift();
        
        // if the node is not null
        if (node != null) {
            
            // process the node
            console.log(node.data);
            
            // enqueue the node's children
            queue.push(node.left);
            queue.push(node.right);
        }
    }
}

// test
var tree = new BinarySearchTree();
tree.insert(1);
tree.insert(2);
tree.insert(3);
tree.insert(4);
tree.insert(5);
tree.insert(6);
tree.insert(7);
tree.insert(8);
tree.insert(9);
tree.BFS(); // 1 2 3 4 5 6 7 8 9
```

## Complejidad temporal de BFS

La complejidad temporal del algoritmo BFS es O(n), donde n es el número de nodos en el árbol. Esto se debe a que el algoritmo visita cada nodo exactamente una vez.

## Complejidad del espacio BFS

La complejidad espacial del algoritmo BFS es O(n), donde n es el número de nodos en el árbol. Esto se debe a que el algoritmo almacena todos los nodos del árbol en la cola.