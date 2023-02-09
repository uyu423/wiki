---
title: [자바스크립트 학습] 002: 시간 복잡도
description: 
published: true
date: 2023-02-09T04:33:09.115Z
tags: 
editor: markdown
dateCreated: 2023-02-09T04:33:09.115Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[Learning in JavaScript] 002: Time Complexity***English** document is available*](/en/Knowledge-base/Algorithm/learning-in-javascript-002-time-complexity)
{.links-list}


# 자바스크립트 학습: 002 시간 복잡도

컴퓨터 과학에서 알고리즘의 시간 복잡도는 실행하는 데 걸리는 시간이며 수행된 작업 수로 측정됩니다. 시간 복잡도는 일반적으로 입력 크기 n의 함수로 표현됩니다. 예를 들어 크기 n의 입력에서 실행하는 데 몇 초가 걸리는 알고리즘의 시간 복잡도는 O(n^2)입니다.

시간 복잡도에는 최악의 경우와 평균의 두 가지 유형이 있습니다. 최악의 경우 시간 복잡도는 실행하는 데 가장 많은 시간이 걸리는 크기 n의 입력인 최악의 경우 입력에서 알고리즘이 실행되는 데 걸리는 시간입니다. 평균 사례 시간 복잡도는 알고리즘이 평균 사례 입력에서 실행되는 데 걸리는 시간입니다. 평균 사례 입력은 실행하는 데 평균 시간이 걸리는 크기 n의 입력입니다.

알고리즘의 시간 복잡도는 데이터 구조의 선택, 연산이 수행되는 순서 및 사용되는 알고리즘 설계 패턴에 의해 영향을 받을 수 있습니다.

## 데이터 구조

데이터 구조의 선택은 알고리즘의 시간 복잡도에 영향을 줄 수 있습니다. 예를 들어 배열에서 요소를 검색하는 문제를 생각해 보십시오. 배열이 정렬되지 않은 경우 전체 배열을 검색해야 하므로 검색 알고리즘의 최악의 경우 시간 복잡도는 O(n)입니다. 그러나 배열이 정렬된 경우 검색 알고리즘의 최악의 경우 시간 복잡도는 O(log n)입니다. 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

## 작업 순서

작업이 수행되는 순서도 알고리즘의 시간 복잡도에 영향을 줄 수 있습니다. 예를 들어, 배열 정렬 문제를 생각해 보십시오. 정렬 알고리즘의 최악의 경우 시간 복잡도는 O(n log n)입니다. 배열을 n log n 파티션으로 나누고 각 파티션을 정렬해야 하기 때문입니다. 그러나 배열이 이미 정렬된 경우 정렬 알고리즘의 최악의 경우 시간 복잡도는 O(n)입니다. 배열을 파티션으로 나눌 필요가 없고 각 요소를 배열의 다음 요소와 비교할 수 있기 때문입니다.

## 알고리즘 설계 패턴

알고리즘의 시간 복잡도를 개선하는 데 사용할 수 있는 알고리즘 설계 패턴에는 여러 가지가 있습니다. 이러한 디자인 패턴에는 다음이 포함됩니다.

- 분할 및 정복: 이 디자인 패턴은 문제를 더 작은 하위 문제로 나누고, 하위 문제를 해결하고, 하위 문제에 대한 솔루션을 결합하여 원래 문제를 해결하는 데 사용됩니다.

- Greedy: 이 디자인 패턴은 전역 최적을 찾기 위해 각 단계에서 로컬 최적 선택을 만드는 데 사용됩니다.

- 동적 프로그래밍: 이 디자인 패턴은 문제를 더 작은 하위 문제로 나누고, 하위 문제를 해결하고, 하위 문제에 대한 솔루션을 테이블에 저장하는 데 사용됩니다. 그런 다음 하위 문제에 대한 솔루션을 재사용하여 원래 문제를 해결할 수 있습니다.

- Brute force: 이 디자인 패턴은 문제에 대한 가능한 모든 솔루션을 시도하고 최상의 솔루션을 선택하는 데 사용됩니다.

## 코드 예제

다음은 시간 복잡도가 O(n log n)인 정렬 알고리즘의 코드 예제입니다.

```javascript
function sort(array) {
  if (array.length <= 1) {
    return array;
  }

  const pivot = array[0];
  const left = [];
  const right = [];

  for (let i = 1; i < array.length; i++) {
    const element = array[i];

    if (element <= pivot) {
      left.push(element);
    } else {
      right.push(element);
    }
  }

  return [...sort(left), pivot, ...sort(right)];
}
```

