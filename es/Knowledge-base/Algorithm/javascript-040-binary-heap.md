---
title: [JavaScript] 040: montón binario
description: 
published: true
date: 2023-02-10T18:32:41.254Z
tags: 
editor: markdown
dateCreated: 2023-02-10T18:32:34.938Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 040: Binary Heap***English** document is available*](/en/Knowledge-base/Algorithm/javascript-040-binary-heap)
{.links-list}


# montón binario

Un montón binario es una estructura de datos de montón que toma la forma de un árbol binario. Los montones binarios son un tipo específico de árbol binario en el que el nodo raíz es mayor o igual que cualquiera de sus elementos secundarios, y cada nodo es el elemento principal de, como máximo, dos nodos secundarios. Un montón binario se usa a menudo para implementar una cola de prioridad.

Hay dos tipos de montones binarios: montones mínimos y montones máximos. En un montón mínimo, el nodo raíz es siempre el elemento más pequeño del montón. En un montón máximo, el nodo raíz es siempre el elemento más grande del montón.

## Ejemplo de código

Aquí hay una implementación simple de un montón mínimo en JavaScript.

```javascript
class BinaryHeap {
  constructor() {
    this.heap = [];
  }

  // Returns the index of the left child of the node at the given index.
  getLeftChildIndex(parentIndex) {
    return 2 * parentIndex + 1;
  }

  // Returns the index of the right child of the node at the given index.
  getRightChildIndex(parentIndex) {
    return 2 * parentIndex + 2;
  }

  // Returns the index of the parent of the node at the given index.
  getParentIndex(childIndex) {
    return Math.floor((childIndex - 1) / 2);
  }

  // Returns true if the node at the given index has a left child.
  hasLeftChild(index) {
    return this.getLeftChildIndex(index) < this.heap.length;
  }

  // Returns true if the node at the given index has a right child.
  hasRightChild(index) {
    return this.getRightChildIndex(index) < this.heap.length;
  }

  // Returns true if the node at the given index is the root node.
  isRoot(index) {
    return index === 0;
  }

  // Swaps the elements at the given indices in the heap.
  swap(index1, index2) {
    const temp = this.heap[index1];
    this.heap[index1] = this.heap[index2];
    this.heap[index2] = temp;
  }

  // Peek at the root element.
  peek() {
    if (this.heap.length === 0) {
      throw new Error('Heap is empty');
    }

    return this.heap[0];
  }

  // Add an element to the heap.
  add(element) {
    this.heap.push(element);
    this.heapifyUp();
  }

  // Remove and return the root element.
  remove() {
    if (this.heap.length === 0) {
      throw new Error('Heap is empty');
    }

    const element = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.pop();
    this.heapifyDown();
    return element;
  }

  // Heapify up.
  heapifyUp() {
    let index = this.heap.length - 1;

    while (!this.isRoot(index) && this.heap[index] < this.heap[this.getParentIndex(index)]) {
      this.swap(index, this.getParentIndex(index));
      index = this.getParentIndex(index);
    }
  }

  // Heapify down.
  heapifyDown() {
    let index = 0;

    while (this.hasLeftChild(index)) {
      let smallerChildIndex = this.getLeftChildIndex(index);

      if (this.hasRightChild(index) && this.heap[this.getRightChildIndex(index)] < this.heap[smallerChildIndex]) {
        smallerChildIndex = this.getRightChildIndex(index);
      }

      if (this.heap[index] < this.heap[smallerChildIndex]) {
        break;
      } else {
        this.swap(index, smallerChildIndex);
      }

      index = smallerChildIndex;
    }
  }
}
```

## Ejercicios

1. Implemente un montón máximo.

2. Use un montón binario para implementar una cola de prioridad.