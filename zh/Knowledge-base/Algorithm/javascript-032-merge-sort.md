---
title: [JavaScript] 032：归并排序
description: 
published: true
date: 2023-02-10T10:32:29.066Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:32:27.476Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 032: Merge Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-032-merge-sort)
{.links-list}


# JavaScript 032：归并排序

合并排序是一种使用分而治之策略的排序算法。它是一种递归算法，其工作原理是将数组划分为更小的子数组，然后对这些子数组进行排序和合并。

归并排序算法可以用伪代码写成如下：

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

合并排序算法的时间复杂度为 O(n log n)。这是因为数组在每一步都被分成两半，并且有 O(log n) 步。每个步骤还涉及合并操作，其时间复杂度为 O(n)。

归并排序算法的空间复杂度为 O(n)。这是因为在每一步，都会创建一个新数组来存储排序后的子数组。

## 代码示例

下面是一个用 JavaScript 编写的归并排序算法的例子：

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

## 解释

合并排序算法的工作原理是将一个数组划分为更小的子数组，然后对这些子数组进行排序并将它们重新合并在一起。

该算法首先检查数组是否为空或只有一个元素。如果是这样，它返回数组。

否则，数组在每一步都被分成两半，并且有 O(log n) 步。每个步骤还涉及合并操作，其时间复杂度为 O(n)。

归并排序算法的空间复杂度为 O(n)。这是因为在每一步，都会创建一个新数组来存储排序后的子数组。

## 复杂度分析

合并排序算法的时间复杂度为 O(n log n)。这是因为数组在每一步都被分成两半，并且有 O(log n) 步。每个步骤还涉及合并操作，其时间复杂度为 O(n)。

归并排序算法的空间复杂度为 O(n)。这是因为在每一步，都会创建一个新数组来存储排序后的子数组。