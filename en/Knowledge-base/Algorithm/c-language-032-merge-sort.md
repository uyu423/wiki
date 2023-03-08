---
title: [C Language] 032: Merge Sort
description: 
published: true
date: 2023-02-13T12:34:05.635Z
tags: 
editor: markdown
dateCreated: 2023-02-13T12:33:58.559Z
---

- [[Lenguaje C] 032: Clasificación por combinación***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-032-merge-sort)
{.links-list}
- [[C语言]032：归并排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-032-merge-sort)
{.links-list}
- [[C언어] 032: 병합 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-032-merge-sort)
{.links-list}


# 032: Merge Sort

Merge sort is a sorting algorithm that uses a divide-and-conquer strategy. It is one of the most efficient sorting algorithms with a time complexity of O(n log n).

The merge sort algorithm works by dividing the array into two halves, sorting each half, and then merging the two halves together. The merge step is the most important part of the merge sort algorithm.

## How does the merge step work?

The merge step works by taking two sorted arrays and merging them together into a single sorted array. The merge step is the most important part of the merge sort algorithm.

To merge two sorted arrays, we can use a simple algorithm called the merge algorithm. The merge algorithm works by taking two sorted arrays and merging them together into a single sorted array.

The merge algorithm works by comparing the first element of each array. The smaller of the two elements is then added to the merged array. The merge algorithm then repeats this process until one of the arrays is empty. The remaining elements of the other array are then added to the merged array.

## Code example

Here is a simple implementation of the merge sort algorithm in C.

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

## Exercise

1. Implement the merge sort algorithm in your favorite programming language.

2. Use the merge sort algorithm to sort an array of integers in ascending order.

3. Use the merge sort algorithm to sort an array of strings in alphabetical order.

## Answers

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