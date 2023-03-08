---
title: [C Language] 012: Queue
description: 
published: true
date: 2023-02-12T21:32:47.210Z
tags: 
editor: markdown
dateCreated: 2023-02-12T21:32:40.350Z
---

- [[Lenguaje C] 012: Cola***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-012-queue)
{.links-list}
- [【C语言】012：队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-012-queue)
{.links-list}
- [[C언어] 012: 큐***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-012-queue)
{.links-list}


# Queue

In this post, we will be discussing queues, a data structure used to store data in a particular order. We will go over the concept and theory behind queues, code examples, and related exercises.

## What is a Queue?

A queue is a data structure that stores data in a particular order. Queues are often used in computer programming to store data that needs to be processed in a specific order. For example, a queue can be used to store a list of tasks to be processed by a computer.

The order in which data is stored in a queue is called the queue's order. The most common queue orders are first-in-first-out (FIFO) and last-in-first-out (LIFO).

## How do Queues Work?

Queues work by storing data in a particular order. The order in which data is stored in a queue is called the queue's order. The most common queue orders are first-in-first-out (FIFO) and last-in-first-out (LIFO).

Data is added to a queue using an operation called enqueue. The data is removed from a queue using an operation called dequeue.

## Code Examples

Here is a code example of a queue in the C programming language:

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

## Exercise

The following is an exercise to test your understanding of queues.

Implement a queue in the C programming language using an array. Your implementation should have the following operations:

- `enqueue`: adds an element to the end of the queue
- `dequeue`: removes an element from the front of the queue
- `is_empty`: returns 1 if the queue is empty, 0 otherwise
- `is_full`: returns 1 if the queue is full, 0 otherwise

Here is a code example of a queue in the C programming language:

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

## Commentary

Queues are a useful data structure for storing data in a particular order. They are often used in computer programming to store data that needs to be processed in a specific order. Queues are easy to implement and can be used in a variety of applications.