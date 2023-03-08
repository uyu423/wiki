---
title: [ JavaScript ] 048：后缀数组
description: 
published: true
date: 2023-02-11T02:32:12.980Z
tags: 
editor: markdown
dateCreated: 2023-02-11T02:32:11.472Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 048: Suffix Array***English** document is available*](/en/Knowledge-base/Algorithm/javascript-048-suffix-array)
{.links-list}


# JavaScript 048：后缀数组

后缀数组是给定字符串的所有后缀的排序数组。它是一种数据结构，用于促进快速字符串操作，例如模式匹配、模式搜索和模式匹配。

后缀数组可以在O(n)的时间和空间内构造，其中n是字符串的长度。

## 建造

后缀数组的构造分为两步：

1.将后缀按字典顺序排序
2.构造后缀数组

第一步可以使用基于比较的排序算法（例如快速排序）在 O(n log n) 时间内完成。

第二步可以使用后缀树在 O(n) 时间内完成。

## 应用

后缀数组可用于各种字符串操作，例如模式匹配、模式搜索和模式匹配。

## 模式匹配

后缀数组可用于模式匹配。这个想法是使用二进制搜索来查找后缀数组中模式的第一次和最后一次出现。此操作的时间复杂度为 O(log n + m)，其中 n 是字符串的长度，m 是模式的长度。

## 模式搜索

后缀数组可用于模式搜索。这个想法是使用后缀数组来查找文本中出现的所有模式。此操作的时间复杂度为 O(log n + m)，其中 n 是字符串的长度，m 是模式的长度。

## 模式匹配

后缀数组可用于模式匹配。这个想法是使用后缀数组来查找文本中出现的所有模式。此操作的时间复杂度为 O(log n + m)，其中 n 是字符串的长度，m 是模式的长度。