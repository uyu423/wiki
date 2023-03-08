---
title: [JavaScript] 033: Quick Sort
description: 
published: true
date: 2023-02-10T11:32:34.124Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:32:27.725Z
---

- [[JavaScript] 033: Clasificación rápida***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-033-quick-sort)
{.links-list}
- [[JavaScript] 033：快速排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-033-quick-sort)
{.links-list}
- [[JavaScript] 033: 빠른 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-033-quick-sort)
{.links-list}


# JavaScript 033: Quick Sort

The quick sort algorithm is a sorting algorithm that sorts an array by partitioning the array into two subarrays, then sorting the subarrays recursively. The algorithm gets its name from the way it sorts the array: it partitions the array into two subarrays, then sorts the subarrays "quickly" by recursively applying the quick sort algorithm.

The quick sort algorithm is usually implemented using recursion. The base case of the recursion is when the array to be sorted has length 1 or 0. In this case, the array is already sorted. Otherwise, the array is partitioned into two subarrays, and the quick sort algorithm is applied recursively to each subarray.

The quick sort algorithm has a time complexity of O(n log n) on average, and a space complexity of O(log n). However, the worst case time complexity of the quick sort algorithm is O(n^2).

## Code Example

The following is a code example of the quick sort algorithm in JavaScript:

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## Exercise

The following is an exercise to test your understanding of the quick sort algorithm:

```javascript
// Write a function that sorts an array using the quick sort algorithm.

function quickSort(arr) {
  // Your code here
}
```

## Answer Code

The following is the answer code for the exercise:

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## Commentary

The quick sort algorithm is a very efficient sorting algorithm with a time complexity of O(n log n) on average. However, the worst case time complexity of the quick sort algorithm is O(n^2). Therefore, the quick sort algorithm is not the best sorting algorithm to use in all cases.