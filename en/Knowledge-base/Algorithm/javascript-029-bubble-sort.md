---
title: [JavaScript] 029: Bubble Sort
description: 
published: true
date: 2023-02-10T07:32:32.381Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:32:30.685Z
---

- [[JavaScript] 029: Clasificación de burbujas***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-029-bubble-sort)
{.links-list}
- [[JavaScript] 029：冒泡排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-029-bubble-sort)
{.links-list}
- [[JavaScript] 029: 버블 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-029-bubble-sort)
{.links-list}


# Bubble Sort

Bubble sort is a simple sorting algorithm that works by repeatedly stepping through the list to be sorted, comparing each pair of adjacent items and swapping them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted. The algorithm gets its name from the way smaller or larger elements "bubble" to the top of the list. 

Bubble sort is generally considered to be the simplest sorting algorithm. However, it is also relatively inefficient for large lists. It works well for relatively small lists, though. 

## Concept

Bubble sort works by comparing each element in the list with the element next to it and swapping them if they are in the wrong order. The process is repeated until all of the elements are sorted. 

For example, let's say we have the following list: 

```
[5, 1, 4, 2, 8]
```

We would first compare the first two elements, `5` and `1`, and swap them because `5` is greater than `1`. The list would then look like this: 

```
[1, 5, 4, 2, 8]
```

We would then compare the next two elements, `5` and `4`, and leave them in the same order because `5` is not greater than `4`. The list would then look like this: 

```
[1, 5, 4, 2, 8]
```

We would then compare the next two elements, `4` and `2`, and swap them because `4` is greater than `2`. The list would then look like this: 

```
[1, 5, 2, 4, 8]
```

Finally, we would compare the last two elements, `4` and `8`, and leave them in the same order because `4` is not greater than `8`. The list would then look like this: 

```
[1, 5, 2, 4, 8]
```

Since we did not need to make any swaps on the last pass, we can conclude that the list is now sorted. 

## Code Example

Here is a simple implementation of bubble sort in JavaScript: 

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

## Complexity

The time complexity of bubble sort is **O(n^2)** in the worst case and **O(n)** in the best case. The worst case occurs when the list is reverse sorted and the best case occurs when the list is already sorted. 

The space complexity of bubble sort is **O(1)** because only a single additional memory space is required. 

## When to Use Bubble Sort

Bubble sort is a good choice for sorting relatively small lists. It is also a good choice if you need to sort a list that is almost sorted. 

## When Not to Use Bubble Sort

Bubble sort is not a good choice for sorting large lists because it is not very efficient. If you need to sort a large list, you should use a different sorting algorithm. 

## Exercises

1. Implement bubble sort in your chosen programming language.

2. Write a function that takes a list and an integer as arguments and sorts the list using bubble sort. The integer should specify the number of times the sort should be run. 

3. Write a function that takes a list as an argument and returns `true` if the list is sorted and `false` if it is not. 

4. Write a function that takes a list and a function as arguments and sorts the list using the function. The function should take two arguments and return `-1` if the first argument is less than the second, `0` if the two arguments are equal, and `1` if the first argument is greater than the second. 

## Answers

1. 

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

2. 

```javascript
function bubbleSortNTimes(arr, n) {
  for (let i = 0; i < n; i++) {
    bubbleSort(arr);
  }
  return arr;
}
```

3. 

```javascript
function isSorted(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] > arr[i + 1]) {
      return false;
    }
  }
  return true;
}
```

4. 

```javascript
function bubbleSortWithComparator(arr, comparator) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (comparator(arr[j], arr[j + 1]) === 1) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```