---
title: 【C语言】041：斐波那契堆
description: 
published: true
date: 2023-02-13T21:32:53.060Z
tags: 
editor: markdown
dateCreated: 2023-02-13T21:32:51.263Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 041: Fibonacci Heap***English** document is available*](/en/Knowledge-base/Algorithm/c-language-041-fibonacci-heap)
{.links-list}


# 斐波那契堆

在计算机科学中，斐波那契堆是一种用于优先队列操作的数据结构，由堆有序树的集合组成。它比许多其他优先级队列数据结构（包括二叉堆和二项式堆）具有更好的摊销运行时间。 Michael L. Fredman 和 Robert E. Tarjan 于 1984 年开发了斐波那契堆，并于 1987 年在科学期刊上发表了它们。

斐波那契堆以斐波那契数命名，用于运行时分析。与二项式堆和二叉堆相比，斐波那契堆具有渐近更好的摊销运行时间。

斐波那契堆是满足最小堆性质的树的集合，其中每个节点的键小于或等于其父节点的键。此外，每个节点都有一个度数，即该节点的子节点数。斐波那契堆由一组树组成，每棵树都是一个最小堆。

Fibonacci 堆的最小键是树的根节点的键。每个节点都有一个指向其父节点的指针（如果有的话）。如果一个节点没有父节点，那么它就是它的树的根节点，并且它是斐波那契堆的成员。

斐波那契堆是一种用于优先队列操作的数据结构，由堆有序树的集合组成。它比许多其他优先级队列数据结构（包括二叉堆和二项式堆）具有更好的摊销运行时间。 Michael L. Fredman 和 Robert E. Tarjan 于 1984 年开发了斐波那契堆，并于 1987 年在科学期刊上发表了它们。

斐波那契堆以斐波那契数命名，用于运行时分析。与二项式堆和二叉堆相比，斐波那契堆具有渐近更好的摊销运行时间。

斐波那契堆是满足最小堆性质的树的集合，其中每个节点的键小于或等于其父节点的键。此外，每个节点都有一个度数，即该节点的子节点数。斐波那契堆由一组树组成，每棵树都是一个最小堆。

Fibonacci 堆的最小键是树的根节点的键。每个节点都有一个指向其父节点的指针（如果有的话）。如果一个节点没有父节点，那么它就是它的树的根节点，并且它是斐波那契堆的成员。

Fibonacci 堆上的操作需要对数时间，常数因子为 O(1)，但 decreaseKey 操作除外，它需要分摊的对数时间。

Fibonacci 堆是第一个对所有操作都具有分摊对数时间限制的堆数据结构。

## 操作

Fibonacci 堆上的操作需要对数时间，常数因子为 O(1)，但 decreaseKey 操作除外，它需要分摊的对数时间。

Fibonacci 堆是第一个对所有操作都具有分摊对数时间限制的堆数据结构。

Fibonacci 堆上的操作是：

- 插入：使用给定的键将新节点插入到堆中。
- 最小值：返回具有最小键的节点。
- extractMin：删除并返回具有最小键的节点。
- union：创建一个新堆，它是两个给定堆的并集。
- 删除：从堆中删除一个节点。
- decreaseKey：减少给定节点的密钥。

## 代码示例

下面是一个使用 C 编程语言实现斐波那契堆的示例。

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

## 练习

1. 用您选择的语言实现斐波那契堆上的操作。

2. 使用斐波那契堆实现优先队列。

3. 使用斐波那契堆实现最小生成树算法。

4. 使用Fibonacci 堆实现Dijkstra 算法。