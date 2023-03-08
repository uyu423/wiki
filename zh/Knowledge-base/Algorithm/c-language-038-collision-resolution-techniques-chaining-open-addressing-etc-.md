---
title: [C语言]038：冲突解决技术（Chaining、Open Addressing等）
description: 
published: true
date: 2023-02-13T18:32:31.728Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:32:30.158Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 038: Collision Resolution Techniques (Chaining, Open Addressing, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-038-collision-resolution-techniques-chaining-open-addressing-etc-)
{.links-list}


# 冲突解决技术

## 介绍

在计算机科学中，冲突是指两个或多个元素在哈希表中发生冲突。哈希表是一种用于存储键和值的数据结构。当一个键被散列时，散列函数将返回一个索引，用于在散列表中存储键值对。但是，如果将两个键散列到同一个索引，则会发生冲突。

存在三种主要的冲突解决技术：链接、开放寻址和双重散列。在这篇文章中，我们将详细讨论这些技术中的每一种。

## 链接

链接是一种冲突解决技术，它使用链表来存储发生冲突的键值对。当一个键被散列时，散列函数将返回一个索引。如果索引为空，则键值对简单地存储在该索引处。但是，如果该索引已被占用，则将键值对添加到该索引处的链表中。

链接的优点是易于实现。链接的缺点是，如果哈希表变得太满，它会导致性能下降。这是因为链表会变得很长，找到特定的键值对需要更长的时间。

下面是伪代码链接的示例：

```
function insert(key, value)
  index = hash(key)

  if table[index] is empty
    table[index] = key-value pair
  else
    add key-value pair to the linked list at table[index]
```

## 打开寻址

开放寻址是一种冲突解决技术，它使用探测来查找空索引来存储键值对。当一个键被散列时，散列函数将返回一个索引。如果索引为空，则键值对简单地存储在该索引处。但是，如果索引已经被占用，则键值对存储在下一个空索引处。

开放寻址的优点是如果哈希表不是太满，它可以比链接更快。开放寻址的缺点是，如果哈希表变得太满，它会导致性能下降。这是因为随着哈希表变满，探测会变得非常慢。

以下是伪代码中开放寻址的示例：

```
function insert(key, value)
  index = hash(key)

  while table[index] is occupied
    index = (index + 1) mod table.size

  table[index] = key-value pair
```

## 双重哈希

双重哈希是一种冲突解决技术，它使用两个哈希函数找到一个空索引来存储键值对。当一个键被散列时，第一个散列函数将返回一个索引。如果索引为空，则键值对简单地存储在该索引处。但是，如果索引已被占用，则使用第二个哈希函数再次对键值对进行哈希处理。第二个哈希函数将返回另一个索引，键值对存储在该索引处。

双哈希的优点是如果哈希表不是太满，它可以比开放寻址更快。双重哈希的缺点是如果哈希表变得太满，它会导致性能下降。这是因为第二个哈希函数可以返回与第一个哈希函数相同的索引，这会导致无限循环。

以下是伪代码中双重哈希的示例：

```
function insert(key, value)
  index = hash(key)
  index2 = hash2(key)

  while table[index] is occupied
    index = (index + index2) mod table.size

  table[index] = key-value pair
```

## 结论

在本文中，我们讨论了三种冲突解决技术：链接、开放寻址和双重哈希。这些技术中的每一种都有其自身的优点和缺点。选择适合您应用的技术。