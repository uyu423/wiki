---
title: [C Language] 015: Single Linked List
description: 
published: true
date: 2023-02-13T00:32:34.048Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:32:27.255Z
---

- [[Lenguaje C] 015: Lista enlazada única***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-015-single-linked-list)
{.links-list}
- [[C语言]015：单链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-015-single-linked-list)
{.links-list}
- [[C언어] 015: 단일 연결 리스트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-015-single-linked-list)
{.links-list}


# 015: Single Linked List

A single linked list is a data structure that contains a sequence of nodes. Each node contains two fields:

- `data`: Contains the data for the node.
- `next`: Contains a pointer to the next node in the list.

The first node in the list is called the `head` node, and the last node in the list is called the `tail` node.

![Single Linked List](https://i.imgur.com/kTGiukN.png)

## Creating a Single Linked List

To create a single linked list, we need to create a `head` node and a `tail` node. The `head` node will point to the first node in the list, and the `tail` node will point to the last node in the list.

We can create a single linked list in C++ like this:

```c++
// Create a head node.
Node* head = new Node();
 
// Create a tail node.
Node* tail = new Node();
 
// Set the head node's "next" field to point to the tail node.
head->next = tail;
```

## Adding Nodes to a Single Linked List

To add a node to a single linked list, we need to do two things:

- Create a new node.
- Set the `next` field of the last node in the list to point to the new node.

We can add a node to a single linked list in C++ like this:

```c++
// Create a new node.
Node* newNode = new Node();
 
// Set the "next" field of the last node in the list to point to the new node.
tail->next = newNode;
 
// Set the new node as the new tail node.
tail = newNode;
```

## Deleting Nodes from a Single Linked List

To delete a node from a single linked list, we need to do two things:

- Set the `next` field of the node before the node to be deleted to point to the node after the node to be deleted.
- Delete the node.

We can delete a node from a single linked list in C++ like this:

```c++
// Set the "next" field of the node before the node to be deleted to point to the node after the node to be deleted.
nodeBefore->next = nodeToDelete->next;
 
// Delete the node.
delete nodeToDelete;
```

## Traversing a Single Linked List

To traverse a single linked list, we need to start at the `head` node and follow the `next` pointers until we reach the `tail` node.

We can traverse a single linked list in C++ like this:

```c++
// Start at the head node.
Node* currentNode = head;
 
// Follow the "next" pointers until we reach the tail node.
while (currentNode != tail)
{
    // Do something with the data in the node.
 
    // Move to the next node.
    currentNode = currentNode->next;
}
```

## Related Exercises

- [015: Single Linked List](https://github.com/egis/data-structures/tree/master/015-single-linked-list)
- [016: Double Linked List](https://github.com/egis/data-structures/tree/master/016-double-linked-list)
- [017: Circular Linked List](https://github.com/egis/data-structures/tree/master/017-circular-linked-list)