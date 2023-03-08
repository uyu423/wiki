---
title: [C언어] 041: 피보나치 힙
description: 
published: true
date: 2023-02-13T21:32:52.967Z
tags: 
editor: markdown
dateCreated: 2023-02-13T21:32:51.259Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 041: Fibonacci Heap***English** document is available*](/en/Knowledge-base/Algorithm/c-language-041-fibonacci-heap)
{.links-list}


# 피보나치 힙

컴퓨터 과학에서 피보나치 힙은 힙 정렬된 트리 모음으로 구성된 우선순위 대기열 작업을 위한 데이터 구조입니다. 이진 힙 및 이항 힙을 포함하여 다른 많은 우선순위 큐 데이터 구조보다 더 나은 상각 실행 시간을 갖습니다. Michael L. Fredman과 Robert E. Tarjan은 1984년에 피보나치 힙을 개발하여 1987년 과학 저널에 발표했습니다.

피보나치 힙은 실행 시간 분석에 사용되는 피보나치 수의 이름을 따서 명명되었습니다. 피보나치 힙은 이항 힙 및 이진 힙보다 점근적으로 더 나은 상각 실행 시간을 갖습니다.

피보나치 힙은 각 노드의 키가 부모의 키보다 작거나 같은 최소 힙 속성을 만족하는 트리 모음입니다. 또한 각 노드에는 해당 노드의 자식 수인 정도가 있습니다. 피보나치 힙은 각각 최소 힙인 트리 세트로 구성됩니다.

피보나치 힙의 최소 키는 트리의 루트 노드 키입니다. 각 노드에는 부모에 대한 포인터가 있습니다(있는 경우). 노드에 부모가 없으면 트리의 루트 노드이며 피보나치 힙의 구성원입니다.

피보나치 힙은 우선 순위 큐 작업을 위한 데이터 구조로, 힙 순서 트리 모음으로 구성됩니다. 이진 힙 및 이항 힙을 포함하여 다른 많은 우선순위 큐 데이터 구조보다 더 나은 상각 실행 시간을 갖습니다. Michael L. Fredman과 Robert E. Tarjan은 1984년에 피보나치 힙을 개발하여 1987년 과학 저널에 발표했습니다.

피보나치 힙은 실행 시간 분석에 사용되는 피보나치 수의 이름을 따서 명명되었습니다. 피보나치 힙은 이항 힙 및 이진 힙보다 점근적으로 더 나은 상각 실행 시간을 갖습니다.

피보나치 힙은 각 노드의 키가 부모의 키보다 작거나 같은 최소 힙 속성을 만족하는 트리 모음입니다. 또한 각 노드에는 해당 노드의 자식 수인 정도가 있습니다. 피보나치 힙은 각각 최소 힙인 트리 세트로 구성됩니다.

피보나치 힙의 최소 키는 트리의 루트 노드 키입니다. 각 노드에는 부모에 대한 포인터가 있습니다(있는 경우). 노드에 부모가 없으면 트리의 루트 노드이며 피보나치 힙의 구성원입니다.

피보나치 힙에 대한 작업은 상각 로그 시간이 걸리는 reduceKey 작업을 제외하고 상수 인수가 O(1)인 로그 시간이 걸립니다.

피보나치 힙은 모든 작업에 대한 상각 대수 시간 제한이 있는 최초의 힙 데이터 구조입니다.

## 운영

피보나치 힙에 대한 작업은 상각 로그 시간이 걸리는 reduceKey 작업을 제외하고 상수 인수가 O(1)인 로그 시간이 걸립니다.

피보나치 힙은 모든 작업에 대한 상각 대수 시간 제한이 있는 최초의 힙 데이터 구조입니다.

피보나치 힙에 대한 작업은 다음과 같습니다.

- 삽입: 주어진 키를 사용하여 새 노드를 힙에 삽입합니다.
- minimum: 키가 가장 작은 노드를 반환합니다.
- extractMin: 최소 키를 가진 노드를 제거하고 반환합니다.
- union: 주어진 두 힙의 합집합인 새 힙을 만듭니다.
- 삭제: 힙에서 노드를 제거합니다.
- reduceKey: 주어진 노드의 키를 감소시킵니다.

