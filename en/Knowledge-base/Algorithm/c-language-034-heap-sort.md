---
title: [C Language] 034: Heap Sort
description: 
published: true
date: 2023-02-13T14:33:12.717Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:33:05.787Z
---

- [[Lenguaje C] 034: Ordenar montón***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-034-heap-sort)
{.links-list}
- [[C语言]034：堆排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-034-heap-sort)
{.links-list}
- [[C언어] 034: 힙정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-034-heap-sort)
{.links-list}


# 034: Heap Sort

Heap sort is a comparison-based sorting algorithm. Heap sort can be thought of as an improved selection sort: like that algorithm, it divides its input into a sorted and an unsorted region, and it iteratively shrinks the unsorted region by extracting the largest element and moving that to the sorted region. The improvement consists of the use of a heap data structure rather than a linear-time search to find the maximum.

Heapsort was invented by J. W. J. Williams in 1964.[1] Heapsort is an in-place algorithm, but it is not a stable sort.

## Algorithm

A binary heap is a heap data structure that takes the form of a binary tree. Binary heaps are a common way of implementing priority queues.

The binary heap is defined as a binary tree with two additional constraints:

* Shape property: the tree is a complete binary tree; that is, all levels of the tree, except possibly the last one (deepest) are fully filled, and, if the last level of the tree is not complete, the nodes of that level are filled from left to right.
* Heap property: each node is greater than or equal to each of its children according to a comparison predicate defined for the heap.

The heap property allows the root node to be quickly accessed; it is guaranteed to be the largest (or smallest) element in the tree.

The algorithm has two phases: heap construction and sorting.

### Heap construction

The heap construction phase starts with an unordered array of numbers and transforms it into a binary heap. The array can be represented as a binary tree, where each node corresponds to an element of the array, and the children of each node are the elements of the array that are larger (or smaller) than the node's element.

The first step is to create a heap from the array. The heap construction algorithm is as follows:

1.  Start with an empty heap.

2.  Insert each element of the array into the heap, in any order.

3.  While the heap is not empty:

    a.  Remove the top element of the heap.

    b.  Insert the element into the sorted array.

4.  Return the sorted array.

The time complexity of the heap construction phase is O(n), where n is the number of elements in the array.

### Sorting

The sorting phase starts with a binary heap and transforms it into a sorted array. The sorting algorithm is as follows:

1.  While the heap is not empty:

    a.  Remove the top element of the heap.

    b.  Insert the element into the sorted array.

2.  Return the sorted array.

The time complexity of the sorting phase is O(nlog(n)), where n is the number of elements in the array. This is because, in each iteration of the while loop, the top element of the heap is removed and the heapify operation is performed. The heapify operation takes O(log(n)) time, and there are n iterations of the while loop, so the total time complexity is O(nlog(n)).

## Code example

The following is a heap sort implementation in the C programming language:

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

## Exercises

1.  Implement the heapify operation in the heap sort algorithm.

2.  Implement the heap sort algorithm.

3.  Compare the running time of the heap sort algorithm with the selection sort algorithm.

## Answers

1.  The heapify operation can be implemented as follows:

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

2.  The heap sort algorithm can be implemented as follows:

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

3.  The running time of the heap sort algorithm is O(nlog(n)), while the running time of the selection sort algorithm is O(n^2).