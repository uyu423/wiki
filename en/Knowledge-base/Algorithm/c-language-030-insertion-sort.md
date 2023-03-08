---
title: [C Language] 030: Insertion Sort
description: 
published: true
date: 2023-02-13T00:17:38.328Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:17:31.317Z
---

- [[Lenguaje C] 030: Clasificación por inserción***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-030-insertion-sort)
{.links-list}
- [[C语言]030：插入排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-030-insertion-sort)
{.links-list}
- [[C언어] 030: 삽입정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-030-insertion-sort)
{.links-list}


# 030: Insertion Sort

Insertion sort is a simple sorting algorithm that works by taking in new items one at a time and inserting them in the correct position in the already sorted list. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort. However, it is very efficient for small lists, and is often used as part of more sophisticated algorithms. It is also a stable sort, meaning that it preserves the order of items with equal keys.

Here is a simple example of insertion sort in action. We start with an unsorted list of numbers:

```
5, 2, 4, 6, 1, 3
```

To sort this list, we first take the second item (`2`) and insert it in the correct position in the already sorted list (`5, 2, 4, 6, 1, 3`). Then we take the third item (`4`) and insert it in the correct position in the already sorted list (`2, 4, 5, 6, 1, 3`). We continue in this way until the entire list is sorted:

```
1, 2, 3, 4, 5, 6
```

The insertion sort algorithm can be implemented in a few lines of code. Here is a simple implementation in C:

```C
void insertion_sort(int array[], int n)
{
    int i, j, temp;
    
    for (i = 1; i < n; i++) {
        temp = array[i];
        j = i-1;
        while (j >= 0 && array[j] > temp) {
            array[j+1] = array[j];
            j--;
        }
        array[j+1] = temp;
    }
}
```

This implementation sorts the array in place, meaning that it sorts the array in-place without creating a new array.

To test this implementation, we can create an array of random numbers and sort it using the insertion sort algorithm. We can then print the sorted array to see if it is indeed sorted:

```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void insertion_sort(int array[], int n);

int main(void)
{
    int i, n = 10;
    int array[n];
    
    srand(time(NULL));
    
    for (i = 0; i < n; i++) {
        array[i] = rand() % 100;
    }
    
    insertion_sort(array, n);
    
    for (i = 0; i < n; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
    
    return 0;
}
```

Running this code gives us the following output:

```
2 4 5 8 12 23 37 38 39 45 
```

We can see that the array is indeed sorted.

## Complexity

The worst case time complexity of insertion sort is `O(n^2)`. This occurs when the array is sorted in reverse order. The best case time complexity is `O(n)` and occurs when the array is already sorted.

Insertion sort is a stable sort, meaning that it preserves the order of items with equal keys. It is also an in-place sort, meaning that it sorts the array in place without creating a new array.

## Exercises

1. Implement the insertion sort algorithm in your favorite programming language.

2. Modify the insertion sort algorithm to sort a singly linked list.

3. Modify the insertion sort algorithm to sort an array of strings.