## 코드 예시

다음은 C 프로그래밍 언어로 피보나치 힙을 구현한 예입니다.

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int key;
    struct node *parent;
    struct node *child;
    struct node *sibling;
};

struct heap {
    struct node *min;
    int n;
};

struct heap *make_heap()
{
    struct heap *h = malloc(sizeof(struct heap));
    h->min = NULL;
    h->n = 0;
    return h;
}

struct node *make_node(int key)
{
    struct node *x = malloc(sizeof(struct node));
    x->key = key;
    x->parent = NULL;
    x->child = NULL;
    x->sibling = NULL;
    return x;
}

void heap_insert(struct heap *h, struct node *x)
{
    x->sibling = h->min;
    if (h->min != NULL) {
        h->min->parent = x;
    }
    h->min = x;
    h->n++;
}

struct node *heap_minimum(struct heap *h)
{
    return h->min;
}

struct node *heap_extract_min(struct heap *h)
{
    struct node *z = h->min;
    if (z != NULL) {
        struct node *x = z->child;
        struct node *y;
        while (x != NULL) {
            y = x->sibling;
            x->sibling = z->sibling;
            x->parent = NULL;
            z->sibling = x;
            x = y;
        }
        h->min = z->sibling;
        if (z == h->min) {
            h->min = NULL;
        }
        h->n--;
    }
    return z;
}

void heap_union(struct heap *h1, struct heap *h2)
{
    struct heap *h = make_heap();
    h->min = h1->min;
    h->n = h1->n + h2->n;
    if (h1->min == NULL || (h2->min != NULL && h2->min->key < h1->min->key)) {
        h->min = h2->min;
    }
    if (h->min != NULL) {
        if (h1->min != NULL && h1->min != h2->min) {
            h1->min->sibling = h2->min->sibling;
        }
        h2->min->sibling = h1->min;
        h1->min = h2->min;
    }
    free(h2);
}

void heap_delete(struct heap *h, struct node *x)
{
    heap_decrease_key(h, x, -1);
    heap_extract_min(h);
}

void heap_decrease_key(struct heap *h, struct node *x, int k)
{
    if (k > x->key) {
        printf("error: new key is larger than current key\n");
        return;
    }
    x->key = k;
    struct node *y = x->parent;
    if (y != NULL && x->key < y->key) {
        cut(h, x, y);
        cascading_cut(h, y);
    }
    if (x->key < h->min->key) {
        h->min = x;
    }
}

void cut(struct heap *h, struct node *x, struct node *y)
{
    x->sibling = y->child;
    if (y->child != NULL) {
        y->child->parent = x;
    }
    y->child = x;
    x->parent = y;
    y->degree++;
}

void cascading_cut(struct heap *h, struct node *y)
{
    struct node *z = y->parent;
    if (z != NULL) {
        if (!y->mark) {
            y->mark = 1;
        } else {
            cut(h, y, z);
            cascading_cut(h, z);
        }
    }
}

void heap_destroy(struct heap *h)
{
    struct node *x = h->min;
    struct node *y;
    struct node *z;
    while (x != NULL) {
        y = x->child;
        while (y != NULL) {
            z = y->sibling;
            free(y);
            y = z;
        }
        z = x->sibling;
        free(x);
        x = z;
    }
    free(h);
}

int main()
{
    struct heap *h = make_heap();
    struct node *x;
    
    x = make_node(3);
    heap_insert(h, x);
    
    x = make_node(2);
    heap_insert(h, x);
    
    x = heap_extract_min(h);
    printf("%d\n", x->key);
    
    x = heap_minimum(h);
    printf("%d\n", x->key);
    
    heap_decrease_key(h, x, 1);
    
    heap_delete(h, x);
    
    heap_destroy(h);
    
    return 0;
}
```

## 운동

1. 선택한 언어로 피보나치 힙에 작업을 구현합니다.

2. 피보나치 힙을 사용하여 우선 순위 대기열을 구현합니다.

3. 피보나치 힙을 사용하여 최소 스패닝 트리 알고리즘을 구현합니다.

4. 피보나치 힙을 사용하여 Dijkstra의 알고리즘을 구현합니다.