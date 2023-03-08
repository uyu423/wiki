---
title: [C Language] 017: Circular Linked List
description: 
published: true
date: 2023-02-13T01:33:04.877Z
tags: 
editor: markdown
dateCreated: 2023-02-13T01:32:57.867Z
---

- [[Lenguaje C] 017: Lista enlazada circular***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-017-circular-linked-list)
{.links-list}
- [[C语言]017：循环链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-017-circular-linked-list)
{.links-list}
- [[C언어] 017: 순환 연결 리스트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-017-circular-linked-list)
{.links-list}


# Circular Linked List

A circular linked list is a variation of the linked list in which the last node points back to the first node (or the head node) instead of pointing to null. That is, it is a linked list whose tail node points to the head node.

## Concept

A circular linked list is a data structure that contains a sequence of nodes. Each node contains two fields:

-   A **data** field to store the data
-   A **next** field that contains a pointer to the next node in the list

The last node of a circular linked list points back to the first node (or the head node). This makes the circular linked list a **circular** data structure.

![Circular Linked List](https://i.imgur.com/zgNU6UQ.png)

As you can see in the above diagram, the last node (node 4) points back to the first node (node 1).

## Operations

A circular linked list supports the following operations:

-   **Insertion**: You can insert a new node at the beginning, at the end, or anywhere in the middle of the list.
-   **Deletion**: You can delete a node from the beginning, from the end, or from anywhere in the middle of the list.
-   **Search**: You can search for a particular node in the list.
-   **Traversal**: You can traverse the list to print the data stored in each node.

## Advantages

Circular linked lists have the following advantages over other data structures:

-   **Faster insertion and deletion**: You can insert and delete nodes at any position in a circular linked list. This is not possible in an array.
-   **Flexible size**: The size of a circular linked list can be increased or decreased at any time. This is not possible in an array.
-   **Efficient memory utilization**: A circular linked list can be implemented using a single pointer. This is not possible in an array.

## Disadvantages

Circular linked lists have the following disadvantages:

-   **Difficult to reverse**: It is difficult to reverse a circular linked list.
-   **No random access**: You cannot access a node in a circular linked list at random. You have to start from the head node and traverse the list until you find the node you are looking for.

## Code Examples

### Insertion

You can insert a new node at the beginning, at the end, or anywhere in the middle of the list.

**Insertion at the beginning:**

```c
void insertAtBeginning(int data) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // Set the next field of the last node to point to the new node
  if(head != NULL) {
    struct Node* temp = head;
    while(temp->next != head) {
      temp = temp->next;
    }
    temp->next = newNode;
  } else {
    // If the list is empty, set the new node as the head node
    newNode->next = newNode;
  }
 
  // Set the new node as the head node
  head = newNode;
}
```

**Insertion at the end:**

```c
void insertAtEnd(int data) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // If the list is empty, set the new node as the head node
  if(head == NULL) {
    head = newNode;
  } else {
    // Set the next field of the last node to point to the new node
    struct Node* temp = head;
    while(temp->next != head) {
      temp = temp->next;
    }
    temp->next = newNode;
  }
}
```

**Insertion in the middle:**

```c
void insertInMiddle(int data, int position) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // If the list is empty, set the new node as the head node
  if(head == NULL) {
    head = newNode;
  } else {
    // Find the node at the given position
    struct Node* temp = head;
    int i;
    for(i=0; i<position-1; i++) {
      temp = temp->next;
    }
 
    // Set the next field of the new node to point to the node at the given position
    newNode->next = temp->next;
 
    // Set the next field of the node at the given position to point to the new node
    temp->next = newNode;
  }
}
```

### Deletion

You can delete a node from the beginning, from the end, or from anywhere in the middle of the list.

**Deletion from the beginning:**

```c
void deleteFromBeginning() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the last node
  struct Node* temp = head;
  while(temp->next != head) {
    temp = temp->next;
  }
 
  // Set the next field of the last node to point to the head node
  temp->next = head->next;
 
  // Free the memory occupied by the head node
  free(head);
 
  // Set the head node to the node at the given position
  head = temp->next;
}
```

**Deletion from the end:**

```c
void deleteFromEnd() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the last node
  struct Node* temp = head;
  while(temp->next != head) {
    temp = temp->next;
  }
 
  // Set the next field of the last node to point to the head node
  temp->next = head;
 
  // Free the memory occupied by the last node
  free(temp);
}
```

**Deletion from the middle:**

```c
void deleteFromMiddle(int position) {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the node at the given position
  struct Node* temp = head;
  int i;
  for(i=0; i<position-1; i++) {
    temp = temp->next;
  }
 
  // Set the next field of the node at the given position to point to the node at the given position
  struct Node* toBeDeleted = temp->next;
 
  // Set the next field of the node at the given position to point to the node at the given position
  temp->next = toBeDeleted->next;
 
  // Free the memory occupied by the node at the given position
  free(toBeDeleted);
}
```

### Search

You can search for a particular node in the list.

```c
void search(int data) {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the node with the given data
  struct Node* temp = head;
  int position = 1;
  while(temp->next != head) {
    if(temp->data == data) {
      break;
    }
    temp = temp->next;
    position++;
  }
 
  // If the data is not found, return
  if(temp->data != data) {
    return;
  }
 
  // Print the data
  printf("%d", temp->data);
}
```

### Traversal

You can traverse the list to print the data stored in each node.

```c
void traverse() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Print the data in each node
  struct Node* temp = head;
  do {
    printf("%d ", temp->data);
    temp = temp->next;
  } while(temp != head);
}
```

## Exercises

1.  Write a program to create a circular linked list and insert nodes at the beginning, at the end, and in the middle of the list.

2.  Write a program to delete nodes from the beginning, from the end, and from the middle of the list.

3.  Write a program to search for a particular node in the list.

4.  Write a program to traverse the list and print the data stored in each node.