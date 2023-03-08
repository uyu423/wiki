---
title: [JavaScript] 008: Lista vinculada
description: 
published: true
date: 2023-02-09T10:32:30.599Z
tags: 
editor: markdown
dateCreated: 2023-02-09T10:32:28.926Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 008: Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-008-linked-list)
{.links-list}


# JavaScript 008: Lista enlazada

Una lista enlazada es una estructura de datos que consta de un conjunto de nodos donde cada nodo contiene una referencia al siguiente nodo de la lista. Este tipo de lista es muy eficaz para operaciones como la inserción y la eliminación, ya que no es necesario reorganizar la lista.

Hay dos tipos de listas enlazadas:

- Lista enlazada simple: Cada nodo tiene una referencia al siguiente nodo.
- Lista doblemente enlazada: Cada nodo tiene una referencia al nodo siguiente y al nodo anterior.

En esta publicación, implementaremos una lista de enlaces únicos en JavaScript.

## Crear un nodo

Lo primero que debemos hacer es crear una clase de nodo. Cada nodo tendrá dos propiedades:

- `data`: Los datos que contendrá el nodo.
- `siguiente`: Una referencia al siguiente nodo en la lista.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

## Creación de una lista vinculada

Ahora que tenemos una clase de nodo, podemos crear una clase de lista enlazada. Esta clase tendrá dos propiedades:

- `head`: una referencia al primer nodo de la lista.
- `tail`: Una referencia al último nodo de la lista.

La clase de lista enlazada también tendrá algunos métodos:

- `append(data)`: Agrega un nuevo nodo con los datos dados al final de la lista.
- `prepend(data)`: Agrega un nuevo nodo con los datos dados al principio de la lista.
- `delete(data)`: Elimina el primer nodo con los datos proporcionados de la lista.
- `print()`: Imprime todos los nodos de la lista en orden.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  append(data) {
    // code here
  }

  prepend(data) {
    // code here
  }

  delete(data) {
    // code here
  }

  print() {
    // code here
  }
}
```

## Agregar nodos

El método `append` agregará un nuevo nodo con los datos proporcionados al final de la lista.

```javascript
append(data) {
  // create a new node with the given data
  const newNode = new Node(data);

  // if the list is empty, set the new node as the head and tail
  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    // set the current tail's next property to the new node
    this.tail.next = newNode;

    // set the new node as the current tail
    this.tail = newNode;
  }
}
```

## Anteponer nodos

El método `prepend` agregará un nuevo nodo con los datos proporcionados al principio de la lista.

```javascript
prepend(data) {
  // create a new node with the given data
  const newNode = new Node(data);

  // if the list is empty, set the new node as the head and tail
  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    // set the new node's next property to the current head
    newNode.next = this.head;

    // set the new node as the current head
    this.head = newNode;
  }
}
```

## Eliminación de nodos

El método `delete` eliminará el primer nodo con los datos proporcionados de la lista.

```javascript
delete(data) {
  // if the list is empty, do nothing
  if (!this.head) {
    return;
  }

  // if the head contains the data to be deleted, delete it and set the next node as the new head
  if (this.head.data === data) {
    this.head = this.head.next;
    return;
  }

  // start at the head
  let currentNode = this.head;

  // loop until the tail
  while (currentNode.next) {
    // if the next node contains the data to be deleted, delete it and set the current node's next property to the next node's next property
    if (currentNode.next.data === data) {
      currentNode.next = currentNode.next.next;
      return;
    }

    // if the data is not found, move to the next node
    currentNode = currentNode.next;
  }
}
```

## Imprimiendo la Lista

El método `imprimir` imprimirá todos los nodos en la lista en orden.

```javascript
print() {
  // if the list is empty, do nothing
  if (!this.head) {
    return;
  }

  // start at the head
  let currentNode = this.head;

  // loop until the tail
  while (currentNode) {
    // print the current node's data
    console.log(currentNode.data);

    // move to the next node
    currentNode = currentNode.next;
  }
}
```

## Poniendolo todo junto

Ahora que hemos implementado nuestra clase de lista enlazada, veámosla en acción.

```javascript
// create a new linked list
const list = new LinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);

// prepend a node
list.prepend(0);

// delete a node
list.delete(2);

// print the list
list.print();
// 0 -> 1 -> 3
```

¡Eso es todo al respecto! Las listas enlazadas son una estructura de datos simple pero poderosa que se puede usar en una variedad de aplicaciones.