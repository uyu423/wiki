---
title: [C Language] 031: Selection Sort
description: 
published: true
date: 2023-02-13T11:32:17.863Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:32:10.903Z
---

- [[Lenguaje C] 031: Clasificación de selección***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-031-selection-sort)
{.links-list}
- [[C语言]031：选择排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-031-selection-sort)
{.links-list}
- [[C언어] 031: 선택정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-031-selection-sort)
{.links-list}


# 031: Selection Sort

The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from unsorted part and putting it at the beginning. The algorithm maintains two subarrays in a given array.

1) The subarray which is already sorted.
2) Remaining subarray which is unsorted.

In every iteration of selection sort, the minimum element (considering ascending order) from the unsorted subarray is picked and moved to the sorted subarray.

## pseudocode

```
procedure selectionSort( A : array of items )
   n = length(A)
   for i = 0 to n-1 do
      /* find the minimum element in the unsorted array */
       
      /* swap the found minimum element with the first element */
     
   done
```

## Complexity

### Time Complexity

Best Case: Ω(n^2)

Average Case: Θ(n^2)

Worst Case: O(n^2)

### Space Complexity

Worst Case: O(1)