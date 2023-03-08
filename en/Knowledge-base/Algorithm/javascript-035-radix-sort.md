---
title: [JavaScript] 035: Radix Sort
description: 
published: true
date: 2023-02-10T13:32:28.275Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:32:21.945Z
---

- [[JavaScript] 035: Clasificación Radix***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-035-radix-sort)
{.links-list}
- [[JavaScript] 035: 基数排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-035-radix-sort)
{.links-list}
- [[JavaScript] 035: 기수 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-035-radix-sort)
{.links-list}


# Radix Sort

Radix sort is a sorting algorithm that sorts numbers by processing the digits one at a time. It is a non-comparative sorting algorithm with asymptotic complexity O(kn), making it suitable for sorting large numbers.

## Algorithm

The basic idea behind radix sort is to take a number and sort it based on its digits. For example, given the number `42`, we can sort it based on the first digit (`4`), then the second digit (`2`).

To do this, we first need to find the largest digit in the number. In our example, the largest digit is `4`. We can then create an array with 10 buckets, one for each digit from `0` to `9`.

Next, we go through each number in the input array and place it in the correct bucket based on its first digit. In our example, `42` would be placed in bucket `4`.

Once we have placed all the numbers in their respective buckets, we can go through the buckets and put the numbers back into the original array in sorted order.

## Code Example

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

## Complexity

Radix sort has a time complexity of O(kn), where k is the number of digits in the largest number and n is the size of the input array.