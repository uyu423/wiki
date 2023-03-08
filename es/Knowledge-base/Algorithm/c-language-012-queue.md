---
title: [Lenguaje C] 012: Cola
description: 
published: true
date: 2023-02-12T21:32:41.945Z
tags: 
editor: markdown
dateCreated: 2023-02-12T21:32:40.346Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 012: Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-012-queue)
{.links-list}


# Cola

En esta publicación, analizaremos las colas, una estructura de datos utilizada para almacenar datos en un orden particular. Repasaremos el concepto y la teoría detrás de las colas, ejemplos de código y ejercicios relacionados.

## ¿Qué es una cola?

Una cola es una estructura de datos que almacena datos en un orden particular. Las colas se utilizan a menudo en la programación informática para almacenar datos que deben procesarse en un orden específico. Por ejemplo, se puede usar una cola para almacenar una lista de tareas que debe procesar una computadora.

El orden en que se almacenan los datos en una cola se denomina orden de la cola. Los órdenes de cola más comunes son el primero en entrar, el primero en salir (FIFO) y el último en entrar, el primero en salir (LIFO).

## ¿Cómo funcionan las colas?

Las colas funcionan almacenando datos en un orden particular. El orden en que se almacenan los datos en una cola se denomina orden de la cola. Los órdenes de cola más comunes son el primero en entrar, el primero en salir (FIFO) y el último en entrar, el primero en salir (LIFO).

Los datos se agregan a una cola mediante una operación llamada poner en cola. Los datos se eliminan de una cola mediante una operación denominada dequeue.

## Ejemplos de código

Aquí hay un ejemplo de código de una cola en el lenguaje de programación C:

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int data;
    struct node* next;
} node_t;

typedef struct queue {
    node_t* head;
    node_t* tail;
} queue_t;

void enqueue(queue_t* queue, int data) {
    node_t* node = malloc(sizeof(node_t));
    node->data = data;
    node->next = NULL;
    
    if (queue->head == NULL) {
        queue->head = node;
    }
    else {
        queue->tail->next = node;
    }
    
    queue->tail = node;
}

int dequeue(queue_t* queue) {
    if (queue->head == NULL) {
        printf("Queue is empty!\n");
        exit(1);
    }
    
    node_t* node = queue->head;
    int data = node->data;
    
    queue->head = queue->head->next;
    
    free(node);
    
    return data;
}

int main() {
    queue_t* queue = malloc(sizeof(queue_t));
    queue->head = NULL;
    queue->tail = NULL;
    
    enqueue(queue, 1);
    enqueue(queue, 2);
    enqueue(queue, 3);
    
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    
    free(queue);
    
    return 0;
}
```

## Ejercicio

El siguiente es un ejercicio para evaluar su comprensión de las colas.

Implemente una cola en el lenguaje de programación C usando una matriz. Su implementación debe tener las siguientes operaciones:

- `enqueue`: agrega un elemento al final de la cola
- `dequeue`: elimina un elemento del principio de la cola
- `is_empty`: devuelve 1 si la cola está vacía, 0 en caso contrario
- `is_full`: devuelve 1 si la cola está llena, 0 en caso contrario

Aquí hay un ejemplo de código de una cola en el lenguaje de programación C:

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct queue {
    int* data;
    int head;
    int tail;
    int size;
    int capacity;
} queue_t;

void enqueue(queue_t* queue, int data) {
    if (is_full(queue)) {
        printf("Queue is full!\n");
        exit(1);
    }
    
    queue->data[queue->tail] = data;
    queue->tail = (queue->tail + 1) % queue->capacity;
    queue->size++;
}

int dequeue(queue_t* queue) {
    if (is_empty(queue)) {
        printf("Queue is empty!\n");
        exit(1);
    }
    
    int data = queue->data[queue->head];
    queue->head = (queue->head + 1) % queue->capacity;
    queue->size--;
    
    return data;
}

int is_empty(queue_t* queue) {
    return queue->size == 0;
}

int is_full(queue_t* queue) {
    return queue->size == queue->capacity;
}

int main() {
    queue_t* queue = malloc(sizeof(queue_t));
    queue->data = malloc(sizeof(int) * 10);
    queue->head = 0;
    queue->tail = 0;
    queue->size = 0;
    queue->capacity = 10;
    
    enqueue(queue, 1);
    enqueue(queue, 2);
    enqueue(queue, 3);
    
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    printf("%d\n", dequeue(queue));
    
    free(queue->data);
    free(queue);
    
    return 0;
}
```

## Comentario

Las colas son una estructura de datos útil para almacenar datos en un orden particular. A menudo se utilizan en la programación de computadoras para almacenar datos que deben procesarse en un orden específico. Las colas son fáciles de implementar y se pueden usar en una variedad de aplicaciones.