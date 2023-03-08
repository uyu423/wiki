---
title: [JavaScript] 030：插入排序
description: 
published: true
date: 2023-02-10T08:32:39.381Z
tags: 
editor: markdown
dateCreated: 2023-02-10T08:32:37.749Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 030: Insertion Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-030-insertion-sort)
{.links-list}


# 插入排序

插入排序是一种排序算法，一次构建一个排序数组的一个元素。与其他排序算法（如快速排序、堆排序或合并排序）相比，它在大型列表上的效率要低得多。但是，插入排序有几个优点：

简单实现：Jon Bentley 在 Programming Pearls[2] 中展示了一个三行 C 版本
对（相当）小的数据集有效，很像其他二次排序算法
比选择排序或冒泡排序更有效
稳定的;即，不改变具有相同键的元素的相对顺序
到位;即，只需要恒定数量的 O(1) 额外内存空间
在线的;即，可以在收到列表时对其进行排序

## 算法

插入排序迭代，每次重复消耗一个输入元素，并增长一个排序的输出列表。在每次迭代中，插入排序从输入数据中删除一个元素，找到它在排序列表中所属的位置，并将其插入到那里。它重复直到没有输入元素剩余。

排序通常是就地完成的，通过迭代数组，在它后面增加排序列表。在每个数组位置，它检查那里的值与排序列表中的最大值（恰好在它旁边，在先前检查的数组位置中）。如果更大，它会将元素留在原地并移动到下一个。如果较小，它会在排序列表中找到正确的位置，将所有较大的值向上移动以形成一个空间，然后插入到正确的位置。

## 复杂性

### 最坏的情况下

最坏情况下的输入是一个按相反顺序排序的数组。要以相反顺序对大小为 n 的数组进行排序，插入排序将需要进行 n^2 次比较和交换。因此，最坏情况的时间复杂度为 O(n^2)。

### 最佳案例

最好的情况输入是一个已经排序的数组。在这种情况下，插入排序将进行 n-1 次比较，但不会进行交换。因此，最佳情况的时间复杂度为 O(n)。

## 代码示例

### JavaScript

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

### Python

```python
def insertion_sort(array):
  for i in range(1, len(array)):
    current = array[i]
    j = i - 1
    while j >= 0 and array[j] > current:
      array[j + 1] = array[j]
      j -= 1
    array[j + 1] = current
  return array
```

## 相关练习

- [ ] 练习 1：实现插入排序
- [ ] 练习 2：使用插入排序对字符串数组进行排序

## 答案

- [ ] 答案 1：

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

- [ ] 答案 2：

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```