---
title: [C Language] 008: Linked List
description: 
published: true
date: 2023-02-12T19:32:41.891Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:32:40.204Z
---

- [[Lenguaje C] 008: Lista vinculada***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-008-linked-list)
{.links-list}
- [【C语言】008：链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-008-linked-list)
{.links-list}
- [[C언어] 008: 연결 리스트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-008-linked-list)
{.links-list}


# C Language 008: Linked List

A linked list is a linear data structure, in which the elements are not stored at contiguous memory locations. The elements in a linked list are linked using pointers.

## What is a Linked List?

A linked list is a data structure that consists of a group of nodes which together represent a sequence. Each node contains two fields:

1.  **Data field**: Contains the actual data.
2.  **Link field**: Contains the address of the next node in the sequence.

![Linked list](https://i.imgur.com/eua0oE7.png)

The above example shows a linked list with four nodes. The first node is called the **head** node, and the last node is called the **tail** node. The head node is the first node in the sequence, and the tail node is the last node in the sequence.

The nodes in a linked list are not stored at contiguous memory locations. The link field of a node contains the address of the next node in the sequence. The first node is pointed to by the head pointer, and the last node is pointed to by the tail pointer.

## Advantages of Linked Lists

1.  **Linked lists are dynamic data structures.** That is, they can grow and shrink during execution of a program.
2.  **Insertion and deletion operations can be easily implemented in linked lists.**
3.  **Linked lists can be easily implemented in different ways.** For example, they can be implemented as **singly linked lists** or **doubly linked lists**.
4.  **Circular linked lists** can be easily implemented in linked lists.

## Disadvantages of Linked Lists

1.  **Random access is not possible in linked lists.** We need to access the nodes sequentially from the beginning.
2.  **Extra memory space is required for storing the pointers.**
3.  **Arrays have better cache locality that can make them slightly faster.**

## Implementation of Linked Lists

There are two ways to implement linked lists:

1.  **Singly linked lists**: In this type of linked list, each node contains a data field and a link field, which contains the address of the next node in the sequence.
2.  **Doubly linked lists**: In this type of linked list, each node contains two link fields, which contain the addresses of the previous and next nodes in the sequence.

![Singly linked list](https://i.imgur.com/FwASDVv.png)
![Doubly linked list](https://i.imgur.com/KzZ4gcD.png)

## Operations on Linked Lists

The following operations can be performed on a linked list:

1.  **Insertion**: Adds a new node to the list.
2.  **Deletion**: Deletes a node from the list.
3.  **Traversal**: Displays the data stored in the nodes of the list.
4.  **Search**: Searches for a given data item in the list.
5.  **Reverse**: Reverses the order of the nodes in the list.

## Insertion in Linked Lists

There are three ways to insert a node in a linked list:

1.  **Insertion at the beginning of the list**: In this type of insertion, the new node is inserted at the beginning of the list.

![Insertion at the beginning of the list](https://i.imgur.com/w4VDm7q.png)

2.  **Insertion at the end of the list**: In this type of insertion, the new node is inserted at the end of the list.

![Insertion at the end of the list](https://i.imgur.com/VkzMVqY.png)

3.  **Insertion in the middle of the list**: In this type of insertion, the new node is inserted in the middle of the list.

![Insertion in the middle of the list](https://i.imgur.com/U4VxK5D.png)

## Deletion in Linked Lists

There are three ways to delete a node in a linked list:

1.  **Deletion at the beginning of the list**: In this type of deletion, the node to be deleted is the first node in the list.

![Deletion at the beginning of the list](https://i.imgur.com/FgxL0b4.png)

2.  **Deletion at the end of the list**: In this type of deletion, the node to be deleted is the last node in the list.

![Deletion at the end of the list](https://i.imgur.com/w4VDm7q.png)

3.  **Deletion in the middle of the list**: In this type of deletion, the node to be deleted is in the middle of the list.

![Deletion in the middle of the list](https://i.imgur.com/U4VxK5D.png)

## Traversal in Linked Lists

There are two ways to traverse a linked list:

1.  **Iterative traversal**: In this type of traversal, we use a loop to visit each node of the list.

2.  **Recursive traversal**: In this type of traversal, we use a recursive function to visit each node of the list.

## Search in Linked Lists

There are two ways to search for a given data item in a linked list:

1.  **Iterative search**: In this type of search, we use a loop to visit each node of the list until we find the desired data item.

2.  **Recursive search**: In this type of search, we use a recursive function to visit each node of the list until we find the desired data item.

## Reverse a Linked List

There are two ways to reverse a linked list:

1.  **Iterative method**: In this method, we use a loop to reverse the pointers of the nodes in the list.

2.  **Recursive method**: In this method, we use a recursive function to reverse the pointers of the nodes in the list.