---
title: 【C语言】004：分而治之算法
description: 
published: true
date: 2023-02-12T15:32:19.185Z
tags: 
editor: markdown
dateCreated: 2023-02-12T15:32:17.492Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 004: Divide and Conquer Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-004-divide-and-conquer-algorithms)
{.links-list}


# C语言】004：分而治之算法

分而治之算法是解决问题的有力工具。通过将问题分解为更小的子问题，我们可以更有效地解决问题。

有许多分而治之的算法，但我们将重点关注两种最流行的算法：归并排序和快速排序。

## 归并排序

归并排序是一种递归算法，其工作原理是将问题划分为更小的子问题，然后组合这些子问题的解决方案。

合并排序的工作原理是将数组分成两半，对每一半进行排序，然后将两半合并在一起。归并步骤是归并排序的关键。为了合并两半，我们需要比较每一半的元素，然后将它们按正确的顺序排列。

下面是归并排序的伪代码实现：

```
def merge_sort(array):
    if len(array) <= 1:
        return array
    
    # split the array in half
    mid = len(array) // 2
    left = array[:mid]
    right = array[mid:]
    
    # sort each half
    left = merge_sort(left)
    right = merge_sort(right)
    
    # merge the halves together
    return merge(left, right)
    
def merge(left, right):
    result = []
    
    while len(left) > 0 and len(right) > 0:
        if left[0] <= right[0]:
            result.append(left[0])
            left = left[1:]
        else:
            result.append(right[0])
            right = right[1:]
            
    # either left or right may have elements left
    while len(left) > 0:
        result.append(left[0])
        left = left[1:]
        
    while len(right) > 0:
        result.append(right[0])
        right = right[1:]
        
    return result
```

归并排序是一种强大的排序算法，时间复杂度为 O(n log n)。然而，它并不是最快的排序算法。

## 快速排序

快速排序是另一种流行的分而治之算法。快速排序的工作原理是选择一个枢轴元素，然后围绕该枢轴对数组进行分区。小于枢轴的元素放在一个数组中，大于枢轴的元素放在另一个数组中。快速排序然后递归地对两个数组进行排序。

下面是快速排序的伪代码实现：

```
def quick_sort(array):
    if len(array) <= 1:
        return array
    
    # select a pivot element
    pivot = array[len(array) // 2]
    
    # partition the array around the pivot
    left = []
    right = []
    
    for element in array:
        if element < pivot:
            left.append(element)
        elif element > pivot:
            right.append(element)
        else:
            # element is equal to the pivot, so we can leave it in the array
            pass
    
    # sort the left and right arrays
    left = quick_sort(left)
    right = quick_sort(right)
    
    # merge the arrays back together
    return left + [pivot] + right
```

快速排序是一种时间复杂度为O(n log n)的快速排序算法。

## 结论

分而治之算法是解决问题的有力工具。合并排序和快速排序是两种最流行的分而治之算法。