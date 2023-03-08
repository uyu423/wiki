---
title: 【C语言】012：队列
description: 
published: true
date: 2023-02-12T21:32:41.972Z
tags: 
editor: markdown
dateCreated: 2023-02-12T21:32:40.342Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 012: Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-012-queue)
{.links-list}


# 队列

在这篇文章中，我们将讨论队列，一种用于按特定顺序存储数据的数据结构。我们将回顾队列、代码示例和相关练习背后的概念和理论。

## 什么是队列？

队列是一种以特定顺序存储数据的数据结构。队列通常用于计算机编程，以存储需要按特定顺序处理的数据。例如，队列可用于存储要由计算机处理的任务列表。

数据存储在队列中的顺序称为队列的顺序。最常见的队列顺序是先进先出 (FIFO) 和后进先出 (LIFO)。

## 队列是如何工作的？

队列通过以特定顺序存储数据来工作。数据存储在队列中的顺序称为队列的顺序。最常见的队列顺序是先进先出 (FIFO) 和后进先出 (LIFO)。

使用称为入队的操作将数据添加到队列中。使用称为出列的操作从队列中删除数据。

## 代码示例

以下是 C 编程语言中队列的代码示例：

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

## 锻炼

以下是测试您对队列的理解的练习。

使用数组在 C 编程语言中实现队列。您的实施应具有以下操作：

- `enqueue`: 添加一个元素到队列的末尾
- `dequeue`: 从队列的前面移除一个元素
- `is_empty`：如果队列为空则返回 1，否则返回 0
- `is_full`：如果队列已满则返回 1，否则返回 0

以下是 C 编程语言中队列的代码示例：

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

## 评论

队列是一种有用的数据结构，用于按特定顺序存储数据。它们通常用于计算机编程以存储需要按特定顺序处理的数据。队列易于实现，可用于各种应用程序。