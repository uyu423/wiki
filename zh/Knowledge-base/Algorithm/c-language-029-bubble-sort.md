---
title: 【C语言】029：冒泡排序
description: 
published: true
date: 2023-02-13T10:33:00.223Z
tags: 
editor: markdown
dateCreated: 2023-02-13T10:32:58.601Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 029: Bubble Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-029-bubble-sort)
{.links-list}


# 029：冒泡排序

冒泡排序是一种排序算法，如果相邻元素的顺序错误，则通过重复交换它们来工作。冒泡排序这个名字来源于这样一个事实，即较小的元素“冒泡”到列表的顶部，而较大的元素沉到底部。

冒泡排序是最简单的排序算法之一，但也是效率最低的算法之一。它的最坏情况和平均复杂度为 **O(n^2)**，其中 **n** 是要排序的项目数。尽管它简单且效率低下，但在某些情况下仍会使用冒泡排序，因为它易于实现。

## 算法

冒泡排序背后的基本思想是将每个元素与其相邻元素进行比较，如果它们的顺序错误则交换它们。重复此过程，直到对整个列表进行排序。

考虑以下需要按升序排序的数字列表：

[5, 1, 4, 2, 8]

我们比较前两个元素 5 和 1，并交换它们，因为 5 大于 1。列表现在变成：

[1, 5, 4, 2, 8]

我们比较接下来的两个元素，5 和 4，并交换它们，因为 5 大于 4。列表现在变成：

[1, 4, 5, 2, 8]

我们比较接下来的两个元素，5 和 2，并交换它们，因为 5 大于 2。列表现在变成：

[1, 4, 2, 5, 8]

我们比较接下来的两个元素，5 和 8，并且不交换它们，因为 5 不大于 8。列表现在变成：

[1, 4, 2, 5, 8]

此时，列表已经排序，所以我们可以停下来。

以下动画显示了列表 [5, 1, 4, 2, 8] 的完整冒泡排序过程：

![冒泡排序动画](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)

## 复杂性

如前所述，冒泡排序的最坏情况和平均复杂度为 **O(n^2)**。这是因为该算法需要将每个元素与列表中的所有其他元素进行比较，如果顺序错误则交换它们。

冒泡排序的最佳情况发生在列表已经排序时。在这种情况下，算法将不需要进行任何交换，复杂度将为 **O(n)**。

## 执行

下面是用 C 编程语言实现的冒泡排序的简单实现：

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

## 锻炼

1. 用自己的编程语言实现冒泡排序算法。

2. 修改冒泡排序算法，如果列表已经排序，它会提前停止。

## 答案

1.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;

    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

2.

```C
void bubble_sort(int array[], int n)
{
    int i, j, temp;
    bool swapped;

    for (i = 0; i < n - 1; i++)
    {
        swapped = false;

        for (j = 0; j < n - i - 1; j++)
        {
            if (array[j] > array[j + 1])
            {
                temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;

                swapped = true;
            }
        }

        if (!swapped)
        {
            break;
        }
    }
}
```