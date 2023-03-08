---
title: [JavaScript] 034: Heap Sort
description: 
published: true
date: 2023-02-10T12:32:39.827Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:32:33.496Z
---

- [[JavaScript] 034: Ordenar montón***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-034-heap-sort)
{.links-list}
- [[JavaScript] 034：堆排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-034-heap-sort)
{.links-list}
- [[JavaScript] 034: 힙 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-034-heap-sort)
{.links-list}


# Heap Sort

Heap sort is a comparison-based sorting algorithm. Heap sort can be thought of as an improved selection sort: like selection sort, heapsort divides its input into a sorted and an unsorted region, and it iteratively shrinks the unsorted region by extracting the largest element from it and inserting it into the sorted region. The improvement consists of the use of a heap data structure rather than a linear-time search to find the maximum.

Heapsort is an in-place algorithm, but it is not a stable sort.

## Algorithm

A heap is a tree-like data structure in which the child nodes have a sort order with respect to the parent node. There are two types of heaps: min heap and max heap. In a min heap, the value of the root node is less than or equal to the values of the child nodes. In a max heap, the value of the root node is greater than or equal to the values of the child nodes.

The heap sort algorithm can be divided into two parts:

1. The first part involves building a heap from the input array. This step is also known as heapify.
2. The second part involves extracting the elements from the heap one by one and inserting them into the sorted array.

The first part can be done using either a min heap or a max heap. In this article, we will use a max heap.

The heapify algorithm starts at the root node and moves down the tree, comparing the value of the current node with the values of its child nodes. If the value of the current node is less than the value of a child node, the two nodes are swapped. This process is repeated until the current node is greater than or equal to both of its child nodes (or the bottom of the tree is reached).

The second part of the algorithm involves repeatedly extracting the maximum element from the heap and inserting it into the sorted array. This is done by swapping the root node of the heap with the last element in the array, and then heapifying the tree. This process is repeated until the heap is empty.

## Complexity

The time complexity of heapify is O(log n) and the time complexity of the overall heap sort algorithm is O(n log n).

## Code Example

The following is a C++ implementation of the heap sort algorithm.

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

## Exercises

1. Implement the heapify and heapSort algorithms in your chosen programming language.

2. Use the heapify algorithm to build a max heap from the following array:

```
[4, 10, 3, 5, 1]
```

3. Use the heapSort algorithm to sort the following array:

```
[4, 10, 3, 5, 1]
```

4. What is the time complexity of the heapify and heapSort algorithms?

5. What is the space complexity of the heapify and heapSort algorithms?