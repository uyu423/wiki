---
title: [JavaScript] 029：冒泡排序
description: 
published: true
date: 2023-02-10T07:32:37.190Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:32:30.682Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 029: Bubble Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-029-bubble-sort)
{.links-list}


# 冒泡排序

冒泡排序是一种简单的排序算法，其工作原理是重复遍历待排序列表，比较每对相邻项，如果顺序错误则交换它们。重复遍历列表，直到不需要交换为止，这表明列表已排序。该算法的名称来源于较小或较大元素“冒泡”到列表顶部的方式。

冒泡排序通常被认为是最简单的排序算法。但是，对于大型列表，它的效率也相对较低。不过，它适用于相对较小的列表。

## 概念

冒泡排序的工作原理是将列表中的每个元素与其旁边的元素进行比较，如果顺序错误则交换它们。重复该过程，直到所有元素都已排序。

例如，假设我们有以下列表：

```
[5, 1, 4, 2, 8]
```

我们首先比较前两个元素“5”和“1”，然后交换它们，因为“5”大于“1”。该列表将如下所示：

```
[1, 5, 4, 2, 8]
```

然后我们将比较接下来的两个元素“5”和“4”，并让它们保持相同的顺序，因为“5”不大于“4”。该列表将如下所示：

```
[1, 5, 4, 2, 8]
```

然后我们将比较接下来的两个元素“4”和“2”，并交换它们，因为“4”大于“2”。该列表将如下所示：

```
[1, 5, 2, 4, 8]
```

最后，我们将比较最后两个元素“4”和“8”，并让它们保持相同的顺序，因为“4”不大于“8”。该列表将如下所示：

```
[1, 5, 2, 4, 8]
```

由于我们不需要在最后一次传递时进行任何交换，因此我们可以得出结论，列表现在已排序。

## 代码示例

下面是 JavaScript 冒泡排序的简单实现：

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

## 复杂性

冒泡排序的时间复杂度在最坏情况下是**O(n^2)**，在最好情况下是**O(n)**。最坏的情况发生在列表被反向排序时，而最好的情况发生在列表已经排序时。

冒泡排序的空间复杂度是**O(1)**，因为只需要一个额外的内存空间。

## 何时使用冒泡排序

冒泡排序是对相对较小的列表进行排序的不错选择。如果你需要对一个几乎已经排好序的列表进行排序，这也是一个不错的选择。

## 何时不使用冒泡排序

冒泡排序不是排序大型列表的好选择，因为它效率不高。如果你需要对一个大列表进行排序，你应该使用不同的排序算法。

## 练习

1. 用你选择的编程语言实现冒泡排序。

2. 编写一个函数，将一个列表和一个整数作为参数，并使用冒泡排序对列表进行排序。该整数应指定应运行排序的次数。

3. 编写一个将列表作为参数的函数，如果列表已排序则返回“true”，否则返回“false”。

4. 编写一个函数，将一个列表和一个函数作为参数，并使用该函数对列表进行排序。该函数应采用两个参数，如果第一个参数小于第二个参数，则返回“-1”；如果两个参数相等，则返回“0”；如果第一个参数大于第二个参数，则返回“1”。

## 答案

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