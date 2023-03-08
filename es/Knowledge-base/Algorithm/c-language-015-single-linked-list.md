---
title: [Lenguaje C] 015: Lista enlazada única
description: 
published: true
date: 2023-02-13T00:32:28.921Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:32:27.251Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 015: Single Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-015-single-linked-list)
{.links-list}


# 015: Lista enlazada única

Una sola lista enlazada es una estructura de datos que contiene una secuencia de nodos. Cada nodo contiene dos campos:

- `data`: Contiene los datos del nodo.
- `siguiente`: contiene un puntero al siguiente nodo de la lista.

El primer nodo de la lista se llama nodo "principal", y el último nodo de la lista se llama nodo "cola".

![Lista de enlaces únicos](https://i.imgur.com/kTGiukN.png)

## Creando una Lista Vinculada Única

Para crear una sola lista enlazada, necesitamos crear un nodo de "cabeza" y un nodo de "cola". El nodo "cabeza" apuntará al primer nodo de la lista, y el nodo "cola" apuntará al último nodo de la lista.

Podemos crear una sola lista enlazada en C++ como esta:

```c++
// Create a head node.
Node* head = new Node();
 
// Create a tail node.
Node* tail = new Node();
 
// Set the head node's "next" field to point to the tail node.
head->next = tail;
```

## Adición de nodos a una sola lista vinculada

Para agregar un nodo a una sola lista enlazada, debemos hacer dos cosas:

- Crear un nuevo nodo.
- Configure el campo `siguiente` del último nodo de la lista para que apunte al nuevo nodo.

Podemos agregar un nodo a una sola lista enlazada en C++ como esta:

```c++
// Create a new node.
Node* newNode = new Node();
 
// Set the "next" field of the last node in the list to point to the new node.
tail->next = newNode;
 
// Set the new node as the new tail node.
tail = newNode;
```

## Eliminación de nodos de una sola lista vinculada

Para eliminar un nodo de una sola lista vinculada, debemos hacer dos cosas:

- Configure el campo `siguiente` del nodo antes del nodo que se eliminará para que apunte al nodo después del nodo que se eliminará.
- Eliminar el nodo.

Podemos eliminar un nodo de una sola lista enlazada en C++ de esta manera:

```c++
// Set the "next" field of the node before the node to be deleted to point to the node after the node to be deleted.
nodeBefore->next = nodeToDelete->next;
 
// Delete the node.
delete nodeToDelete;
```

## Recorriendo una sola lista enlazada

Para recorrer una sola lista enlazada, debemos comenzar en el nodo "principal" y seguir los punteros "siguientes" hasta llegar al nodo "cola".

Podemos recorrer una sola lista enlazada en C++ como esta:

```c++
// Start at the head node.
Node* currentNode = head;
 
// Follow the "next" pointers until we reach the tail node.
while (currentNode != tail)
{
    // Do something with the data in the node.
 
    // Move to the next node.
    currentNode = currentNode->next;
}
```

## Ejercicios relacionados

- [015: Lista enlazada única](https://github.com/egis/data-structures/tree/master/015-single-linked-list)
- [016: Lista de doble enlace] (https://github.com/egis/data-structures/tree/master/016-double-linked-list)
- [017: Lista enlazada circular](https://github.com/egis/data-structures/tree/master/017-circular-linked-list)