---
title: [JavaScript] 016: Lista doblemente enlazada
description: 
published: true
date: 2023-02-09T18:32:31.893Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:32:30.293Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 016: Doubly Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-016-doubly-linked-list)
{.links-list}


# JavaScript 016: Lista doblemente enlazada

Una lista doblemente enlazada es una estructura de datos que consta de un conjunto de nodos secuenciales enlazados entre sí de manera que cada nodo contiene una referencia al nodo anterior así como al siguiente nodo. Este tipo de lista enlazada es ventajoso sobre una lista enlazada simple porque permite el recorrido en ambas direcciones.

Un nodo de lista doblemente enlazado típico contiene tres campos:

- **anterior**: Una referencia al nodo anterior en la lista
- **siguiente**: Una referencia al siguiente nodo en la lista
- **datos**: Los datos almacenados en el nodo

El primer nodo en una lista doblemente enlazada normalmente se denomina nodo **principal** y el último nodo normalmente se denomina nodo **cola**. El nodo principal y el nodo final tienen propiedades especiales en las que el campo anterior del nodo principal es nulo y el siguiente campo del nodo final es nulo.

Aquí hay una ilustración de una lista doblemente enlazada con cuatro nodos:

![Lista de enlaces dobles](https://i.imgur.com/eLzWqlN.png)

Y aquí está el código para un nodo de lista doblemente enlazado básico en JavaScript:

```javascript
function Node(data) {
  this.prev = null;
  this.next = null;
  this.data = data;
}
```

Para insertar un nuevo nodo en una lista doblemente enlazada, primero debemos encontrar el nodo en el que queremos insertar el nuevo nodo después. Una vez que hayamos encontrado ese nodo, podemos configurar el siguiente campo del nuevo nodo para que apunte al nodo que encontramos, y podemos configurar el campo anterior del nodo encontrado para que apunte al nuevo nodo. Finalmente, podemos configurar el campo anterior del nuevo nodo para que apunte al nodo encontrado.

Aquí hay una ilustración de cómo se ve este proceso de inserción:

![Inserción en una lista doblemente enlazada](https://i.imgur.com/TGiukgD.png)

Y aquí está el código para este proceso de inserción:

```javascript
function insertAfter(node, newNode) {
  newNode.next = node.next;
  node.next = newNode;
  newNode.prev = node;
}
```

Para eliminar un nodo de una lista doblemente enlazada, primero debemos encontrar el nodo que queremos eliminar. Una vez que hemos encontrado el nodo, podemos configurar el campo anterior del siguiente campo del nodo para que apunte al campo anterior del nodo, y podemos configurar el siguiente campo del campo anterior del nodo para que apunte al siguiente campo del nodo. Finalmente, podemos establecer el campo anterior y el campo siguiente del nodo en nulo.

Aquí hay una ilustración de cómo se ve este proceso de eliminación:

![Eliminación de una lista doblemente enlazada](https://i.imgur.com/FgxLbNv.png)

Y aquí está el código para este proceso de eliminación:

```javascript
function deleteNode(node) {
  node.prev.next = node.next;
  node.next.prev = node.prev;
  node.prev = null;
  node.next = null;
}
```

¡Eso es todo al respecto! Una lista doblemente enlazada es una estructura de datos simple pero poderosa que se puede usar en una variedad de aplicaciones.