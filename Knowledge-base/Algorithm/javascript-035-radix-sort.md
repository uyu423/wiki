---
title: [JavaScript] 035: 기수 정렬
description: 
published: true
date: 2023-02-10T13:32:23.484Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:32:21.938Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 035: Radix Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-035-radix-sort)
{.links-list}


# 기수 정렬

기수 정렬은 숫자를 한 번에 하나씩 처리하여 숫자를 정렬하는 정렬 알고리즘입니다. 점근적 복잡도가 O(kn)인 비비교 정렬 알고리즘이므로 큰 수를 정렬하는 데 적합합니다.

## 알고리즘

기수 정렬의 기본 아이디어는 숫자를 가져와 숫자를 기준으로 정렬하는 것입니다. 예를 들어 숫자 '42'가 주어지면 첫 번째 숫자('4')를 기준으로 정렬한 다음 두 번째 숫자('2')를 기준으로 정렬할 수 있습니다.

이렇게 하려면 먼저 숫자에서 가장 큰 숫자를 찾아야 합니다. 이 예에서 가장 큰 숫자는 '4'입니다. 그런 다음 `0`에서 `9`까지의 각 숫자에 대해 하나씩 10개의 버킷이 있는 배열을 만들 수 있습니다.

다음으로 입력 배열의 각 숫자를 살펴보고 첫 번째 숫자를 기준으로 올바른 버킷에 배치합니다. 이 예에서 '42'는 버킷 '4'에 배치됩니다.

각 버킷에 모든 숫자를 배치한 후에는 버킷을 살펴보고 숫자를 정렬된 순서로 원래 배열에 다시 넣을 수 있습니다.

## 코드 예

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

## 복잡성

기수 정렬의 시간 복잡도는 O(kn)입니다. 여기서 k는 가장 큰 숫자의 자릿수이고 n은 입력 배열의 크기입니다.