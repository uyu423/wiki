---
title: [C语言]034：堆排序
description: 
published: true
date: 2023-02-13T14:33:07.408Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:33:05.783Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 034: Heap Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-034-heap-sort)
{.links-list}


# 034：堆排序

堆排序是一种基于比较的排序算法。堆排序可以被认为是一种改进的选择排序：与该算法一样，它将其输入分为已排序和未排序区域，并通过提取最大元素并将其移动到已排序区域来迭代缩小未排序区域。改进包括使用堆数据结构而不是线性时间搜索来查找最大值。

堆排序由 J. W. J. Williams 于 1964 年发明。 [1] Heapsort 是一种就地算法，但它不是一种稳定的排序。

## 算法

二叉堆是一种采用二叉树形式的堆数据结构。二叉堆是实现优先级队列的常用方法。

二叉堆被定义为具有两个附加约束的二叉树：

* Shape属性：树是一棵完全二叉树；也就是说，树的所有级别，可能除了最后一层（最深的）都被完全填充，并且如果树的最后一层不完整，则该级别的节点从左到右填充。
* 堆属性：根据为堆定义的比较谓词，每个节点大于或等于其每个子节点。

堆属性允许快速访问根节点；它保证是树中最大（或最小）的元素。

该算法有两个阶段：堆构建和排序。

### 堆构造

堆构建阶段从无序数字数组开始，并将其转换为二叉堆。数组可以表示为二叉树，其中每个节点对应数组的一个元素，每个节点的子节点是数组中大于（或小于）节点元素的元素。

第一步是从数组创建一个堆。堆构建算法如下：

1. 从一个空堆开始。

2. 以任意顺序将数组的每个元素插入堆中。

3. 当堆不为空时：

    A。移除堆顶元素。

    b.将元素插入排序的数组。

4. 返回排序后的数组。

堆构建阶段的时间复杂度为 O(n)，其中 n 是数组中元素的数量。

### 排序

排序阶段从二叉堆开始并将其转换为排序数组。排序算法如下：

1. 当堆不为空时：

    A。移除堆顶元素。

    b.将元素插入排序的数组。

2. 返回排序后的数组。

排序阶段的时间复杂度为 O(nlog(n))，其中 n 是数组中元素的数量。这是因为，在 while 循环的每次迭代中，堆顶元素被移除并执行 heapify 操作。 heapify操作耗时O(log(n))，while循环有n次迭代，所以总时间复杂度为O(nlog(n))。

## 代码示例

下面是C语言的堆排序实现：

```c
#include <stdio.h>
#include <stdlib.h>

void heapify(int* array, int size, int i)
{
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < size && array[left] > array[largest])
        largest = left;

    if (right < size && array[right] > array[largest])
        largest = right;

    if (largest != i)
    {
        int temp = array[i];
        array[i] = array[largest];
        array[largest] = temp;

        heapify(array, size, largest);
    }
}

void heap_sort(int* array, int size)
{
    for (int i = size / 2 - 1; i >= 0; i--)
        heapify(array, size, i);

    for (int i = size - 1; i >= 0; i--)
    {
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;

        heapify(array, i, 0);
    }
}

int main()
{
    int array[] = {3, 2, 1, 5, 4};
    int size = sizeof(array) / sizeof(array[0]);

    heap_sort(array, size);

    for (int i = 0; i < size; i++)
        printf("%d ", array[i]);
    printf("\n");

    return 0;
}
```

## 练习

1、实现堆排序算法中的heapify操作。

2.实现堆排序算法。

3.比较堆排序算法和选择排序算法的运行时间。

## 答案

1、heapify操作可以这样实现：

```c
void heapify(int* array, int size, int i)
{
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < size && array[left] > array[largest])
        largest = left;

    if (right < size && array[right] > array[largest])
        largest = right;

    if (largest != i)
    {
        int temp = array[i];
        array[i] = array[largest];
        array[largest] = temp;

        heapify(array, size, largest);
    }
}
```

2、堆排序算法可以实现如下：

```c
void heap_sort(int* array, int size)
{
    for (int i = size / 2 - 1; i >= 0; i--)
        heapify(array, size, i);

    for (int i = size - 1; i >= 0; i--)
    {
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;

        heapify(array, i, 0);
    }
}
```

3、堆排序算法的运行时间是O(nlog(n))，而选择排序算法的运行时间是O(n^2)。