---
title: [C Language] 014: Priority Queue
description: 
published: true
date: 2023-02-12T23:32:27.627Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:32:20.780Z
---

- [[Lenguaje C] 014: cola de prioridad***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-014-priority-queue)
{.links-list}
- [[C语言]014：优先队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-014-priority-queue)
{.links-list}
- [[C언어] 014: 우선순위 큐***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-014-priority-queue)
{.links-list}


# Priority Queue

A priority queue is a data structure that holds a set of elements, each with a priority. The elements are removed from the priority queue in order of their priority, with the element with the highest priority being removed first.

Priority queues are often used in algorithms such as Dijkstra's shortest path algorithm and Prim's minimum spanning tree algorithm, where the priority of an element is based on its distance from the starting vertex or its weight.

## Code Example

Here is an example of a priority queue implemented in C. The priority queue is implemented as a min heap, with the element with the lowest priority being at the root of the heap.


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

## Exercises

1. Implement a priority queue in your favorite programming language.

2. Use a priority queue to implement Dijkstra's shortest path algorithm.

3. Use a priority queue to implement Prim's minimum spanning tree algorithm.