---
title: [JavaScript] 032: Merge Sort
description: 
published: true
date: 2023-02-10T10:32:33.732Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:32:27.487Z
---

- [[JavaScript] 032: Clasificación por combinación***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-032-merge-sort)
{.links-list}
- [[JavaScript] 032：归并排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-032-merge-sort)
{.links-list}
- [[JavaScript] 032: 병합 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-032-merge-sort)
{.links-list}


# JavaScript 032: Merge Sort

Merge sort is a sorting algorithm that uses a divide-and-conquer strategy. It is a recursive algorithm that works by dividing an array into smaller subarrays, then sorting and merging those subarrays back together.

The merge sort algorithm can be written in pseudocode as follows:

```
function mergeSort(array)
  if array.length <= 1
    return array
  end
 
  middle = array.length / 2
  left = array.slice(0, middle)
  right = array.slice(middle)
 
  return merge(
    mergeSort(left),
    mergeSort(right)
  )
end
 
function merge(left, right)
  result = []
 
  while left.length && right.length
    if left[0] <= right[0]
      result.push(left.shift())
    else
      result.push(right.shift())
    end
  end
 
  return result.concat(left, right)
end
```

The merge sort algorithm has a time complexity of O(n log n). This is because the array is divided in half at each step, and there are O(log n) steps. Each step also involves a merge operation, which has a time complexity of O(n).

The space complexity of the merge sort algorithm is O(n). This is because at each step, a new array is created to store the sorted subarray.

## Code Example

Here is an example of the merge sort algorithm written in JavaScript:

```javascript
function mergeSort(array) {
  if (array.length <= 1) {
    return array;
  }
 
  const middle = Math.floor(array.length / 2);
  const left = array.slice(0, middle);
  const right = array.slice(middle);
 
  return merge(
    mergeSort(left),
    mergeSort(right)
  );
}
 
function merge(left, right) {
  const result = [];
 
  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
 
  return result.concat(left, right);
}
 
const array = [5, 3, 2, 1, 4];
console.log(mergeSort(array)); // [1, 2, 3, 4, 5]
```

## Explanation

The merge sort algorithm works by dividing an array into smaller subarrays, then sorting and merging those subarrays back together.

The algorithm starts by checking if the array is empty or has only one element. If so, it returns the array.

Otherwise, the array is divided in half at each step, and there are O(log n) steps. Each step also involves a merge operation, which has a time complexity of O(n).

The space complexity of the merge sort algorithm is O(n). This is because at each step, a new array is created to store the sorted subarray.

## Complexity Analysis

The time complexity of the merge sort algorithm is O(n log n). This is because the array is divided in half at each step, and there are O(log n) steps. Each step also involves a merge operation, which has a time complexity of O(n).

The space complexity of the merge sort algorithm is O(n). This is because at each step, a new array is created to store the sorted subarray.