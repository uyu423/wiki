---
title: [JavaScript] 017: Lista enlazada circular
description: 
published: true
date: 2023-02-09T19:33:10.719Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:33:08.932Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 017: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-017-circular-linked-list)
{.links-list}


# JavaScript 017: Lista enlazada circular

En esta publicación, discutiremos las listas circulares enlazadas. Hablaremos sobre qué son, en qué se diferencian de las listas enlazadas normales y cómo implementarlas. También repasaremos algunas de las ventajas y desventajas de usar listas enlazadas circulares.

## ¿Qué es una lista enlazada circular?

Una lista enlazada circular es un tipo de lista enlazada donde el último nodo de la lista apunta al primer nodo de la lista. Esto crea un ciclo en la lista que nos permite recorrer la lista sin fin.

Aquí hay un ejemplo de una lista enlazada circular:

![Lista enlazada circular](https://i.imgur.com/kzgW4vD.png)

Como puede ver, el último nodo de la lista (nodo 4) apunta al primer nodo de la lista (nodo 1). Esto crea un ciclo en la lista.

## Diferencia entre listas enlazadas circulares y regulares

La principal diferencia entre las listas enlazadas circulares y regulares es que una lista enlazada regular tendrá un puntero nulo al final de la lista para indicar que se ha llegado al final de la lista. Una lista enlazada circular, por otro lado, tendrá un puntero que apunta al primer nodo de la lista.

Aquí hay un ejemplo de una lista enlazada regular:

![Lista de enlaces regulares](https://i.imgur.com/FgwJKwB.png)

Como puede ver, el último nodo de la lista (nodo 4) tiene un puntero nulo. Esto indica que se ha llegado al final de la lista.

## Cómo implementar una lista enlazada circular

Hay dos formas de implementar una lista enlazada circular:

**1. Uso de una matriz**

La primera forma de implementar una lista enlazada circular es usar una matriz. La ventaja de usar una matriz es que es fácil de implementar y recorrer la lista. La desventaja de usar una matriz es que no es muy flexible. Por ejemplo, si desea insertar un nuevo nodo en el medio de la lista, deberá cambiar todos los elementos de la matriz para dejar espacio para el nuevo nodo.

Aquí hay un ejemplo de cómo implementar una lista enlazada circular usando una matriz:

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // add a new node to the end of the list
  append(data) {
    // create a new node
    let node = new Node(data);

    // if the list is empty, set the head and tail to the new node
    if (this.size === 0) {
      this.head = node;
      this.tail = node;
    } else {
      // otherwise, set the current tail's next pointer to the new node
      this.tail.next = node;
      // and set the new node as the current tail
      this.tail = node;
    }

    // set the new node's next pointer to the head
    node.next = this.head;

    // increment the size
    this.size++;
  }

  // remove the node at the given index
  removeAt(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // if the index is the same as the size of the list,
    // it means we want to remove the tail
    if (index === this.size - 1) {
      // so set the current tail's next pointer to the head
      this.tail.next = this.head;
      // and set the head as the current tail
      this.tail = this.tail.next;
    } else {
      // otherwise, we need to find the node at the given index
      // so set a pointer to the head
      let pointer = this.head;
      // and set a counter to keep track of our position
      let counter = 0;

      // loop through the list until we find the node at the given index
      while (counter < index) {
        pointer = pointer.next;
        counter++;
      }

      // set the next pointer of the node before the one we want to remove
      // to the node after the one we want to remove
      pointer.next = pointer.next.next;
    }

    // decrement the size
    this.size--;
  }

  // return the node at the given index
  get(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we find the node at the given index
    for (let i = 0; i < index; i++) {
      pointer = pointer.next;
    }

    // return the node at the given index
    return pointer;
  }

  // return the size of the list
  getSize() {
    return this.size;
  }

  // return the head of the list
  getHead() {
    return this.head;
  }

  // return the tail of the list
  getTail() {
    return this.tail;
  }

  // return true if the list is empty, false otherwise
  isEmpty() {
    return this.size === 0;
  }

  // print the list
  print() {
    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we reach the tail
    while (pointer.next !== this.tail) {
      // print the data of the current node
      console.log(pointer.data);
      // and set the pointer to the next node
      pointer = pointer.next;
    }

    // print the data of the tail
    console.log(pointer.data);
  }
}

// create a new linked list
let list = new CircularLinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);
list.append(4);

// print the list
list.print(); // 1 2 3 4

// remove a node
list.removeAt(2);

// print the list
list.print(); // 1 2 4

// get the node at the given index
let node = list.get(1);

// print the data of the node
console.log(node.data); // 2

// get the size of the list
let size = list.getSize();

// print the size of the list
console.log(size); // 3

// get the head of the list
let head = list.getHead();

// print the data of the head
console.log(head.data); // 1

// get the tail of the list
let tail = list.getTail();

// print the data of the tail
console.log(tail.data); // 4

// check if the list is empty
let isEmpty = list.isEmpty();

