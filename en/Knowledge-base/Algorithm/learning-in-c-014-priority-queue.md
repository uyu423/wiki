---
title: Learning in C 014: Priority Queue
description: 
published: true
date: 2023-02-09T03:32:16.312Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:32:16.312Z
---

- [Aprendizaje en C 014: cola de prioridad***Spanish** document is available*](/es/Knowledge-base/Algorithm/learning-in-c-014-priority-queue)
{.links-list}
- [C语言学习014：优先队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/learning-in-c-014-priority-queue)
{.links-list}
- [C 014 학습: 우선순위 큐***Korean** document is available*](/ko/Knowledge-base/Algorithm/learning-in-c-014-priority-queue)
{.links-list}


# Learning in C 014: Priority Queue

## What is a Priority Queue?

A priority queue is a data structure that allows you to store and retrieve elements in a specific order. The order is determined by a priority value assigned to each element.

## How does a Priority Queue work?

A priority queue works by maintaining a collection of elements, each with a assigned priority value. When you add an element to the queue, it is inserted into the collection in order of its priority value. When you retrieve an element from the queue, the element with the highest priority value is returned.

## Code Examples

Here is a simple example of a priority queue in C.

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int priority;
    int data;
} element;

typedef struct {
    element* elements;
    int size;
    int max_size;
} priority_queue;

void init(priority_queue* q, int max_size) {
    q->elements = malloc(sizeof(element) * max_size);
    q->size = 0;
    q->max_size = max_size;
}

void insert(priority_queue* q, int data, int priority) {
    if (q->size == q->max_size) {
        return;
    }

    element e;
    e.data = data;
    e.priority = priority;

    int i;
    for (i = q->size; i > 0 && q->elements[i-1].priority < priority; i--) {
        q->elements[i] = q->elements[i-1];
    }

    q->elements[i] = e;
    q->size++;
}

int remove(priority_queue* q) {
    if (q->size == 0) {
        return -1;
    }

    int data = q->elements[0].data;

    int i;
    for (i = 0; i < q->size - 1; i++) {
        q->elements[i] = q->elements[i+1];
    }

    q->size--;
    return data;
}

void print(priority_queue* q) {
    int i;
    for (i = 0; i < q->size; i++) {
        printf("%d ", q->elements[i].data);
    }
    printf("\n");
}

int main() {
    priority_queue q;
    init(&q, 100);

    insert(&q, 1, 3);
    insert(&q, 2, 5);
    insert(&q, 3, 1);
    insert(&q, 4, 4);

    print(&q);

    remove(&q);

    print(&q);

    return 0;
}
```

## Exercises

1. Implement a priority queue in your favorite programming language.

2. Use your priority queue to solve the following problem:

You are given a list of tasks, each with a assigned priority value. Your goal is to schedule the tasks in such a way that you complete all of the tasks, while maximizing the total priority value of the tasks completed.

3. Use your priority queue to solve the following problem:

You are given a list of tasks, each with a assigned priority value. Your goal is to schedule the tasks in such a way that you complete all of the tasks, while minimizing the number of tasks left incomplete.