---
title: [C Language] 029: Bubble Sort
description: 
published: true
date: 2023-02-13T10:33:05.601Z
tags: 
editor: markdown
dateCreated: 2023-02-13T10:32:58.605Z
---

- [[Lenguaje C] 029: Clasificación de burbuja***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-029-bubble-sort)
{.links-list}
- [【C语言】029：冒泡排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-029-bubble-sort)
{.links-list}
- [[C언어] 029: 버블정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-029-bubble-sort)
{.links-list}


# 029: Bubble Sort

Bubble sort is a sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order. The name bubble sort comes from the fact that smaller elements "bubble" to the top of the list while the larger elements sink to the bottom. 

Bubble sort is one of the simplest sorting algorithms but it is also one of the most inefficient. It has a worst-case and average complexity of **O(n^2)** where **n** is the number of items being sorted. Despite its simplicity and inefficiency, bubble sort is still used in some cases because it is easy to implement.

## Algorithm

The basic idea behind bubble sort is to compare each element with its adjacent element and swap them if they are in the wrong order. This process is repeated until the whole list is sorted. 

Consider the following list of numbers that needs to be sorted in ascending order: 

[5, 1, 4, 2, 8]

We compare the first two elements, 5 and 1, and swap them since 5 is greater than 1. The list now becomes:

[1, 5, 4, 2, 8]

We compare the next two elements, 5 and 4, and swap them since 5 is greater than 4. The list now becomes:

[1, 4, 5, 2, 8]

We compare the next two elements, 5 and 2, and swap them since 5 is greater than 2. The list now becomes:

[1, 4, 2, 5, 8]

We compare the next two elements, 5 and 8, and do not swap them since 5 is not greater than 8. The list now becomes:

[1, 4, 2, 5, 8]

At this point, the list is already sorted so we can stop. 

The following animation shows the complete bubble sort process for the list [5, 1, 4, 2, 8]:

![Bubble Sort Animation](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)

## Complexity

As mentioned earlier, bubble sort has a worst-case and average complexity of **O(n^2)**. This is because the algorithm needs to compare each element with all the other elements in the list and swap them if they are in the wrong order. 

The best case scenario for bubble sort occurs when the list is already sorted. In this case, the algorithm will not need to do any swapping and the complexity will be **O(n)**. 

## Implementation

Here is a simple implementation of bubble sort in the C programming language:

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

## Exercise

1. Implement the bubble sort algorithm in your own programming language.

2. Modify the bubble sort algorithm so that it stops early if the list is already sorted.

## Answers

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