---
title: [C Language] 041: Fibonacci Heap
description: 
published: true
date: 2023-02-13T21:32:58.507Z
tags: 
editor: markdown
dateCreated: 2023-02-13T21:32:51.267Z
---

- [[Lenguaje C] 041: Montón de Fibonacci***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-041-fibonacci-heap)
{.links-list}
- [【C语言】041：斐波那契堆***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-041-fibonacci-heap)
{.links-list}
- [[C언어] 041: 피보나치 힙***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-041-fibonacci-heap)
{.links-list}


# Fibonacci Heap

In computer science, a Fibonacci heap is a data structure for priority queue operations, consisting of a collection of heap-ordered trees. It has a better amortized running time than many other priority queue data structures including the binary heap and binomial heap. Michael L. Fredman and Robert E. Tarjan developed Fibonacci heaps in 1984 and published them in a scientific journal in 1987.

Fibonacci heaps are named after the Fibonacci numbers, which are used in their running time analysis. Fibonacci heaps have an asymptotically better amortized running time than binomial heaps and binary heaps.

A Fibonacci heap is a collection of trees satisfying the min-heap property, in which the key of each node is less than or equal to the key of its parent. In addition, each node has a degree, which is the number of children of that node. A Fibonacci heap is made up of a set of trees, each of which is a min-heap.

The minimum key of a Fibonacci heap is the key of the root node of the tree. Each node has a pointer to its parent, if any. If a node has no parent, then it is the root node of its tree, and it is a member of the Fibonacci heap.

A Fibonacci heap is a data structure for priority queue operations, consisting of a collection of heap-ordered trees. It has a better amortized running time than many other priority queue data structures including the binary heap and binomial heap. Michael L. Fredman and Robert E. Tarjan developed Fibonacci heaps in 1984 and published them in a scientific journal in 1987.

Fibonacci heaps are named after the Fibonacci numbers, which are used in their running time analysis. Fibonacci heaps have an asymptotically better amortized running time than binomial heaps and binary heaps.

A Fibonacci heap is a collection of trees satisfying the min-heap property, in which the key of each node is less than or equal to the key of its parent. In addition, each node has a degree, which is the number of children of that node. A Fibonacci heap is made up of a set of trees, each of which is a min-heap.

The minimum key of a Fibonacci heap is the key of the root node of the tree. Each node has a pointer to its parent, if any. If a node has no parent, then it is the root node of its tree, and it is a member of the Fibonacci heap.

The operations on a Fibonacci heap take logarithmic time, with a constant factor of O(1), except for the decreaseKey operation, which takes amortized logarithmic time.

The Fibonacci heap was the first heap data structure to have an amortized logarithmic time bound for all operations.

## Operations

The operations on a Fibonacci heap take logarithmic time, with a constant factor of O(1), except for the decreaseKey operation, which takes amortized logarithmic time.

The Fibonacci heap was the first heap data structure to have an amortized logarithmic time bound for all operations.

The operations on a Fibonacci heap are:

- insert: inserts a new node into the heap with a given key.
- minimum: returns the node with the minimum key.
- extractMin: removes and returns the node with the minimum key.
- union: creates a new heap that is the union of two given heaps.
- delete: removes a node from the heap.
- decreaseKey: decreases the key of a given node.

## Code example

Here is an example implementation of a Fibonacci heap in the C programming language.

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

## Exercises

1. Implement the operations on a Fibonacci heap in the language of your choice.

2. Use a Fibonacci heap to implement a priority queue.

3. Use a Fibonacci heap to implement a minimum spanning tree algorithm.

4. Use a Fibonacci heap to implement Dijkstra's algorithm.