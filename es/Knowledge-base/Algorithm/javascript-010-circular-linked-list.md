---
title: [JavaScript] 010: Lista enlazada circular
description: 
published: true
date: 2023-02-09T12:32:50.665Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:32:49.032Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 010: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-010-circular-linked-list)
{.links-list}


# JavaScript 010: Lista enlazada circular

Una lista enlazada es una estructura de datos lineal, formada por nodos que apuntan al siguiente nodo de la lista. Una lista enlazada circular es una lista enlazada donde el último nodo apunta hacia el primer nodo, creando un bucle.

## Concepto

Una lista enlazada es una estructura de datos lineal, formada por nodos que apuntan al siguiente nodo de la lista. Una lista enlazada circular es una lista enlazada donde el último nodo apunta hacia el primer nodo, creando un bucle.

Una lista enlazada circular puede ser una lista enlazada simple, donde cada nodo solo tiene una referencia al siguiente nodo, o una lista doblemente enlazada, donde cada nodo tiene una referencia al nodo siguiente y al nodo anterior.

Una lista enlazada circular es una estructura de datos que se puede utilizar para almacenar una lista de elementos. Es similar a una lista enlazada individualmente, excepto que el último nodo de la lista apunta hacia el primer nodo. Esto crea un bucle, de modo que puede recorrer la lista sin fin.

Hay varias ventajas de usar una lista enlazada circular sobre una lista enlazada simple. En primer lugar, es más fácil de implementar porque no es necesario realizar un seguimiento del final de la lista. En segundo lugar, es más eficiente porque puede comenzar en cualquier punto de la lista y recorrer toda la lista sin tener que reiniciar desde el principio. Finalmente, es más flexible porque puede insertar y eliminar elementos en cualquier punto de la lista.

## Ejemplos de código

Aquí hay una implementación simple de una lista enlazada circular en JavaScript.

```javascript
function Node(data) {
  this.data = data;
  this.next = null;
}

function CircularLinkedList() {
  this.head = null;
  this.tail = null;
  this.length = 0;
}

CircularLinkedList.prototype.add = function(data) {
  var node = new Node(data);

  if (this.length === 0) {
    this.head = node;
  } else {
    this.tail.next = node;
  }

  node.next = this.head;
  this.tail = node;
  this.length++;
};

CircularLinkedList.prototype.remove = function(data) {
  var current = this.head;
  var previous = null;
  var index = 0;

  if (this.length === 0) {
    return null;
  }

  if (this.length === 1) {
    this.head = null;
    this.tail = null;
    this.length--;
    return current.data;
  }

  while (current) {
    if (current.data === data) {
      previous.next = current.next;
      this.length--;
      return current.data;
    }

    previous = current;
    current = current.next;
    index++;
  }

  return null;
};

CircularLinkedList.prototype.get = function(index) {
  var current = this.head;
  var count = 0;

  while (count < index) {
    current = current.next;
    count++;
  }

  return current.data;
};

CircularLinkedList.prototype.contains = function(data) {
  var current = this.head;

  while (current) {
    if (current.data === data) {
      return true;
    }

    current = current.next;
  }

  return false;
};

CircularLinkedList.prototype.size = function() {
  return this.length;
};

CircularLinkedList.prototype.toString = function() {
  var current = this.head;
  var string = '';

  while (current) {
    string += current.data + ' ';
    current = current.next;
  }

  return string.trim();
};

var list = new CircularLinkedList();
list.add('a');
list.add('b');
list.add('c');
list.add('d');
console.log(list.toString()); // a b c d
list.remove('c');
console.log(list.toString()); // a b d
console.log(list.contains('a')); // true
console.log(list.contains('b')); // true
console.log(list.contains('c')); // false
console.log(list.contains('d')); // true
console.log(list.get(0)); // a
console.log(list.get(1)); // b
console.log(list.get(2)); // d
console.log(list.size()); // 3
```

## Ejercicios

1. Implemente un método para insertar un elemento en un índice específico de la lista.

2. Implementar un método para invertir la lista.

## Respuestas

1.

```javascript
CircularLinkedList.prototype.insert = function(index, data) {
  if (index < 0 || index > this.length) {
    return null;
  }

  var node = new Node(data);
  var current = this.head;
  var previous = null;
  var count = 0;

  if (index === 0) {
    if (this.head) {
      node.next = this.head;
    }

    this.head = node;
  } else {
    while (count < index) {
      previous = current;
      current = current.next;
      count++;
    }

    node.next = current;
    previous.next = node;
  }

  this.length++;
  return node.data;
};
```

2.

```javascript
CircularLinkedList.prototype.reverse = function() {
  var current = this.head;
  var previous = null;
  var next = null;

  while (current) {
    next = current.next;
    current.next = previous;
    previous = current;
    current = next;
  }

  this.tail = this.head;
  this.head = previous;
};
```