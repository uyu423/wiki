---
title: [JavaScript] 033：快速排序
description: 
published: true
date: 2023-02-10T11:32:29.395Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:32:27.715Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 033: Quick Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-033-quick-sort)
{.links-list}


# JavaScript 033：快速排序

快速排序算法是一种排序算法，它通过将数组划分为两个子数组，然后递归地对子数组进行排序来对数组进行排序。该算法的名称来源于它对数组进行排序的方式：它将数组划分为两个子数组，然后通过递归地应用快速排序算法对子数组进行“快速”排序。

快速排序算法通常使用递归实现。递归的基本情况是要排序的数组的长度为 1 或 0。在这种情况下，数组已经排序。否则，数组被分成两个子数组，快速排序算法递归地应用于每个子数组。

快速排序算法的平均时间复杂度为 O(n log n)，空间复杂度为 O(log n)。然而，快速排序算法的最坏情况时间复杂度是 O(n^2)。

## 代码示例

以下是JavaScript中快速排序算法的代码示例：

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

## 锻炼

下面是一个练习来测试你对快速排序算法的理解：

```javascript
// Write a function that sorts an array using the quick sort algorithm.

function quickSort(arr) {
  // Your code here
}
```

## 答案代码

以下是练习的答案代码：

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

## 评论

快速排序算法是一种非常高效的排序算法，平均时间复杂度为 O(n log n)。然而，快速排序算法的最坏情况时间复杂度是 O(n^2)。因此，快速排序算法并不是适用于所有情况的最佳排序算法。