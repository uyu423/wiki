---
title: [JavaScript] 041: Fibonacci Heap
description: 
published: true
date: 2023-02-10T19:32:34.704Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:32:28.112Z
---

- [[JavaScript] 041: Montón de Fibonacci***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-041-fibonacci-heap)
{.links-list}
- [[JavaScript] 041：斐波那契堆***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-041-fibonacci-heap)
{.links-list}
- [[JavaScript] 041: 피보나치 힙***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-041-fibonacci-heap)
{.links-list}


# Fibonacci Heap

In computer science, a Fibonacci heap is a data structure for priority queue operations, consisting of a collection of heap-ordered trees. It has a better amortized running time than many other priority queue data structures including the binary heap and binomial heap. Michael L. Fredman and Robert E. Tarjan developed Fibonacci heaps in 1984 and published them in a scientific journal in 1987.

A Fibonacci heap is a collection of min-heap-ordered trees. Each node has an associated value, called a key. The min-heap property is the following: the value of a node is at least the value of its children. That is, the root of the heap has the minimum key.

The Fibonacci heap data structure supports two operations: insert and extract-min. Both of these operations have a worst-case time complexity of O(log n).

## Code Examples

### Insert

In order to insert a new key into the Fibonacci heap, we simply create a new node with the key and insert it into the root list. This new node is automatically heap-ordered with respect to the other nodes in the root list, so there is no need to perform any further heap operations.

```javascript
function insert(key) {
    // create a new node with the given key
    var node = new Node(key);
    
    // insert the new node into the root list
    if (this.root == null) {
        this.root = node;
    } else {
        node.next = this.root;
        this.root.prev = node;
        this.root = node;
    }
    
    // update the size of the heap
    this.size++;
}
```

### Extract-Min

In order to extract the minimum key from the Fibonacci heap, we simply remove the minimum node from the root list and return it. Since the root list may now be empty, we need to find the new minimum node and make it the root. We also need to consolidate the heap by pairwise-linking the trees of the same degree.

```javascript
function extractMin() {
    // if the heap is empty, return null
    if (this.root == null) {
        return null;
    }
    
    // remove the minimum node from the root list
    var minNode = this.root;
    if (this.root.next == this.root) {
        this.root = null;
    } else {
        this.root.prev.next = this.root.next;
        this.root.next.prev = this.root.prev;
        this.root = this.root.next;
    }
    
    // update the size of the heap
    this.size--;
    
    // if the heap is now empty, return the minimum node
    if (this.root == null) {
        return minNode;
    }
    
    // create a new array for the root list
    var roots = [];
    
    // find the new minimum node and add the other nodes to the array
    var current = this.root;
    do {
        roots.push(current);
        current = current.next;
    } while (current != this.root);
    
    // consolidate the heap by pairwise-linking the trees of the same degree
    this.consolidate(roots);
    
    // return the minimum node
    return minNode;
}
```

## Exercises

1. Implement the Fibonacci heap data structure in your favorite programming language.

2. Use the Fibonacci heap data structure to implement a priority queue.

3. Use the Fibonacci heap data structure to solve the shortest path problem in a graph.