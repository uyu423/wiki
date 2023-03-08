---
title: [C언어] 012: 큐
description: 
published: true
date: 2023-02-12T21:32:41.953Z
tags: 
editor: markdown
dateCreated: 2023-02-12T21:32:40.342Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 012: Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-012-queue)
{.links-list}


# 대기줄

이 게시물에서는 특정 순서로 데이터를 저장하는 데 사용되는 데이터 구조인 대기열에 대해 설명합니다. 대기열, 코드 예제 및 관련 연습의 이면에 있는 개념과 이론을 살펴보겠습니다.

## 대기열이란 무엇입니까?

큐는 특정 순서로 데이터를 저장하는 데이터 구조입니다. 대기열은 특정 순서로 처리해야 하는 데이터를 저장하기 위해 컴퓨터 프로그래밍에서 자주 사용됩니다. 예를 들어 대기열을 사용하여 컴퓨터에서 처리할 작업 목록을 저장할 수 있습니다.

큐에 데이터가 저장되는 순서를 큐의 순서라고 합니다. 가장 일반적인 대기열 순서는 선입선출(FIFO) 및 후입선출(LIFO)입니다.

## 대기열은 어떻게 작동합니까?

대기열은 특정 순서로 데이터를 저장하여 작동합니다. 큐에 데이터가 저장되는 순서를 큐의 순서라고 합니다. 가장 일반적인 대기열 순서는 선입선출(FIFO) 및 후입선출(LIFO)입니다.

enqueue라는 작업을 사용하여 데이터를 대기열에 추가합니다. 대기열에서 빼기라는 작업을 사용하여 데이터를 대기열에서 제거합니다.

## 코드 예제

다음은 C 프로그래밍 언어로 된 대기열의 코드 예입니다.

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

## 운동

다음은 대기열에 대한 이해도를 테스트하기 위한 연습입니다.

배열을 사용하여 C 프로그래밍 언어로 대기열을 구현합니다. 구현에는 다음 작업이 있어야 합니다.

- `enqueue`: 큐의 끝에 요소를 추가합니다.
- `dequeue`: 대기열의 맨 앞에서 요소를 제거합니다.
- `is_empty`: 큐가 비어 있으면 1, 그렇지 않으면 0을 반환합니다.
- `is_full`: 대기열이 가득 차면 1, 그렇지 않으면 0을 반환합니다.

다음은 C 프로그래밍 언어로 된 대기열의 코드 예입니다.

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

## 해설

큐는 특정 순서로 데이터를 저장하는 데 유용한 데이터 구조입니다. 컴퓨터 프로그래밍에서 특정 순서로 처리해야 하는 데이터를 저장하는 데 자주 사용됩니다. 대기열은 구현하기 쉽고 다양한 응용 프로그램에서 사용할 수 있습니다.