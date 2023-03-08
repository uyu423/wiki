---
title: [JavaScript] 030: Insertion Sort
description: 
published: true
date: 2023-02-10T08:32:44.070Z
tags: 
editor: markdown
dateCreated: 2023-02-10T08:32:37.752Z
---

- [[JavaScript] 030: ordenación por inserción***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-030-insertion-sort)
{.links-list}
- [[JavaScript] 030：插入排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-030-insertion-sort)
{.links-list}
- [[JavaScript] 030: 삽입 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-030-insertion-sort)
{.links-list}


# Insertion Sort

Insertion sort is a sorting algorithm that builds up a sorted array one element at a time. It is much less efficient on large lists than other sort algorithms such as quicksort, heapsort, or merge sort. However, insertion sort provides several advantages:

Simple implementation: Jon Bentley shows a three-line C version in Programming Pearls[2]
Efficient for (quite) small data sets, much like other quadratic sorting algorithms
More efficient than selection sort or bubble sort
Stable; i.e., does not change the relative order of elements with equal keys
In-place; i.e., only requires a constant amount O(1) of additional memory space
Online; i.e., can sort a list as it receives it

## The Algorithm

Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there. It repeats until no input elements remain.

Sorting is typically done in-place, by iterating up the array, growing the sorted list behind it. At each array-position, it checks the value there against the largest value in the sorted list (which happens to be next to it, in the previous array-position checked). If larger, it leaves the element in place and moves to the next. If smaller, it finds the correct position within the sorted list, shifts all the larger values up to make a space, and inserts into that correct position.

## Complexity

### Worst Case

The worst case input is an array sorted in reverse order. To sort an array of size n in reverse order, insertion sort will need to make n^2 comparisons and swaps. Therefore, the time complexity for the worst case scenario is O(n^2).

### Best Case

The best case input is an array that is already sorted. In this case, insertion sort will make n-1 comparisons but no swaps. Therefore, the time complexity for the best case scenario is O(n).

## Code Examples

### JavaScript

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

### Python

```python
def insertion_sort(array):
  for i in range(1, len(array)):
    current = array[i]
    j = i - 1
    while j >= 0 and array[j] > current:
      array[j + 1] = array[j]
      j -= 1
    array[j + 1] = current
  return array
```

## Related Exercises

- [ ] Exercise 1: Implement insertion sort
- [ ] Exercise 2: Sort an array of strings using insertion sort

## Answers

- [ ] Answer 1: 

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

- [ ] Answer 2: 

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```