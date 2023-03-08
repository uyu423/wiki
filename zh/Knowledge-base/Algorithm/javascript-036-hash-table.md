---
title: [JavaScript] 036：哈希表
description: 
published: true
date: 2023-02-10T14:33:06.480Z
tags: 
editor: markdown
dateCreated: 2023-02-10T14:33:04.735Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 036: Hash Table***English** document is available*](/en/Knowledge-base/Algorithm/javascript-036-hash-table)
{.links-list}


# JavaScript 036：哈希表

在这篇文章中，我们将讨论哈希表，这是一种用于存储键值对的数据结构。我们将介绍哈希表背后的概念和理论，查看一些代码示例，并完成一些相关练习。

## 什么是哈希表？

哈希表是一种存储键值对的数据结构。它类似于数组，但键用于索引值的位置而不是数字索引。

哈希表用于实现映射和集合。它们还用于许多其他应用程序，例如缓存、快速查找等。

## 哈希表是如何工作的？

哈希表使用哈希函数将键映射到值。哈希函数是一个函数，它接受一个键并将其映射到哈希表中的一个位置。

该位置称为存储桶。桶只是一个数组索引。

哈希函数用于计算给定键的桶。该函数获取键并根据键计算数组索引。该索引用于存储数组中的值。

## 为什么要使用哈希表？

哈希表很快。他们有恒定的时间插入和查找。这意味着插入或查找值所花费的时间与哈希表的大小无关。

哈希表也很灵活。它们可用于实现许多不同的数据结构，例如映射、集合等。

## 代码示例

这是一个简单的 JavaScript 哈希表实现。


```javascript
function HashTable(size) {
  this.buckets = new Array(size);
  this.numBuckets = this.buckets.length;
}

function HashNode(key, value, next) {
  this.key = key;
  this.value = value;
  this.next = next || null;
}

HashTable.prototype.hash = function(key) {
  var total = 0;
  for (var i = 0; i < key.length; i++) {
    total += key.charCodeAt(i);
  }
  var bucket = total % this.numBuckets;
  return bucket;
};

HashTable.prototype.insert = function(key, value) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    this.buckets[bucket] = new HashNode(key, value);
  }
  else if (this.buckets[bucket].key === key) {
    this.buckets[bucket].value = value;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode.next) {
      if (currentNode.next.key === key) {
        currentNode.next.value = value;
        return;
      }
      currentNode = currentNode.next;
    }
    currentNode.next = new HashNode(key, value);
  }
};

HashTable.prototype.get = function(key) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    return null;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode) {
      if (currentNode.key === key) {
        return currentNode.value;
      }
      currentNode = currentNode.next;
    }
    return null;
  }
};

HashTable.prototype.retrieveAll = function() {
  var allValues = [];
  for (var i = 0; i < this.numBuckets; i++) {
    var currentNode = this.buckets[i];
    while (currentNode) {
      allValues.push(currentNode.value);
      currentNode = currentNode.next;
    }
  }
  return allValues;
};

var myHT = new HashTable(30);

myHT.insert('dean', 'dean@gmail.com');
myHT.insert('megan', 'megan@gmail.com');
myHT.insert('dave', 'dave@gmail.com');
myHT.insert('jane', 'jane@gmail.com');
myHT.insert('mike', 'mike@gmail.com');
myHT.insert('sarah', 'sarah@gmail.com');
myHT.insert('john', 'john@gmail.com');

console.log(myHT.retrieveAll());
// ['dean@gmail.com', 'megan@gmail.com', 'dave@gmail.com', 'jane@gmail.com', 'mike@gmail.com', 'sarah@gmail.com', 'john@gmail.com']
```

在上面的代码示例中，我们创建了一个 HashTable 类和一个 HashNode 类。 HashTable 类有一个用于初始化数组的大小属性。它还有一个 numBuckets 属性，用于存储数组的大小。

HashNode 类具有键、值和下一个属性。 key用来存放节点的key，value用来存放节点的值，next属性用来存放链表中的下一个节点。

HashTable 类有一个散列函数，它接受一个键并将其映射到数组中的一个位置。该位置称为存储桶。桶只是一个数组索引。

HashTable 类还有一个插入函数，它接受一个键和一个值。它使用哈希函数计算给定键的桶。如果桶是空的，它会创建一个新的 HashNode 并将其存储在桶中。如果桶不为空，它会检查密钥是否已经存在。如果键存在，它会更新值。如果键不存在，则将新的 HashNode 添加到链表的末尾。

HashTable 类还有一个 get 函数，它接受一个键并返回给定键的值。如果键不存在，则返回 null。

HashTable 类还有一个 retrieveAll 函数，它返回哈希表中所有值的数组。

## 练习

1. 用你最喜欢的编程语言实现一个哈希表。

2. 编写一个函数，接受一个键和一个值并将其插入到哈希表中。

3. 编写一个函数，接受一个键并返回给定键的值。

4. 编写一个函数，返回哈希表中所有值的数组。