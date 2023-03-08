---
title: [JavaScript] 034：堆排序
description: 
published: true
date: 2023-02-10T12:32:35.097Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:32:33.485Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 034: Heap Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-034-heap-sort)
{.links-list}


# 堆排序

堆排序是一种基于比较的排序算法。堆排序可以看作是一种改进的选择排序：与选择排序一样，堆排序将其输入分为已排序区域和未排序区域，并通过从中提取最大元素并将其插入已排序区域来迭代缩小未排序区域。改进包括使用堆数据结构而不是线性时间搜索来查找最大值。

Heapsort 是一种就地算法，但它不是一种稳定的排序。

## 算法

堆是一种树状数据结构，其中子节点相对于父节点具有排序顺序。有两种类型的堆：最小堆和最大堆。在最小堆中，根节点的值小于或等于子节点的值。在最大堆中，根节点的值大于或等于子节点的值。

堆排序算法可以分为两部分：

1. 第一部分涉及从输入数组构建堆。此步骤也称为堆化。
2. 第二部分涉及从堆中逐个提取元素并将它们插入到已排序的数组中。

第一部分可以使用最小堆或最大堆来完成。在本文中，我们将使用最大堆。

heapify 算法从根节点开始向下移动，将当前节点的值与其子节点的值进行比较。如果当前节点的值小于子节点的值，则交换两个节点。重复此过程，直到当前节点大于或等于它的两个子节点（或到达树的底部）。

该算法的第二部分涉及重复从堆中提取最大元素并将其插入到排序数组中。这是通过将堆的根节点与数组中的最后一个元素交换，然后堆化树来完成的。重复此过程，直到堆为空。

## 复杂性

heapify 的时间复杂度为 O(log n)，整个堆排序算法的时间复杂度为 O(n log n)。

## 代码示例

下面是堆排序算法的 C++ 实现。

```C++
#include <iostream>
#include <vector>

using namespace std;

void heapify(vector<int>& A, int n, int i)
{
    int largest = i;
    int l = 2*i + 1;
    int r = 2*i + 2;

    if (l < n && A[l] > A[largest])
        largest = l;

    if (r < n && A[r] > A[largest])
        largest = r;

    if (largest != i)
    {
        swap(A[i], A[largest]);
        heapify(A, n, largest);
    }
}

void heapSort(vector<int>& A, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(A, n, i);

    for (int i=n-1; i>=0; i--)
    {
        swap(A[0], A[i]);
        heapify(A, i, 0);
    }
}

int main()
{
    vector<int> A = {4, 10, 3, 5, 1};
    int n = A.size();

    heapSort(A, n);

    for (int i=0; i<n; ++i)
        cout << A[i] << " ";

    return 0;
}
```

## 练习

1. 用你选择的编程语言实现 heapify 和 heapSort 算法。

2. 使用 heapify 算法从以下数组构建最大堆：

```
[4, 10, 3, 5, 1]
```

3.使用heapSort算法对以下数组进行排序：

```
[4, 10, 3, 5, 1]
```

4. heapify 和heapSort 算法的时间复杂度是多少？

5. heapify 和 heapSort 算法的空间复杂度是多少？