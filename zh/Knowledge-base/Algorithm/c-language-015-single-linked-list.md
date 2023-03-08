---
title: [C语言]015：单链表
description: 
published: true
date: 2023-02-13T00:32:28.964Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:32:27.247Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 015: Single Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-015-single-linked-list)
{.links-list}


# 015：单链表

单链表是一种包含节点序列的数据结构。每个节点包含两个字段：

- `data`：包含节点的数据。
- `next`：包含指向列表中下一个节点的指针。

列表中的第一个节点称为“head”节点，列表中的最后一个节点称为“tail”节点。

![单链表](https://i.imgur.com/kTGiukN.png)

## 创建单链表

要创建单链表，我们需要创建一个“head”节点和一个“tail”节点。 `head` 节点将指向列表中的第一个节点，`tail` 节点将指向列表中的最后一个节点。

我们可以像这样在 C++ 中创建一个单链表：

```c++
// Create a head node.
Node* head = new Node();
 
// Create a tail node.
Node* tail = new Node();
 
// Set the head node's "next" field to point to the tail node.
head->next = tail;
```

## 将节点添加到单链表

要将节点添加到单个链表，我们需要做两件事：

- 创建一个新节点。
- 将列表中最后一个节点的“下一个”字段设置为指向新节点。

我们可以像这样在 C++ 中将节点添加到单个链表：

```c++
// Create a new node.
Node* newNode = new Node();
 
// Set the "next" field of the last node in the list to point to the new node.
tail->next = newNode;
 
// Set the new node as the new tail node.
tail = newNode;
```

## 从单链表中删除节点

要从单链表中删除节点，我们需要做两件事：

- 将待删除节点之前节点的`next`字段设置为指向待删除节点之后的节点。
- 删除节点。

我们可以在 C++ 中从单链表中删除一个节点，如下所示：

```c++
// Set the "next" field of the node before the node to be deleted to point to the node after the node to be deleted.
nodeBefore->next = nodeToDelete->next;
 
// Delete the node.
delete nodeToDelete;
```

## 遍历单链表

要遍历单个链表，我们需要从“head”节点开始，然后跟随“next”指针，直到到达“tail”节点。

我们可以像这样在 C++ 中遍历单个链表：

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

## 相关练习

- [015: 单链表](https://github.com/egis/data-structures/tree/master/015-single-linked-list)
- [016: 双链表](https://github.com/egis/data-structures/tree/master/016-double-linked-list)
- [017：循环链表](https://github.com/egis/data-structures/tree/master/017-circular-linked-list)