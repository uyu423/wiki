---
title: [C Language] 039: 힙 기반 우선순위 큐
description: 
published: true
date: 2023-02-13T19:32:57.775Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:32:56.142Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 039: Heap-Based Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/c-language-039-heap-based-priority-queue)
{.links-list}


# 039: 힙 기반 우선순위 큐

우선 순위 큐는 우선 순위가 있는 항목을 저장하고 검색할 수 있는 데이터 구조입니다. 우선순위 대기열은 각 항목과 관련된 우선순위가 있다는 점을 제외하면 일반 대기열과 유사합니다. 우선 순위 대기열을 사용하면 우선 순위가 가장 높은 항목을 먼저 제거할 수 있습니다.

우선 순위 큐에는 힙 기반 및 연결 목록 기반의 두 가지 유형이 있습니다. 이 게시물에서는 힙 기반 우선 순위 큐에 중점을 둘 것입니다.

힙 기반 우선순위 큐는 힙을 사용하여 구현되는 우선순위 큐입니다. 힙은 루트 노드가 항상 트리에서 가장 작은(또는 가장 큰) 요소라는 특성을 갖는 트리와 유사한 데이터 구조입니다. 이 속성을 힙 속성이라고 합니다.

힙 기반 우선 순위 큐에는 다음 작업이 있습니다.

- insert(item, priority): 주어진 우선순위를 가진 항목을 queue에 삽입합니다.
- remove(): 큐에서 우선 순위가 가장 높은 항목을 제거하고 반환합니다.
- peek(): 대기열에서 제거하지 않고 우선 순위가 가장 높은 항목을 반환합니다.

이러한 작업의 시간 복잡도는 다음과 같습니다.

- 삽입(): O(log n)
- 제거(): O(로그 n)
- 엿보기(): O(1)

삽입 및 제거 작업은 힙 속성을 유지해야 하므로 O(log n)입니다. 엿보기 작업은 힙을 수정할 필요가 없기 때문에 O(1)입니다.

다음은 작동 중인 힙 기반 우선 순위 큐의 예입니다. 루트 노드가 트리에서 가장 작은 요소인 힙인 최소 힙을 사용합니다.

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

산출:

```
1, 3
2, 5
3, 7
4, 9
5, 11
```

위의 예에서 용량이 5인 우선순위 대기열을 생성합니다. 그런 다음 우선순위가 다른 5개의 항목을 대기열에 삽입합니다. 대기열에서 항목을 하나씩 제거합니다. 항목은 우선 순위에 따라 제거되며 우선 순위가 가장 높은 항목이 먼저 제거됩니다.

## 운동

1. 최대 힙을 구현합니다. 최대 힙은 루트 노드가 트리에서 가장 큰 요소인 힙입니다.

2. 연결 목록을 사용하여 우선 순위 큐를 구현합니다.