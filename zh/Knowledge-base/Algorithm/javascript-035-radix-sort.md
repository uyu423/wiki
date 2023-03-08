---
title: [JavaScript] 035: 基数排序
description: 
published: true
date: 2023-02-10T13:32:23.496Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:32:21.941Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 035: Radix Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-035-radix-sort)
{.links-list}


# 基数排序

基数排序是一种排序算法，它通过一次处理一个数字来对数字进行排序。它是一种渐近复杂度为 O(kn) 的非比较排序算法，适用于对大数进行排序。

## 算法

基数排序背后的基本思想是获取一个数字并根据其数字对其进行排序。例如，给定数字“42”，我们可以根据第一个数字 (“4”)，然后是第二个数字 (“2”) 对其进行排序。

为此，我们首先需要找到数字中最大的数字。在我们的示例中，最大的数字是“4”。然后我们可以创建一个包含 10 个桶的数组，每个桶对应从“0”到“9”的每个数字。

接下来，我们遍历输入数组中的每个数字，并根据其第一个数字将其放入正确的桶中。在我们的示例中，“42”将被放置在存储桶“4”中。

一旦我们将所有数字放入各自的桶中，我们就可以遍历桶并将数字按排序顺序放回原始数组。

## 代码示例

```javascript
function radixSort(arr) {
  // find the largest digit in the array
  let max = Math.max(...arr);

  // create an array of 10 buckets, one for each digit from 0 to 9
  let buckets = Array.from({ length: 10 }, () => []);

  // go through each number in the input array and place it in the
  // correct bucket based on its first digit
  for (let num of arr) {
    let digit = Math.floor(num / 10);
    buckets[digit].push(num);
  }

  // go through the buckets and put the numbers back into the original
  // array in sorted order
  let i = 0;
  for (let bucket of buckets) {
    for (let num of bucket) {
      arr[i++] = num;
    }
  }

  return arr;
}
```

## 复杂性

基数排序的时间复杂度为 O(kn)，其中 k 是最大数的位数，n 是输入数组的大小。