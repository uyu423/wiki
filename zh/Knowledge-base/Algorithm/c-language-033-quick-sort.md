---
title: 【C语言】033：快速排序
description: 
published: true
date: 2023-02-13T13:32:36.012Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:32:34.310Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 033: Quick Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-033-quick-sort)
{.links-list}


# 033：快速排序

快速排序是一种排序算法，它通过将数组划分为两个子数组，然后递归地对子数组进行排序来对数组进行排序。

该算法的工作原理是从数组中选择一个主元，然后围绕主元对数组进行分区，这样所有小于主元的元素都在它之前，所有大于主元的元素都在它之后。然后递归地对这两个子数组进行排序。

快速排序是一种分而治之的算法，这意味着它将问题分解为更小的子问题，然后递归地解决这些子问题。

快速排序的时间复杂度取决于实现，但最坏的情况是 O(n^2)，最好的情况是 O(n log n)。

## 代码示例

这是一个用 C 语言实现的快速排序算法。

```C
void quick_sort(int *arr, int left, int right)
{
    int i, j, pivot, tmp;

    if (left < right) {
        pivot = left;
        i = left;
        j = right;

        while (i < j) {
            while (arr[i] <= arr[pivot] && i <= right) {
                i++;
            }
            while (arr[j] > arr[pivot]) {
                j--;
            }
            if (i <= j) {
                tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
                i++;
                j--;
            }
        }

        tmp = arr[pivot];
        arr[pivot] = arr[j];
        arr[j] = tmp;

        quick_sort(arr, left, j - 1);
        quick_sort(arr, j + 1, right);
    }
}
```

## 解释

快速排序算法的工作原理是从数组中选择一个主元，然后围绕主元对数组进行分区，这样所有小于主元的元素都在它之前，所有大于主元的元素都在它之后。然后递归地对这两个子数组进行排序。

快速排序的时间复杂度取决于实现，但最坏的情况是 O(n^2)，最好的情况是 O(n log n)。

## 相关练习

1. 用你最喜欢的编程语言实现快速排序。

2. 比较快速排序和归并排序在各种输入上的运行时间。