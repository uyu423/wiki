---
title: [JavaScript] 031: Selection Sort
description: 
published: true
date: 2023-02-10T09:32:36.730Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:32:30.421Z
---

- [[JavaScript] 031: Clasificación de selección***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-031-selection-sort)
{.links-list}
- [[JavaScript] 031：选择排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-031-selection-sort)
{.links-list}
- [[JavaScript] 031: 선택 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-031-selection-sort)
{.links-list}


# JavaScript 031: Selection Sort

Selection sort is a sorting algorithm, specifically an in-place comparison sort. It has O(n2) time complexity, making it inefficient on large lists, and generally performs worse than the similar insertion sort. Selection sort is noted for its simplicity, and it has performance advantages over more complicated algorithms in certain situations, particularly where auxiliary memory is limited.

The algorithm divides the input list into two parts: the sublist of items already sorted, which is built up from left to right at the front (left) of the list, and the sublist of items remaining to be sorted that occupy the rest of the list. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list. The algorithm proceeds by finding the smallest (or largest, depending on sorting order) element in the unsorted sublist, exchanging (swapping) it with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the right.

## Code Examples

```javascript
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) {
        min = j;
      }
    }
    if (i !== min) {
      [arr[i], arr[min]] = [arr[min], arr[i]];
    }
  }
  return arr;
}
```

## Selection Sort Pseudocode

```
procedure selectionSort( A : list of sortable items )
   n = length(A)
   for i = 1 to n - 1
   /* set current element as minimum*/
      minIndex = i    
   /* check the element to be minimum */
 
      for j = i+1 to n      
         if A[j] < A[minIndex]   
            minIndex = j;
      end if
   end for
   /* swap the minimum element with the current element*/
   if indexMin != i  then
      swap A[minIndex] with A[i]
   end if
   end for
end procedure
```

## Selection Sort Visualization

![Selection Sort Visualization](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)

## Selection Sort Complexity

Selection sort has a time complexity of O(n2). This means that, in the worst case scenario, the algorithm will take n2 steps to sort a list of n elements.

## Related Exercises

- [Exercise 1](https://repl.it/@ezekielelin/Selection-Sort#index.js): Implement selection sort in JavaScript
- [Exercise 2](https://repl.it/@ezekielelin/Selection-Sort-Optimized#index.js): Optimize selection sort for nearly sorted data

## Answers

- [Answer 1](https://repl.it/@ezekielelin/Selection-Sort-Answer#index.js)
- [Answer 2](https://repl.it/@ezekielelin/Selection-Sort-Optimized-Answer#index.js)