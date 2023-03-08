---
title: [JavaScript] 009: Lista de enlaces dobles
description: 
published: true
date: 2023-02-09T11:32:54.013Z
tags: 
editor: markdown
dateCreated: 2023-02-09T11:32:47.801Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 009: Double Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-009-double-linked-list)
{.links-list}


# JavaScript 009: Lista de enlaces dobles

## ¿Qué es una lista de doble enlace?

Una **lista de enlaces dobles** es una estructura de datos que consta de un conjunto de nodos, cada uno de los cuales apunta al siguiente y al anterior nodo de la lista. Este tipo de lista enlazada se usa a menudo cuando necesitamos poder avanzar y retroceder a través de los datos.

## El objeto de nodo

En una lista de doble enlace, cada nodo tiene dos punteros:
* `siguiente`: apunta al siguiente nodo en la lista
* `prev`: apunta al nodo anterior en la lista

Además, cada nodo tiene un atributo `data` que contiene los datos reales.

## Creación de una lista de enlaces dobles

Vamos a crear una lista doble enlazada simple con tres nodos. Comenzaremos creando una clase `Nodo`:

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}
```

Ahora podemos crear nuestra clase `LinkedList`:

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

Nuestra `LinkedList` tiene dos atributos:
* `head`: apunta al primer nodo de la lista
* `tail`: apunta al último nodo de la lista

## Inserción de nodos

Hay dos formas de insertar nodos en una lista de doble enlace:
* en la **cabeza** de la lista
* en la **cola** de la lista

Comenzaremos con el método `insertAtHead`. Este método toma un parámetro `datos` y crea un nuevo nodo con esos datos. Luego, el nuevo nodo se asigna como el "cabeza" de la lista, y el puntero "siguiente" del nuevo nodo se establece para que apunte al antiguo nodo principal. Finalmente, el puntero `prev` del antiguo nodo principal se configura para apuntar al nuevo nodo.

```javascript
insertAtHead(data) {
  const newNode = new Node(data);
  newNode.next = this.head;
  this.head.prev = newNode;
  this.head = newNode;
}
```

El método 'insertAtTail' es similar, pero el nuevo nodo se asigna como 'cola' de la lista, y el puntero 'anterior' del nuevo nodo se establece para apuntar al antiguo nodo de cola. Finalmente, el puntero `siguiente` del antiguo nodo de cola se configura para apuntar al nuevo nodo.

```javascript
insertAtTail(data) {
  const newNode = new Node(data);
  newNode.prev = this.tail;
  this.tail.next = newNode;
  this.tail = newNode;
}
```

## Eliminación de nodos

También hay dos formas de eliminar nodos de una lista de doble enlace:
* del **cabeza** de la lista
* de la **cola** de la lista

Comenzaremos con el método `deleteFromHead`. Este método simplemente asigna el 'cabezal' de la lista al nodo al que apunta el puntero 'siguiente' del nodo principal actual. Luego, el puntero `prev` del nuevo nodo principal se establece en `null`.

```javascript
deleteFromHead() {
  this.head = this.head.next;
  this.head.prev = null;
}
```

El método `deleteFromTail` es similar, pero la `cola` de la lista se asigna al nodo al que apunta el puntero `anterior` del nodo final actual. Luego, el puntero `siguiente` del nuevo nodo de cola se establece en `nulo`.

```javascript
deleteFromTail() {
  this.tail = this.tail.prev;
  this.tail.next = null;
}
```

## Buscando en la lista

Podemos buscar en la lista un dato en particular usando el método de `búsqueda`. Este método toma un parámetro `data` y devuelve el nodo que contiene esos datos. Si no se encuentran los datos, el método devuelve `null`.

```javascript
search(data) {
  let current = this.head;

  while (current) {
    if (current.data === data) {
      return current;
    }
    current = current.next;
  }

  return null;
}
```

## Recorriendo la Lista

Podemos recorrer la lista usando el método `recorrer`. Este método toma una función de "devolución de llamada" que se llama en cada nodo de la lista.

```javascript
traverse(callback) {
  let current = this.head;

  while (current) {
    callback(current);
    current = current.next;
  }
}
```

## Invertir la lista

Podemos invertir la lista usando el método `reverse`. Este método simplemente intercambia los punteros `siguiente` y `anterior` de cada nodo en la lista.

```javascript
reverse() {
  let current = this.head;

  while (current) {
    const temp = current.next;
    current.next = current.prev;
    current.prev = temp;
    current = current.next;
  }

  const temp = this.head;
  this.head = this.tail;
  this.tail = temp;
}
```

## Conclusión

En esta publicación, hemos visto cómo crear y usar una lista de doble enlace. Esta estructura de datos puede ser útil cuando necesitamos poder avanzar y retroceder a través de los datos.