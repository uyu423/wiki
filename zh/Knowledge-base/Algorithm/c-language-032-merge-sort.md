---
title: [C语言]032：归并排序
description: 
published: true
date: 2023-02-13T12:34:00.295Z
tags: 
editor: markdown
dateCreated: 2023-02-13T12:33:58.555Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 032: Merge Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-032-merge-sort)
{.links-list}


# 032：归并排序

合并排序是一种使用分而治之策略的排序算法。它是最有效的排序算法之一，时间复杂度为 O(n log n)。

合并排序算法的工作原理是将数组分成两半，对每一半进行排序，然后将两半合并在一起。合并步骤是合并排序算法中最重要的部分。

## 合并步骤如何工作？

合并步骤的工作原理是采用两个排序数组并将它们合并到一个排序数组中。合并步骤是合并排序算法中最重要的部分。

要合并两个排序数组，我们可以使用一种称为合并算法的简单算法。合并算法的工作原理是将两个排序数组合并成一个排序数组。

合并算法通过比较每个数组的第一个元素来工作。然后将两个元素中较小的一个添加到合并后的数组中。合并算法然后重复此过程，直到其中一个数组为空。然后将另一个数组的剩余元素添加到合并后的数组中。

## 代码示例

下面是 C 中归并排序算法的简单实现。

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

## 锻炼

1. 用你喜欢的编程语言实现归并排序算法。

2. 使用归并排序算法对整数数组进行升序排序。

3. 使用合并排序算法按字母顺序对字符串数组进行排序。

## 答案

1.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

2.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

3.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
void merge(char **array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    char **L = malloc(sizeof(char*)*n1);
    char **R = malloc(sizeof(char*)*n2);
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (strcmp(L[i], R[j]) <= 0)
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
 
    free(L);
    free(R);
}
 
void mergeSort(char **array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    char *array[] = {"c", "a", "e", "b", "d"};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```