---
title: [Lenguaje C] 039: cola de prioridad basada en almacenamiento dinámico
description: 
published: true
date: 2023-02-13T19:32:57.809Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:32:56.146Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 039: Heap-Based Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-039-heap-based-priority-queue)
{.links-list}


# 039: cola de prioridad basada en montón

Una cola de prioridad es una estructura de datos que le permite almacenar y recuperar elementos con una prioridad. La cola de prioridad es similar a una cola normal, excepto que cada elemento tiene una prioridad asociada. La cola de prioridad le permite eliminar primero el elemento con la prioridad más alta.

Hay dos tipos de colas de prioridad: basadas en montones y basadas en listas vinculadas. En esta publicación, nos centraremos en las colas de prioridad basadas en montón.

Una cola de prioridad basada en montón es una cola de prioridad que se implementa mediante un montón. Un montón es una estructura de datos similar a un árbol que tiene la propiedad de que el nodo raíz es siempre el elemento más pequeño (o más grande) del árbol. Esta propiedad se llama propiedad del montón.

Las colas de prioridad basadas en montón tienen las siguientes operaciones:

- insert(elemento, prioridad): inserta un elemento con la prioridad dada en la cola
- remove (): elimina y devuelve el elemento con la prioridad más alta de la cola
- peek(): devuelve el elemento con mayor prioridad de la cola sin eliminarlo

La complejidad temporal de estas operaciones es la siguiente:

- insertar (): O (registro n)
- remove(): O(log n)
- mirar(): O(1)

Las operaciones de inserción y eliminación son O (log n) porque necesitan mantener la propiedad del montón. La operación de inspección es O(1) porque no necesita modificar el montón.

Este es un ejemplo de una cola de prioridad basada en montón en acción. Usaremos un montón mínimo, que es un montón donde el nodo raíz es el elemento más pequeño del árbol.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int priority;
    int data;
} Item;

typedef struct {
    int size;
    int capacity;
    Item* items;
} PriorityQueue;

PriorityQueue* create_queue(int capacity) {
    PriorityQueue* queue = malloc(sizeof(PriorityQueue));
    queue->size = 0;
    queue->capacity = capacity;
    queue->items = malloc(sizeof(Item) * capacity);
    return queue;
}

void insert(PriorityQueue* queue, int data, int priority) {
    if (queue->size == queue->capacity) {
        return;
    }

    Item item;
    item.data = data;
    item.priority = priority;

    queue->items[queue->size] = item;
    queue->size++;

    int current_index = queue->size - 1;
    int parent_index = (current_index - 1) / 2;

    while (current_index > 0 && queue->items[current_index].priority < queue->items[parent_index].priority) {
        Item temp = queue->items[current_index];
        queue->items[current_index] = queue->items[parent_index];
        queue->items[parent_index] = temp;

        current_index = parent_index;
        parent_index = (current_index - 1) / 2;
    }
}

Item remove(PriorityQueue* queue) {
    if (queue->size == 0) {
        Item item;
        item.data = -1;
        item.priority = -1;
        return item;
    }

    Item item = queue->items[0];
    queue->size--;
    queue->items[0] = queue->items[queue->size];

    int current_index = 0;
    int left_child_index = 2 * current_index + 1;
    int right_child_index = 2 * current_index + 2;

    while (left_child_index < queue->size) {
        int min_index = current_index;

        if (queue->items[min_index].priority > queue->items[left_child_index].priority) {
            min_index = left_child_index;
        }

        if (right_child_index < queue->size && queue->items[min_index].priority > queue->items[right_child_index].priority) {
            min_index = right_child_index;
        }

        if (min_index == current_index) {
            break;
        }

        Item temp = queue->items[current_index];
        queue->items[current_index] = queue->items[min_index];
        queue->items[min_index] = temp;

        current_index = min_index;
        left_child_index = 2 * current_index + 1;
        right_child_index = 2 * current_index + 2;
    }

    return item;
}

Item peek(PriorityQueue* queue) {
    if (queue->size == 0) {
        Item item;
        item.data = -1;
        item.priority = -1;
        return item;
    }

    return queue->items[0];
}

void destroy_queue(PriorityQueue* queue) {
    free(queue->items);
    free(queue);
}

int main() {
    PriorityQueue* queue = create_queue(5);
    insert(queue, 1, 3);
    insert(queue, 2, 5);
    insert(queue, 3, 7);
    insert(queue, 4, 9);
    insert(queue, 5, 11);

    Item item = remove(queue);
    printf("%d, %d\n", item.data, item.priority);

    item = remove(queue);
    printf("%d, %d\n", item.data, item.priority);

    item = remove(queue);
    printf("%d, %d\n", item.data, item.priority);

    item = remove(queue);
    printf("%d, %d\n", item.data, item.priority);

    item = remove(queue);
    printf("%d, %d\n", item.data, item.priority);

    destroy_queue(queue);
    return 0;
}
```

Producción:

```
1, 3
2, 5
3, 7
4, 9
5, 11
```

En el ejemplo anterior, creamos una cola de prioridad con una capacidad de 5. Luego insertamos 5 elementos con diferentes prioridades en la cola. Eliminamos los elementos de la cola uno por uno. Los elementos se eliminan en orden de prioridad, y el elemento con mayor prioridad se elimina primero.

## Ejercicios

1. Implemente un montón máximo. Un montón máximo es un montón donde el nodo raíz es el elemento más grande del árbol.

2. Implemente una cola de prioridad usando una lista enlazada.