// print true if the list is empty, false otherwise
console.log(isEmpty); // false
```

**2. Uso de una lista enlazada**

La segunda forma de implementar una lista enlazada circular es usar una lista enlazada. La ventaja de usar una lista enlazada es que es más flexible que una matriz. Por ejemplo, si desea insertar un nuevo nodo en medio de la lista, simplemente puede cambiar los punteros de los nodos alrededor del nuevo nodo para que apunten al nuevo nodo. La desventaja de usar una lista enlazada es que es más difícil recorrer la lista.

Aquí hay un ejemplo de cómo implementar una lista enlazada circular usando una lista enlazada:

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // add a new node to the end of the list
  append(data) {
    // create a new node
    let node = new Node(data);

    // if the list is empty, set the head and tail to the new node
    if (this.size === 0) {
      this.head = node;
      this.tail = node;
    } else {
      // otherwise, set the current tail's next pointer to the new node
      this.tail.next = node;
      // and set the new node as the current tail
      this.tail = node;
    }

    // set the new node's next pointer to the head
    node.next = this.head;

    // increment the size
    this.size++;
  }

  // remove the node at the given index
  removeAt(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // if the index is the same as the size of the list,
    // it means we want to remove the tail
    if (index === this.size - 1) {
      // so set the current tail's next pointer to the head
      this.tail.next = this.head;
      // and set the head as the current tail
      this.tail = this.tail.next;
    } else {
      // otherwise, we need to find the node at the given index
      // so set a pointer to the head
      let pointer = this.head;
      // and set a counter to keep track of our position
      let counter = 0;

      // loop through the list until we find the node before the one we want to remove
      while (counter < index - 1) {
        pointer = pointer.next;
        counter++;
      }

      // set the next pointer of the node before the one we want to remove
      // to the node after the one we want to remove
      pointer.next = pointer.next.next;
    }

    // decrement the size
    this.size--;
  }

  // return the node at the given index
  get(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we find the node at the given index
    for (let i = 0; i < index; i++) {
      pointer = pointer.next;
    }

    // return the node at the given index
    return pointer;
  }

  // return the size of the list
  getSize() {
    return this.size;
  }

  // return the head of the list
  getHead() {
    return this.head;
  }

  // return the tail of the list
  getTail() {
    return this.tail;
  }

  // return true if the list is empty, false otherwise
  isEmpty() {
    return this.size === 0;
  }

  // print the list
  print() {
    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we reach the tail
    while (pointer.next !== this.tail) {
      // print the data of the current node
      console.log(pointer.data);
      // and set the pointer to the next node
      pointer = pointer.next;
    }

    // print the data of the tail
    console.log(pointer.data);
  }
}

// create a new linked list
let list = new CircularLinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);
list.append(4);

// print the list
list.print(); // 1 2 3 4

// remove a node
list.removeAt(2);

// print the list
list.print(); // 1 2 4

// get the node at the given index
let node = list.get(1);

// print the data of the node
console.log(node.data); // 2

// get the size of the list
let size = list.getSize();

// print the size of the list
console.log(size); // 3

// get the head of the list
let head = list.getHead();

// print the data of the head
console.log(head.data); // 1

// get the tail of the list
let tail = list.getTail();

// print the data of the tail
console.log(tail.data); // 4

// check if the list is empty
let isEmpty = list.isEmpty();

// print true if the list is empty, false otherwise
console.log(isEmpty); // false
```

## Ventajas y desventajas de las listas enlazadas circulares

Hay ventajas y desventajas en el uso de listas enlazadas circulares.

**Ventajas:**

- **Se pueden usar para implementar colas.** Una cola es una estructura de datos que le permite insertar elementos al final de la lista y eliminar elementos del principio de la lista. Esto se denomina estructura de datos primero en entrar, primero en salir (FIFO). Se puede usar una lista enlazada circular para implementar una cola porque le permite insertar y eliminar elementos de la lista de manera FIFO.

- **Se pueden usar para implementar pilas.** Una pila es una estructura de datos que le permite insertar elementos en la parte superior de la lista y eliminar elementos de la parte superior de la lista. Esto se denomina estructura de datos LIFO (último en entrar, primero en salir). Se puede usar una lista enlazada circular para implementar una pila porque le permite insertar y eliminar elementos de la lista de manera LIFO.

- **Se pueden usar para implementar deques.** Un deque es una estructura de datos que le permite insertar y eliminar elementos tanto del frente como del reverso de la lista. Se puede usar una lista enlazada circular para implementar un deque porque le permite insertar y eliminar elementos de la lista tanto del frente como del reverso.

- **Se pueden usar para implementar búferes circulares.** Un búfer circular es un tipo de cola donde el último elemento de la lista está conectado al primer elemento de la lista. Esto permite que la cola se ajuste y reutilice los elementos que ya se han utilizado. Se puede usar una lista enlazada circular para implementar un búfer circular porque permite que la cola se ajuste y reutilice los elementos que ya se han usado.

- **Se pueden utilizar para implementar colas de prioridad.** Una cola de prioridad es un tipo de cola donde los elementos se insertan en la cola en orden de prioridad. Esto significa que el elemento con la prioridad más alta estará al frente de la cola y el elemento con la prioridad más baja estará al final de la cola. Se puede usar una lista enlazada circular para implementar una cola de prioridad porque le permite insertar y eliminar elementos de la lista de manera FIFO.

**Desventajas:**

-