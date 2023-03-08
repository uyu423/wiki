---
title: [C Language] 039: Heap-Based Priority Queue
description: 
published: true
date: 2023-02-13T19:33:03.132Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:32:56.150Z
---

- [[Lenguaje C] 039: cola de prioridad basada en almacenamiento dinámico***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-039-heap-based-priority-queue)
{.links-list}
- [[C语言]039：基于堆的优先级队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-039-heap-based-priority-queue)
{.links-list}
- [[C Language] 039: 힙 기반 우선순위 큐***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-039-heap-based-priority-queue)
{.links-list}


# 039: Heap-Based Priority Queue

A priority queue is a data structure that allows you to store and retrieve items with a priority. The priority queue is similar to a regular queue, except that each item has a priority associated with it. The priority queue allows you to remove the item with the highest priority first.

There are two types of priority queues: heap-based and linked-list based. In this post, we will focus on heap-based priority queues.

A heap-based priority queue is a priority queue that is implemented using a heap. A heap is a tree-like data structure that has the property that the root node is always the smallest (or largest) element in the tree. This property is called the heap property.

Heap-based priority queues have the following operations:

- insert(item, priority): inserts an item with the given priority into the queue
- remove(): removes and returns the item with the highest priority from the queue
- peek(): returns the item with the highest priority from the queue without removing it

The time complexity of these operations is as follows:

- insert(): O(log n)
- remove(): O(log n)
- peek(): O(1)

The insert and remove operations are O(log n) because they need to maintain the heap property. The peek operation is O(1) because it does not need to modify the heap.

Here is an example of a heap-based priority queue in action. We will use a min heap, which is a heap where the root node is the smallest element in the tree.

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

Output:

```
1, 3
2, 5
3, 7
4, 9
5, 11
```

In the example above, we create a priority queue with a capacity of 5. We then insert 5 items with different priorities into the queue. We remove the items from the queue one by one. The items are removed in order of their priority, with the item with the highest priority being removed first.

## Exercises

1. Implement a max heap. A max heap is a heap where the root node is the largest element in the tree.

2. Implement a priority queue using a linked list.