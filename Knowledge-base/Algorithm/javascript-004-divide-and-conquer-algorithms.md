---
title: [JavaScript] 004: 분할 정복 알고리즘
description: 
published: true
date: 2023-02-09T06:32:32.009Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:32:30.418Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 004: Divide and Conquer Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-004-divide-and-conquer-algorithms)
{.links-list}


# 분할 정복 알고리즘

분할 정복 알고리즘은 문제 해결을 위한 강력한 도구입니다. 문제를 더 작은 조각으로 나누면 보다 효율적으로 문제를 해결할 수 있습니다.

분할 정복 알고리즘에는 다양한 유형이 있지만 모두 한 가지 공통점이 있습니다. 문제를 더 작은 하위 문제로 나누고 하위 문제를 해결한 다음 하위 문제에 대한 솔루션을 결합하여 원래 문제를 해결합니다.

## 기본 사항

간단한 예를 살펴보겠습니다. 다음과 같은 문제가 있다고 가정해 보겠습니다.

숫자 목록이 주어지면 목록에서 가장 큰 숫자를 찾으십시오.

분할 정복 알고리즘을 사용하여 이 문제를 해결할 수 있습니다. 먼저 문제를 더 작은 하위 문제로 나눕니다. 목록의 전반부를 본 다음 목록의 후반부를 보면 됩니다.

다음으로 하위 문제를 해결합니다. 이 경우 목록의 각 절반에서 가장 큰 숫자를 찾습니다.

마지막으로 하위 문제에 대한 솔루션을 결합하여 원래 문제를 해결합니다. 이 경우 목록의 각 절반에서 찾은 두 개의 가장 큰 숫자를 비교하고 둘 중 큰 값을 반환합니다.

## 코드 예

이제 좀 더 복잡한 예를 살펴보겠습니다. 다음과 같은 문제가 있다고 가정해 보겠습니다.

숫자 목록이 주어지면 목록에 있는 모든 숫자의 합을 구합니다.

분할 정복 알고리즘을 사용하여 이 문제를 해결할 수 있습니다. 먼저 문제를 더 작은 하위 문제로 나눕니다. 목록의 전반부를 본 다음 목록의 후반부를 보면 됩니다.

다음으로 하위 문제를 해결합니다. 이 경우 목록의 각 절반에 있는 모든 숫자의 합계를 찾습니다.

마지막으로 하위 문제에 대한 솔루션을 결합하여 원래 문제를 해결합니다. 이 경우 목록의 각 절반에서 찾은 두 합계를 더하고 결과를 반환합니다.

## 코드 예

방금 살펴본 분할 정복 알고리즘의 코드는 다음과 같습니다.

```javascript
function findSum(list) {
  // Base case: if the list is empty, the sum is 0
  if (list.length === 0) {
    return 0;
  }
  // Divide the problem into smaller subproblems
  var mid = Math.floor(list.length / 2);
  var left = list.slice(0, mid);
  var right = list.slice(mid);
  // Solve the subproblems
  var leftSum = findSum(left);
  var rightSum = findSum(right);
  // Combine the solutions to the subproblems
  return leftSum + rightSum;
}
```

## 복잡성 분석

분할 정복 알고리즘의 시간 복잡도는 문제의 크기, 하위 문제의 수 및 하위 문제 해결의 시간 복잡도에 따라 달라집니다.

최악의 경우 문제의 크기는 각 단계에서 절반으로 줄어들고 하위 문제의 수는 두 배가 됩니다. 하위 문제 해결의 시간 복잡도가 일정하면 분할 정복 알고리즘의 시간 복잡도는 O(n)입니다.

그러나 하위 문제를 해결하는 시간 복잡도가 일정하지 않으면 분할 정복 알고리즘의 시간 복잡도가 더 복잡해질 수 있습니다. 예를 들어 하위 문제 해결의 시간 복잡도가 O(n)이면 분할 정복 알고리즘의 시간 복잡도는 O(nlogn)입니다.

## 결론

분할 정복 알고리즘은 문제 해결을 위한 강력한 도구입니다. 문제를 더 작은 조각으로 나누면 보다 효율적으로 문제를 해결할 수 있습니다. 분할 정복 알고리즘에는 다양한 유형이 있지만 모두 한 가지 공통점이 있습니다. 문제를 더 작은 하위 문제로 나누고 하위 문제를 해결한 다음 하위 문제에 대한 솔루션을 결합하여 원래 문제를 해결합니다.