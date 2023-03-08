---
title: [JavaScript] 031：选择排序
description: 
published: true
date: 2023-02-10T09:32:32.070Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:32:30.418Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 031: Selection Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-031-selection-sort)
{.links-list}


# JavaScript 031: 选择排序

选择排序是一种排序算法，具体来说是一种就地比较排序。它具有 O(n2) 的时间复杂度，使其在大型列表上效率低下，并且通常比类似的插入排序表现更差。选择排序以其简单性着称，在某些情况下，特别是在辅助内存有限的情况下，它比更复杂的算法具有性能优势。

该算法将输入列表分为两部分：已排序项目的子列表，它在列表的前面（左）从左到右构建，以及剩余待排序的项目的子列表，占据其余部分列表。最初，已排序的子列表为空，未排序的子列表是整个输入列表。该算法通过在未排序的子列表中找到最小（或最大，取决于排序顺序）元素，将其与最左边的未排序元素交换（交换）（将其按排序顺序排列），并将子列表边界向右移动一个元素来进行.

## 代码示例

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

## 选择排序伪代码

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

## 选择排序可视化

![选择排序可视化](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)

## 选择排序复杂度

选择排序的时间复杂度为 O(n2)。这意味着，在最坏的情况下，该算法将采取 n2 个步骤来对 n 个元素的列表进行排序。

## 相关练习

- [练习 1](https://repl.it/@ezkielelin/Selection-Sort# index.js): 在 JavaScript 中实现选择排序
- [练习 2](https://repl.it/@ezekielelin/Selection-Sort-Optimized# index.js): 为接近排序的数据优化选择排序

## 答案

- [答案 1](https://repl.it/@ezekielelin/Selection-Sort-Answer# index.js)
- [答案 2](https://repl.it/@ezekielelin/Selection-Sort-Optimized-Answer# index.js)