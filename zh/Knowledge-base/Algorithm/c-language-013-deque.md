---
title: 【C语言】013：双端队列
description: 
published: true
date: 2023-02-12T22:32:42.949Z
tags: 
editor: markdown
dateCreated: 2023-02-12T22:32:36.056Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 013: Deque***English** document is available*](/en/Knowledge-base/Algorithm/c-language-013-deque)
{.links-list}


# 双端队列

双端队列，也称为双端队列，是类似于堆栈或队列的有序项目集合。双端队列是栈和队列的概括（名称发音为“deck”，是“双端队列”的缩写）。

双端队列支持在恒定时间内从数据结构的任一端添加和删除项目。相反，队列和堆栈需要线性时间来添加或删除项目。

## 执行

双端队列可以实现为动态数组或链表。

### 动态数组

如果预先知道最大项目数，动态数组是双端队列的不错选择。数组可以根据需要调整大小。

要使用动态数组实现双端队列，我们可以使用循环数组。这使我们能够避免在双端队列中添加或删除项目时移动元素的需要。

![圆形阵列](https://i.imgur.com/zk0Fgdq.png)

可以使用两个变量跟踪前后索引。前面的索引表示双端队列中第一个元素的索引，后面的索引表示双端队列中最后一个元素的索引。

要将元素添加到双端队列的前面，我们递减前面的索引并将元素插入到该索引处。如果前面的索引小于 0，我们将环绕到数组的末尾。

要将元素添加到双端队列的尾部，我们增加尾部索引并将元素插入到该索引处。如果后面的索引等于数组的大小，我们就环绕到数组的开头。

要从双端队列的前面删除一个元素，我们只需删除前面索引处的元素。要从双端队列的尾部删除元素，我们删除尾部索引处的元素。

### 链表

如果事先不知道最大项目数，链表是双端队列的不错选择。

要使用链表实现双端队列，我们可以使用双向链表。这允许我们在恒定时间内从双端队列的任一端添加和删除项目。

![双向链表](https://i.imgur.com/7W5rNcu.png)

可以使用两个变量跟踪前后指针。前指针代表双端队列中的第一个节点，后指针代表双端队列中的最后一个节点。

要将元素添加到双端队列的前面，我们只需将元素插入列表的前面即可。要将元素添加到双端队列的尾部，我们将元素插入到列表的尾部。

要从双端队列的前面删除一个元素，我们只需删除列表前面的元素。要从双端队列的尾部删除元素，我们删除列表尾部的元素。

## 应用

双端队列有很多应用。下面介绍了一些更常见的应用程序。

### 队列

队列是一种数据结构，允许在一端添加项目并从另一端删除项目。队列通常称为先进先出 (FIFO) 数据结构。

队列可以用双端队列来实现。要将项目添加到队列中，我们将其添加到双端队列的尾部。要从队列中删除一个项目，我们将其从双端队列的前面删除。

### 堆

堆栈是一种数据结构，允许仅从一端添加和删除项目。堆栈通常称为后进先出 (LIFO) 数据结构。

栈可以用双端队列来实现。要将项目添加到堆栈，我们将其添加到双端队列的前面。要从堆栈中删除一个项目，我们将其从双端队列的前面删除。

### 回文

回文是前后相同的单词、短语或数字。例如，“racecar”和“1001”是回文。

要检查一个单词是否是回文，我们可以使用双端队列。我们将单词的每个字符添加到双端队列的后面。然后我们从双端队列中删除每个字符，并将其与双端队列前面的相应字符进行比较。如果所有的字符都匹配，那么这个词就是回文。

## 复杂度分析

双端队列具有以下时间复杂度：

- 访问：O(1)
- 搜索：O(n)
- 插入：O(1)
- 删除：O(1)

其中 n 是双端队列中的项目数。

双端队列具有以下空间复杂性：

- 静态数组：O(n)
- 动态数组：O(n)
- 链表：O(n)

其中 n 是可以存储在双端队列中的最大项目数。