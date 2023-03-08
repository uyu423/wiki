---
title: [C语言]014：优先队列
description: 
published: true
date: 2023-02-12T23:32:22.457Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:32:20.776Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 014: Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-014-priority-queue)
{.links-list}


# 优先队列

优先级队列是一种数据结构，它包含一组元素，每个元素都有一个优先级。元素按照优先级顺序从优先级队列中移除，优先级最高的元素首先被移除。

优先级队列常用于 Dijkstra 的最短路径算法和 Prim 的最小生成树算法等算法中，其中元素的优先级基于其与起始顶点的距离或其权重。

## 代码示例

下面是一个用 C 实现的优先级队列的例子。优先级队列被实现为一个最小堆，具有最低优先级的元素位于堆的根部。


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

## 练习

1. 用你最喜欢的编程语言实现一个优先级队列。

2.使用优先级队列实现Dijkstra最短路径算法。

3、使用优先级队列实现Prim的最小生成树算法。