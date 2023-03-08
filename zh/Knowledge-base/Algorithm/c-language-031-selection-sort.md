---
title: [C语言]031：选择排序
description: 
published: true
date: 2023-02-13T11:32:12.470Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:32:10.900Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 031: Selection Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-031-selection-sort)
{.links-list}


# 031：选择排序

选择排序算法通过从未排序的部分中重复找到最小元素（考虑升序）并将其放在开头来对数组进行排序。该算法在给定数组中维护两个子数组。

1) 已经排序的子数组。
2) 未排序的剩余子数组。

在选择排序的每次迭代中，从未排序的子数组中选取最小元素（考虑升序）并将其移动到已排序的子数组中。

## 伪代码

```
procedure selectionSort( A : array of items )
   n = length(A)
   for i = 0 to n-1 do
      /* find the minimum element in the unsorted array */
       
      /* swap the found minimum element with the first element */
     
   done
```

## 复杂性

### 时间复杂度

最佳情况：Ω(n^2)

平均情况：Θ(n^2)

最坏情况：O(n^2)

### 空间复杂度

最坏情况：O(1)