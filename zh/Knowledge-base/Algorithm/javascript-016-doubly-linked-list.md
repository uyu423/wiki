---
title: [JavaScript] 016：双向链表
description: 
published: true
date: 2023-02-09T18:32:31.886Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:32:30.291Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 016: Doubly Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-016-doubly-linked-list)
{.links-list}


# JavaScript 016: 双向链表

双向链表是一种数据结构，由一组以某种方式链接在一起的顺序节点组成，其中每个节点都包含对前一个节点和下一个节点的引用。这种类型的链表优于单向链表，因为它允许双向遍历。

一个典型的双向链表节点包含三个字段：

- **prev**：对列表中前一个节点的引用
- **next**：对列表中下一个节点的引用
- **data**：节点中存储的数据

双向链表中的第一个节点通常称为 **head** 节点，最后一个节点通常称为 **tail** 节点。头节点和尾节点的特殊属性是头节点的prev字段为null，尾节点的next字段为null。

这是具有四个节点的双向链表的图示：

![双向链表](https://i.imgur.com/eLzWqlN.png)

下面是 JavaScript 中基本双向链表节点的代码：

```javascript
function Node(data) {
  this.prev = null;
  this.next = null;
  this.data = data;
}
```

要在双向链表中插入一个新节点，我们首先需要找到我们要在其后插入新节点的节点。一旦我们找到那个节点，我们就可以将新节点的 next 字段设置为指向我们找到的节点，我们可以将找到的节点的 prev 字段设置为指向新节点。最后，我们可以将新节点的 prev 字段设置为指向找到的节点。

这是此插入过程的示例：

![插入双向链表](https://i.imgur.com/TGiukgD.png)

这是此插入过程的代码：

```javascript
function insertAfter(node, newNode) {
  newNode.next = node.next;
  node.next = newNode;
  newNode.prev = node;
}
```

要从双向链表中删除节点，我们首先需要找到要删除的节点。一旦我们找到了节点，我们就可以设置节点的next字段的prev字段指向节点的prev字段，我们可以设置节点的prev字段的next字段指向节点的next字段。最后，我们可以将节点的 prev 字段和 next 字段设置为 null。

这是此删除过程的示例：

![从双向链表中删除](https://i.imgur.com/FgxLbNv.png)

这是此删除过程的代码：

```javascript
function deleteNode(node) {
  node.prev.next = node.next;
  node.next.prev = node.prev;
  node.prev = null;
  node.next = null;
}
```

这里的所有都是它的！双向链表是一种简单但功能强大的数据结构，可用于各种应用程序。