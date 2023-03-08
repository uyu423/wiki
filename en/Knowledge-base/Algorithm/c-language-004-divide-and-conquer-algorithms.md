---
title: [C Language] 004: Divide and Conquer Algorithms
description: 
published: true
date: 2023-02-12T15:32:24.371Z
tags: 
editor: markdown
dateCreated: 2023-02-12T15:32:17.498Z
---

- [[Lenguaje C] 004: Divide y vencerás Algoritmos***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-004-divide-and-conquer-algorithms)
{.links-list}
- [【C语言】004：分而治之算法***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-004-divide-and-conquer-algorithms)
{.links-list}
- [[C언어] 004: 분할정복 알고리즘***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-004-divide-and-conquer-algorithms)
{.links-list}


# C Language] 004: Divide and Conquer Algorithms

Divide and conquer algorithms are a powerful tool for solving problems. By dividing a problem into smaller subproblems, we can solve the problem more efficiently.

There are many divide and conquer algorithms, but we will focus on two of the most popular: the merge sort and the quick sort.

## The Merge Sort

The merge sort is a recursive algorithm that works by dividing a problem into smaller subproblems and then combining the solutions to those subproblems.

The merge sort works by dividing an array in half, sorting each half, and then merging the two halves together. The merge step is the key to the merge sort. In order to merge the two halves, we need to compare the elements of each half and then put them in the correct order.

Here is a pseudocode implementation of the merge sort:

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

The merge sort is a powerful sorting algorithm with a time complexity of O(n log n). However, it is not the fastest sorting algorithm.

## The Quick Sort

The quick sort is another popular divide and conquer algorithm. The quick sort works by selecting a pivot element and then partitioning the array around the pivot. The elements less than the pivot are placed in one array and the elements greater than the pivot are placed in another array. The quick sort then recursively sorts the two arrays.

Here is a pseudocode implementation of the quick sort:

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

The quick sort is a fast sorting algorithm with a time complexity of O(n log n).

## Conclusion

Divide and conquer algorithms are a powerful tool for solving problems. The merge sort and quick sort are two of the most popular divide and conquer algorithms.