---
title: [C언어] 014: 우선순위 큐
description: 
published: true
date: 2023-02-12T23:32:22.475Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:32:20.776Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 014: Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-014-priority-queue)
{.links-list}


# 우선순위 대기열

우선순위 큐는 각각 우선순위가 있는 요소 세트를 보유하는 데이터 구조입니다. 요소는 우선 순위에 따라 우선 순위 대기열에서 제거되며 우선 순위가 가장 높은 요소가 먼저 제거됩니다.

우선 순위 큐는 Dijkstra의 최단 경로 알고리즘 및 Prim의 최소 스패닝 트리 알고리즘과 같은 알고리즘에서 자주 사용되며 요소의 우선 순위는 시작 정점으로부터의 거리 또는 해당 가중치를 기반으로 합니다.

## 코드 예

다음은 C로 구현된 우선 순위 큐의 예입니다. 우선 순위 큐는 최소 힙으로 구현되며 우선 순위가 가장 낮은 요소가 힙의 루트에 있습니다.


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

## 운동

1. 선호하는 프로그래밍 언어로 우선 순위 큐를 구현합니다.

2. 우선 순위 대기열을 사용하여 Dijkstra의 최단 경로 알고리즘을 구현합니다.

3. 우선 순위 대기열을 사용하여 Prim의 최소 스패닝 트리 알고리즘을 구현합니다.