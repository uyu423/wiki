---
title: [C语言]039：基于堆的优先级队列
description: 
published: true
date: 2023-02-13T19:32:57.789Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:32:56.145Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 039: Heap-Based Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-039-heap-based-priority-queue)
{.links-list}


# 039：基于堆的优先级队列

优先级队列是一种数据结构，允许您存储和检索具有优先级的项目。优先级队列类似于常规队列，不同之处在于每个项目都有一个与之关联的优先级。优先级队列允许您首先删除具有最高优先级的项目。

有两种类型的优先级队列：基于堆的和基于链表的。在这篇文章中，我们将重点关注基于堆的优先级队列。

基于堆的优先级队列是使用堆实现的优先级队列。堆是一种树状数据结构，具有根节点始终是树中最小（或最大）元素的属性。此属性称为堆属性。

基于堆的优先级队列有以下操作：

- insert(item, priority)：将具有给定优先级的项目插入队列
- remove()：从队列中移除并返回优先级最高的项目
- peek()：从队列中返回优先级最高的项目而不删除它

这些操作的时间复杂度如下：

- 插入（）：O（log n）
- 删除（）：O（log n）
- 偷看（）：O（1）

插入和删除操作是 O(log n) 因为它们需要维护堆属性。 peek 操作是 O(1)，因为它不需要修改堆。

下面是一个基于堆的优先级队列的例子。我们将使用一个最小堆，这是一个根节点是树中最小元素的堆。

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

输出：

```
1, 3
2, 5
3, 7
4, 9
5, 11
```

在上面的示例中，我们创建了一个容量为 5 的优先级队列。然后我们将 5 个具有不同优先级的项目插入到队列中。我们从队列中一个一个地删除项目。项目按优先级顺序删除，优先级最高的项目最先删除。

## 练习

1. 实现最大堆。最大堆是根节点是树中最大元素的堆。

2.使用链表实现优先级队列。