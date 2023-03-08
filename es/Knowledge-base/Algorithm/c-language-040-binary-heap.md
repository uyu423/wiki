---
title: [Lenguaje C] 040: montón binario
description: 
published: true
date: 2023-02-13T20:32:18.820Z
tags: 
editor: markdown
dateCreated: 2023-02-13T20:32:17.160Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 040: Binary Heap***English** document is available*](/en/Knowledge-base/Algorithm/c-language-040-binary-heap)
{.links-list}


# 040: montón binario

Un montón binario es una estructura de datos de montón que toma la forma de un árbol binario. Un montón binario se define como un árbol binario con dos propiedades especiales:

1. El árbol está completo. Es decir, todos los niveles del árbol se llenan por completo excepto posiblemente el último nivel, que se llena de izquierda a derecha.
2. El árbol satisface la propiedad del montón. Es decir, cada nodo es mayor o igual que el valor de sus hijos.

Un montón binario se usa a menudo para implementar una cola de prioridad. Una cola de prioridad es una estructura de datos que le permite insertar elementos con una prioridad dada y recuperar el elemento con la prioridad más alta.

## Ejemplos de código

### Inserción

Para insertar un elemento en un montón binario, primero agregamos el elemento al nivel inferior del montón. Luego, comparamos el elemento con su padre. Si el elemento es mayor que su padre, intercambiamos los dos elementos. Continuamos comparando el elemento con su padre e intercambiando hasta que el elemento esté en la posición correcta.

```c
void insert(int value) {
  // Add the element to the bottom level of the heap.
  heap[size] = value;
  size++;

  // Compare the element to its parent.
  int index = size - 1;
  int parent = (index - 1) / 2;
  while (index > 0 && heap[parent] < heap[index]) {
    // Swap the two elements.
    int temp = heap[parent];
    heap[parent] = heap[index];
    heap[index] = temp;

    // Update the index and parent.
    index = parent;
    parent = (index - 1) / 2;
  }
}
```

### Eliminación

Para eliminar un elemento de un montón binario, primero eliminamos el elemento de la parte superior del montón. Luego, reemplazamos el elemento con el último elemento en el montón. Finalmente, comparamos el elemento con sus hijos e intercambiamos hasta que el elemento esté en la posición correcta.

```c
void delete(int value) {
  // Remove the element from the top of the heap.
  int index = 0;
  heap[index] = heap[size - 1];
  size--;

  // Compare the element to its children.
  int left = 2 * index + 1;
  int right = 2 * index + 2;
  while (left < size && (heap[index] < heap[left] || heap[index] < heap[right])) {
    // Find the largest child.
    int largest = heap[left];
    int largestIndex = left;
    if (right < size && heap[right] > largest) {
      largest = heap[right];
      largestIndex = right;
    }

    // Swap the element with the largest child.
    int temp = heap[index];
    heap[index] = heap[largestIndex];
    heap[largestIndex] = temp;

    // Update the index and children.
    index = largestIndex;
    left = 2 * index + 1;
    right = 2 * index + 2;
  }
}
```

## Ejercicios

1. Implemente un montón binario en su lenguaje de programación favorito.
2. Use su implementación de montón binario para implementar una cola de prioridad.
3. ¿Cuál es la complejidad temporal de la inserción y eliminación en un montón binario?

## Respuestas

1. Consulte los ejemplos de código para la inserción y eliminación.
2. La complejidad temporal de inserción y eliminación es O(log n).