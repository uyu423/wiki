---
title: [Lenguaje C] 017: Lista enlazada circular
description: 
published: true
date: 2023-02-13T01:32:59.553Z
tags: 
editor: markdown
dateCreated: 2023-02-13T01:32:57.863Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 017: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-017-circular-linked-list)
{.links-list}


# Lista enlazada circular

Una lista enlazada circular es una variación de la lista enlazada en la que el último nodo apunta al primer nodo (o al nodo principal) en lugar de apuntar a nulo. Es decir, es una lista enlazada cuyo nodo de cola apunta al nodo de cabeza.

## Concepto

Una lista enlazada circular es una estructura de datos que contiene una secuencia de nodos. Cada nodo contiene dos campos:

- Un campo de **datos** para almacenar los datos
- Un campo **siguiente** que contiene un puntero al siguiente nodo en la lista

El último nodo de una lista enlazada circular apunta al primer nodo (o al nodo principal). Esto hace que la lista enlazada circular sea una estructura de datos **circular**.

![Lista enlazada circular](https://i.imgur.com/zgNU6UQ.png)

Como puede ver en el diagrama anterior, el último nodo (nodo 4) apunta hacia el primer nodo (nodo 1).

## Operaciones

Una lista enlazada circular admite las siguientes operaciones:

- **Inserción**: puede insertar un nuevo nodo al principio, al final o en cualquier lugar en el medio de la lista.
- **Eliminación**: puede eliminar un nodo desde el principio, desde el final o desde cualquier lugar en el medio de la lista.
- **Buscar**: puede buscar un nodo en particular en la lista.
- **Recorrido**: Puede recorrer la lista para imprimir los datos almacenados en cada nodo.

## Ventajas

Las listas enlazadas circulares tienen las siguientes ventajas sobre otras estructuras de datos:

- **Inserción y eliminación más rápidas**: puede insertar y eliminar nodos en cualquier posición en una lista enlazada circular. Esto no es posible en una matriz.
- **Tamaño flexible**: el tamaño de una lista enlazada circular se puede aumentar o disminuir en cualquier momento. Esto no es posible en una matriz.
- **Uso eficiente de la memoria**: se puede implementar una lista enlazada circular usando un solo puntero. Esto no es posible en una matriz.

## Desventajas

Las listas enlazadas circulares tienen las siguientes desventajas:

- **Difícil de revertir**: Es difícil revertir una lista enlazada circular.
- **Sin acceso aleatorio**: no puede acceder a un nodo en una lista circular enlazada al azar. Debe comenzar desde el nodo principal y recorrer la lista hasta encontrar el nodo que está buscando.

## Ejemplos de código

### Inserción

Puede insertar un nuevo nodo al principio, al final o en cualquier lugar en el medio de la lista.

**Inserción al principio:**

```c
void insertAtBeginning(int data) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // Set the next field of the last node to point to the new node
  if(head != NULL) {
    struct Node* temp = head;
    while(temp->next != head) {
      temp = temp->next;
    }
    temp->next = newNode;
  } else {
    // If the list is empty, set the new node as the head node
    newNode->next = newNode;
  }
 
  // Set the new node as the head node
  head = newNode;
}
```

**Inserción al final:**

```c
void insertAtEnd(int data) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // If the list is empty, set the new node as the head node
  if(head == NULL) {
    head = newNode;
  } else {
    // Set the next field of the last node to point to the new node
    struct Node* temp = head;
    while(temp->next != head) {
      temp = temp->next;
    }
    temp->next = newNode;
  }
}
```

**Inserción en el medio:**

```c
void insertInMiddle(int data, int position) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // If the list is empty, set the new node as the head node
  if(head == NULL) {
    head = newNode;
  } else {
    // Find the node at the given position
    struct Node* temp = head;
    int i;
    for(i=0; i<position-1; i++) {
      temp = temp->next;
    }
 
    // Set the next field of the new node to point to the node at the given position
    newNode->next = temp->next;
 
    // Set the next field of the node at the given position to point to the new node
    temp->next = newNode;
  }
}
```

### Eliminación

Puede eliminar un nodo desde el principio, desde el final o desde cualquier lugar en el medio de la lista.

**Eliminación desde el principio:**

```c
void deleteFromBeginning() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the last node
  struct Node* temp = head;
  while(temp->next != head) {
    temp = temp->next;
  }
 
  // Set the next field of the last node to point to the head node
  temp->next = head->next;
 
  // Free the memory occupied by the head node
  free(head);
 
  // Set the head node to the node at the given position
  head = temp->next;
}
```

**Eliminación del final:**

```c
void deleteFromEnd() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the last node
  struct Node* temp = head;
  while(temp->next != head) {
    temp = temp->next;
  }
 
  // Set the next field of the last node to point to the head node
  temp->next = head;
 
  // Free the memory occupied by the last node
  free(temp);
}
```

**Supresión del medio:**

```c
void deleteFromMiddle(int position) {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the node at the given position
  struct Node* temp = head;
  int i;
  for(i=0; i<position-1; i++) {
    temp = temp->next;
  }
 
  // Set the next field of the node at the given position to point to the node at the given position
  struct Node* toBeDeleted = temp->next;
 
  // Set the next field of the node at the given position to point to the node at the given position
  temp->next = toBeDeleted->next;
 
  // Free the memory occupied by the node at the given position
  free(toBeDeleted);
}
```

### Buscar

Puede buscar un nodo en particular en la lista.

```c
void search(int data) {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the node with the given data
  struct Node* temp = head;
  int position = 1;
  while(temp->next != head) {
    if(temp->data == data) {
      break;
    }
    temp = temp->next;
    position++;
  }
 
  // If the data is not found, return
  if(temp->data != data) {
    return;
  }
 
  // Print the data
  printf("%d", temp->data);
}
```

### El recorrido

Puede recorrer la lista para imprimir los datos almacenados en cada nodo.

```c
void traverse() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Print the data in each node
  struct Node* temp = head;
  do {
    printf("%d ", temp->data);
    temp = temp->next;
  } while(temp != head);
}
```

## Ejercicios

1. Escriba un programa para crear una lista enlazada circular e inserte nodos al principio, al final y en el medio de la lista.

2. Escriba un programa para eliminar nodos desde el principio, desde el final y desde el medio de la lista.

3. Escriba un programa para buscar un nodo en particular en la lista.

4. Escriba un programa para recorrer la lista e imprimir los datos almacenados en cada nodo.