다음은 시간 복잡도가 O(n)인 정렬 알고리즘의 코드 예제입니다.

```javascript
function sort(array) {
  for (let i = 0; i < array.length - 1; i++) {
    for (let j = i + 1; j < array.length; j++) {
      if (array[i] > array[j]) {
        const temp = array[i];
        array[i] = array[j];
        array[j] = temp;
      }
    }
  }

  return array;
}
```

## 운동

1. 정수 배열을 받아 배열 요소의 합을 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

2. 정수 배열을 받아 배열에서 가장 큰 정수를 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

3. 정수 배열과 대상 정수를 받아 배열에서 대상 정수의 인덱스를 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

4. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

5. 정수 배열을 받아 오름차순으로 정렬된 배열을 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

6. 정수 배열과 목표 정수를 받아 배열에 있는 목표 정수의 인덱스를 반환하거나 목표 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

7. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

8. 정수 배열을 받아 오름차순으로 정렬된 배열을 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

9. 정수 배열과 대상 정수를 가져와서 대상 정수의 인덱스를 배열에 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성합니다. 함수의 시간복잡도는?

10. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

11. 정수 배열과 대상 정수를 받아서 배열에서 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

12. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

13. 정수 배열을 받아 오름차순으로 정렬된 배열을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

14. 정수 배열과 대상 정수를 받아서 배열에서 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

15. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 참을 반환하고 그렇지 않으면 거짓을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

16. 정수 배열과 대상 정수를 받아서 배열에서 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

17. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

18. 정수 배열과 대상 정수를 받아서 배열에 있는 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

19. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 true를 반환하고 그렇지 않으면 false를 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

20. 정수 배열과 대상 정수를 받아서 배열에서 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

21. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 참을 반환하고 그렇지 않으면 거짓을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

22. 정수 배열과 대상 정수를 받아서 배열에 있는 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

23. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 참을 반환하고 그렇지 않으면 거짓을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

24. 정수 배열과 대상 정수를 받아서 배열에 있는 대상 정수의 인덱스를 반환하거나 대상 정수가 배열에 없으면 -1을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

25. 정수 배열과 대상 정수를 받아 대상 정수가 배열에 있으면 참을 반환하고 그렇지 않으면 거짓을 반환하는 함수를 작성하십시오. 함수의 시간복잡도는?

## 답변

1. 함수의 시간 복잡도는 O(n)입니다. 합계를 계산하려면 전체 배열을 순회해야 하기 때문입니다.

2. 함수의 시간 복잡도는 O(n)입니다. 가장 큰 정수를 찾기 위해 전체 배열을 순회해야 하기 때문입니다.

3. 함수의 시간복잡도는 O(log n)이다. 왜냐하면 각 단계에서 검색 공간을 반으로 나누는 이진 검색을 사용하여 어레이를 검색할 수 있기 때문이다.

4. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

5. 함수의 시간 복잡도는 O(n log n)입니다. 배열을 n log n 분할로 나누고 각 분할을 정렬해야 하기 때문입니다.

6. 함수의 시간복잡도는 O(log n)이다. 배열은 각 단계에서 검색 공간을 반으로 나누는 이진 검색을 사용하여 검색할 수 있기 때문이다.

7. 함수의 시간복잡도는 O(log n)이다. 배열은 각 단계에서 검색 공간을 반으로 나누는 이진 검색을 사용하여 검색할 수 있기 때문이다.

8. 함수의 시간 복잡도는 O(n log n)입니다. 배열을 n log n 분할로 나누고 각 분할을 정렬해야 하기 때문입니다.

9. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

10. 함수의 시간복잡도는 O(log n)이다. 배열은 각 단계에서 검색 공간을 반으로 나누는 이진 검색을 사용하여 검색할 수 있기 때문이다.

11. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

12. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

13. 함수의 시간 복잡도는 O(n log n)입니다. 배열을 n log n 분할로 나누고 각 분할을 정렬해야 하기 때문입니다.

14. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

15. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

16. 함수의 시간복잡도는 O(log n)인데, 이는 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

17. 함수의 시간복잡도는 O(log n)인데, 이는 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

18. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

19. 함수의 시간복잡도는 O(log n)인데, 이는 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

20. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

21. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

22. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

23. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

24. 함수의 시간복잡도는 O(log n)인데, 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.

25. 함수의 시간복잡도는 O(log n)인데, 이는 각 단계에서 검색 공간을 절반으로 줄이는 이진 검색을 사용하여 배열을 검색할 수 있기 때문입니다.