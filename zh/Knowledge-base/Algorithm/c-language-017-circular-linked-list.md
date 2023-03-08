---
title: [C语言]017：循环链表
description: 
published: true
date: 2023-02-13T01:32:59.535Z
tags: 
editor: markdown
dateCreated: 2023-02-13T01:32:57.863Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 017: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-017-circular-linked-list)
{.links-list}


# 循环链表

循环链表是链表的变体，其中最后一个节点指向第一个节点（或头节点）而不是指向空。即它是一个尾节点指向头节点的链表。

## 概念

循环链表是一种包含节点序列的数据结构。每个节点包含两个字段：

- 一个 **data** 字段来存储数据
- 一个 **next** 字段，包含指向列表中下一个节点的指针

循环链表的最后一个节点指向第一个节点（或头节点）。这使得循环链表成为一个**循环**的数据结构。

![循环链表](https://i.imgur.com/zgNU6UQ.png)

正如您在上图中看到的，最后一个节点（节点 4）指向第一个节点（节点 1）。

## 操作

循环链表支持以下操作：

- **插入**：您可以在列表的开头、结尾或中间的任意位置插入新节点。
- **删除**：您可以从列表的开头、结尾或中间的任意位置删除节点。
- **搜索**：您可以在列表中搜索特定节点。
- **遍历**：可以遍历链表打印每个节点存储的数据。

## 优点

循环链表与其他数据结构相比有以下优点：

- **更快的插入和删除**：您可以在循环链表的任意位置插入和删除节点。这在数组中是不可能的。
- **灵活大小**：循环链表的大小可以随时增加或减少。这在数组中是不可能的。
- **高效的内存利用**：循环链表可以使用单个指针来实现。这在数组中是不可能的。

## 缺点

循环链表有以下缺点：

- **Difficult to reverse**：循环链表很难反转。
- **无随机访问**：不能随机访问循环链表中的节点。您必须从头节点开始遍历列表，直到找到要查找的节点。

## 代码示例

### 插入

您可以在列表的开头、结尾或中间的任何位置插入新节点。

**开头插入：**

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

**最后插入：**

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

**中间插入：**

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

### 删除

您可以从列表的开头、结尾或中间的任何位置删除节点。

**从头开始删除：**

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

**从末尾删除：**

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

**从中间删除：**

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

### 搜索

您可以在列表中搜索特定节点。

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

### 遍历

您可以遍历列表以打印每个节点中存储的数据。

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

## 练习

1. 编写程序创建一个循环链表，并在链表的开头、结尾和中间插入节点。

2. 编写程序删除链表的开头、结尾和中间的节点。

3. 编写一个程序来搜索列表中的特定节点。

4. 编写程序遍历链表，打印每个节点存储的数据。