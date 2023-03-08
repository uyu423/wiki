---
title: [JavaScript] 018: Skip List
description: 
published: true
date: 2023-02-09T20:32:44.632Z
tags: 
editor: markdown
dateCreated: 2023-02-09T20:32:38.423Z
---

- [[JavaScript] 018: Lista de omisión***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-018-skip-list)
{.links-list}
- [[JavaScript] 018：跳过列表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-018-skip-list)
{.links-list}
- [[JavaScript] 018: 건너뛰기 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-018-skip-list)
{.links-list}


# Skip List

A skip list is a data structure that allows for efficient search within an ordered sequence of elements. It is a type of linked list that employs a hierarchical structure of nodes, with each node having multiple "links" to other nodes at different levels within the hierarchy. This skip list was first described by Pugh in his 1990 paper "Skip Lists: A Probabilistic Alternative to Balanced Trees".

The skip list is a randomized data structure, meaning that the order in which the nodes are linked together is determined by a random number generator. The advantage of this approach is that it allows the skip list to be constructed in O(n) time, where n is the number of elements to be inserted into the list.

The skip list has a number of applications, including in databases and file systems. It is also used in the Linux kernel's radix tree data structure.

## How Skip Lists Work

A skip list is composed of a series of levels, with each level having a set of nodes. The first level is the lowest level, and the last level is the highest level. The number of levels is determined by a random number generator.

The nodes on each level are linked together in a sorted order. The nodes on the lowest level are linked together in order of increasing value, and the nodes on the higher levels are linked together in order of decreasing value.

The skip list also has a "head" node, which is the first node on the lowest level. The head node has a pointer to the first node on the next level up. If there is no node on the next level up, then the head node's pointer will be null.

Each node in the skip list has a "value" field and a "level" field. The value field stores the value of the node, and the level field stores the level of the node.

The level of a node is determined by the random number generator. The probability that a node will be assigned a level i is 1/(2^i). This means that the chance of a node being assigned to the highest level is 1/2, the chance of a node being assigned to the second-highest level is 1/4, and so on.

The skip list is searched by starting at the head node and following the pointers to the next node at the same level. If the value of the next node is less than the value being searched for, then the pointer is followed to the next node at the same level. This process is repeated until a node is reached with a value that is greater than or equal to the value being searched for. At this point, the search follows the pointer to the next node on the level below and repeats the process.

If the value being searched for is not found in the skip list, then the search returns null.

## Code Example

Here is a simple Java implementation of a skip list. The "SkipList" class represents a skip list, and the "Node" class represents a node in the skip list.

```java
public class SkipList {
    
    private Node head;
    private int size;
    private Random random;
    
    public SkipList() {
        head = new Node(Integer.MIN_VALUE);
        size = 0;
        random = new Random();
    }
    
    public void insert(int value) {
        Node node = new Node(value);
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        node.next = current.next;
        current.next = node;
        size++;
    }
    
    public boolean contains(int value) {
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        return current.value == value;
    }
    
    public int size() {
        return size;
    }
    
    private class Node {
        int value;
        Node next;
        
        public Node(int value) {
            this.value = value;
        }
    }
    
}
```

## Exercises

1. Implement the "insert" and "contains" methods for the SkipList class.

2. Modify the SkipList class to use a doubly-linked list instead of a singly-linked list.

3. Modify the SkipList class to keep track of the number of nodes at each level.

4. Modify the SkipList class to allow for custom comparators to be used for ordering the elements in the list.

5. Modify the SkipList class to allow for custom hash functions to be used for hashing the elements in the list.