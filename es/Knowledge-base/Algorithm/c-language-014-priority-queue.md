---
title: [Lenguaje C] 014: cola de prioridad
description: 
published: true
date: 2023-02-12T23:32:22.375Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:32:20.778Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 014: Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-014-priority-queue)
{.links-list}


# cola de prioridad

Una cola de prioridad es una estructura de datos que contiene un conjunto de elementos, cada uno con una prioridad. Los elementos se eliminan de la cola de prioridad en orden de prioridad, y el elemento con la prioridad más alta se elimina primero.

Las colas de prioridad a menudo se usan en algoritmos como el algoritmo de ruta más corta de Dijkstra y el algoritmo de árbol de expansión mínimo de Prim, donde la prioridad de un elemento se basa en su distancia desde el vértice inicial o su peso.

## Ejemplo de código

Este es un ejemplo de una cola de prioridad implementada en C. La cola de prioridad se implementa como un montón mínimo, con el elemento con la prioridad más baja en la raíz del montón.


```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int priority;
    int data;
} Element;

typedef struct {
    int size;
    int capacity;
    Element* elements;
} PriorityQueue;

PriorityQueue* createQueue(int capacity) {
    PriorityQueue* queue = malloc(sizeof(PriorityQueue));
    queue->size = 0;
    queue->capacity = capacity;
    queue->elements = malloc(sizeof(Element) * capacity);
    return queue;
}

int isEmpty(PriorityQueue* queue) {
    return queue->size == 0;
}

int isFull(PriorityQueue* queue) {
    return queue->size == queue->capacity;
}

void enqueue(PriorityQueue* queue, int data, int priority) {
    if (isFull(queue)) {
        printf("Queue is full\n");
        return;
    }
    
    Element element;
    element.data = data;
    element.priority = priority;
    
    int i;
    for (i = queue->size; i > 0 && queue->elements[i-1].priority > priority; i--) {
        queue->elements[i] = queue->elements[i-1];
    }
    
    queue->elements[i] = element;
    queue->size++;
}

int dequeue(PriorityQueue* queue) {
    if (isEmpty(queue)) {
        printf("Queue is empty\n");
        return -1;
    }
    
    int data = queue->elements[0].data;
    queue->size--;
    queue->elements[0] = queue->elements[queue->size];
    
    int i, child;
    for (i = 0; (child = 2*i + 1) < queue->size; i = child) {
        if (child + 1 < queue->size && queue->elements[child].priority > queue->elements[child+1].priority) {
            child++;
        }
        
        if (queue->elements[i].priority > queue->elements[child].priority) {
            queue->elements[i] = queue->elements[child];
        } else {
            break;
        }
    }
    
    return data;
}

int main() {
    PriorityQueue* queue = createQueue(10);
    
    enqueue(queue, 1, 3);
    enqueue(queue, 2, 5);
    enqueue(queue, 3, 1);
    enqueue(queue, 4, 4);
    enqueue(queue, 5, 2);
    
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    
    return 0;
}
```

## Ejercicios

1. Implemente una cola de prioridad en su lenguaje de programación favorito.

2. Utilice una cola de prioridad para implementar el algoritmo de ruta más corta de Dijkstra.

3. Utilice una cola de prioridad para implementar el algoritmo de árbol de expansión mínimo de Prim.