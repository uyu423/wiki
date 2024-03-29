---
title: 【C语言】003：空间复杂度
description: 
published: true
date: 2023-02-12T14:32:26.254Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:32:19.506Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 003: Space Complexity***English** document is available*](/en/Knowledge-base/Algorithm/c-language-003-space-complexity)
{.links-list}



什么是空间复杂度？

空间复杂度是算法运行完成所需的内存量。它与算法使用的内存量有关，因为输入数据的大小会增加。

有两种类型的空间复杂度：静态和动态。静态空间复杂度是算法针对特定输入大小所需的内存量。动态空间复杂度是随着输入大小的增加算法所需的内存量。

静态空间复杂度通常很容易计算。例如，如果算法需要大小为 n 的数组，则静态空间复杂度为 O(n)。

动态空间复杂度通常更难计算。例如，如果一个算法需要一个大小为 n 的数组，并且每次运行该算法时数组的大小都会增加 1，那么动态空间复杂度为 O(n)。

要计算算法的空间复杂度，我们需要知道以下内容：

- 特定输入大小的算法所需的内存量
- 输入数据的大小
- 随着输入大小的增加，算法所需的内存量

例如，假设我们有一个算法需要大小为 n 的数组。如果算法每次运行时数组的大小都增加 1，那么动态空间复杂度就是 O(n)。

要计算算法的空间复杂度，我们需要知道以下内容：

- 特定输入大小的算法所需的内存量
- 输入数据的大小
- 随着输入大小的增加，算法所需的内存量

例如，假设我们有一个算法需要大小为 n 的数组。如果算法每次运行时数组的大小都增加 1，那么动态空间复杂度就是 O(n)。

要计算算法的空间复杂度，我们需要知道以下内容：

- 特定输入大小的算法所需的内存量
- 输入数据的大小
- 随着输入大小的增加，算法所需的内存量

例如，假设我们有一个算法需要大小为 n 的数组。如果算法每次运行时数组的大小都增加 1，那么动态空间复杂度就是 O(n)。

让我们看一个例子。

考虑以下算法：

```
int findMax(int array[], int n) {
   int max = array[0];
   for (int i = 1; i < n; i++) {
      if (array[i] > max) {
         max = array[i];
      }
   }
   return max;
}
```

该算法的静态空间复杂度为 O(1)，因为它只需要一个变量来存储最大值。

现在，假设我们有一个算法，它需要一个大小为 n 的数组，并且每次运行该算法时，数组的大小都会增加 1。在这种情况下，动态空间复杂度为 O(n)。

要计算算法的空间复杂度，我们需要知道以下内容：

- 特定输入大小的算法所需的内存量
- 输入数据的大小
- 随着输入大小的增加，算法所需的内存量

例如，假设我们有一个算法需要大小为 n 的数组。如果算法每次运行时数组的大小都增加 1，那么动态空间复杂度就是 O(n)。