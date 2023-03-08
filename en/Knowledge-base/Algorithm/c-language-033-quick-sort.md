---
title: [C Language] 033: Quick Sort
description: 
published: true
date: 2023-02-13T13:32:41.292Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:32:34.315Z
---

- [[Lenguaje C] 033: Clasificación rápida***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-033-quick-sort)
{.links-list}
- [【C语言】033：快速排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-033-quick-sort)
{.links-list}
- [[C언어] 033: 퀵소트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-033-quick-sort)
{.links-list}


# 033: Quick Sort

Quick sort is a sorting algorithm that sorts an array by partitioning the array into two subarrays, then sorting the subarrays recursively.

The algorithm works by selecting a pivot element from the array, then partitioning the array around the pivot such that all elements less than the pivot are before it and all elements greater than the pivot are after it. The two subarrays are then sorted recursively.

Quick sort is a divide and conquer algorithm, meaning it breaks the problem down into smaller subproblems which it then solves recursively.

The time complexity of quick sort depends on the implementation, but the worst case is O(n^2) and the best case is O(n log n).

## Code Example

Here is a quick sort algorithm implemented in C.

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

## Explanation

The quick sort algorithm works by selecting a pivot element from the array, then partitioning the array around the pivot such that all elements less than the pivot are before it and all elements greater than the pivot are after it. The two subarrays are then sorted recursively.

The time complexity of quick sort depends on the implementation, but the worst case is O(n^2) and the best case is O(n log n).

## Related Exercises

1. Implement quick sort in your favorite programming language.

2. Compare the running time of quick sort and merge sort on various inputs.