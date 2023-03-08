---
title: [JavaScript] 013: Entonces
description: 
published: true
date: 2023-02-09T15:32:30.289Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:32:28.703Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 013: Deque***English** document is available*](/en/Knowledge-base/Algorithm/javascript-013-deque)
{.links-list}


# deque

Una deque, también conocida como cola de dos extremos, es una colección ordenada de elementos que permite agregar o eliminar elementos de cualquier extremo de la cola. Los deques son una generalización de pilas y colas y, a menudo, se implementan como una lista de enlaces dobles.

## Operaciones

Deques soporta las siguientes operaciones:

* ```push(x)```: Agrega un elemento x al final de la deque.
* ```pop()```: elimina y devuelve el elemento en la parte posterior de la deque.
* ```unshift(x)```: Agrega un elemento x al frente de la deque.
* ```shift()```: elimina y devuelve el elemento al principio de la deque.

## Implementación

En JavaScript, podemos implementar una deque usando una matriz:

```javascript
function Deque() {
  this.dataStore = [];
  this.push = push;
  this.pop = pop;
  this.unshift = unshift;
  this.shift = shift;
}

function push(element) {
  this.dataStore.push(element);
}

function pop() {
  return this.dataStore.pop();
}

function unshift(element) {
  this.dataStore.unshift(element);
}

function shift() {
  return this.dataStore.shift();
}
```

## Uso

Podemos usar un deque para implementar una cola, donde se usan las operaciones ```unshift()``` y ```shift()```:

```javascript
function Queue() {
  this.dataStore = [];
  this.enqueue = enqueue;
  this.dequeue = dequeue;
}

function enqueue(element) {
  this.dataStore.unshift(element);
}

function dequeue() {
  return this.dataStore.shift();
}
```

También podemos usar un deque para implementar una pila, donde se usan las operaciones ```push()``` y ```pop()```:

```javascript
function Stack() {
  this.dataStore = [];
  this.push = push;
  this.pop = pop;
}

function push(element) {
  this.dataStore.push(element);
}

function pop() {
  return this.dataStore.pop();
}
```

## Ejercicios

1. Implemente una cola usando un deque.

2. Implemente una pila usando un deque.

3. Implemente un verificador de palíndromo usando un deque.