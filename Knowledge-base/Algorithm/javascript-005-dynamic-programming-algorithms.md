---
title: [JavaScript] 005: 동적 프로그래밍 알고리즘
description: 
published: true
date: 2023-02-09T07:32:23.891Z
tags: 
editor: markdown
dateCreated: 2023-02-09T07:32:22.342Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 005: Dynamic Programming Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-005-dynamic-programming-algorithms)
{.links-list}


# JavaScript 005: 동적 프로그래밍 알고리즘

동적 프로그래밍 알고리즘은 하위 문제로 나눌 수 있는 문제를 해결하기 위한 강력한 도구입니다. 하위 문제를 해결하고 결과를 저장하면 전체 문제를 훨씬 빠르게 해결할 수 있습니다.

동적 프로그래밍 알고리즘에는 하향식과 상향식의 두 가지 주요 유형이 있습니다.

## 위에서 아래로

하향식 알고리즘은 문제의 맨 위에서 시작하여 더 작은 하위 문제로 나눕니다. 그런 다음 하위 문제를 해결하고 결과를 저장합니다. 하위 문제가 이미 해결된 경우 하위 문제를 다시 해결하는 대신 저장된 결과를 사용합니다.

하향식 알고리즘은 종종 이해하기 쉽지만 상향식 알고리즘보다 느리고 더 많은 메모리를 사용할 수 있습니다.

## 상향식

상향식 알고리즘은 문제의 바닥에서 시작하여 위로 올라갑니다. 먼저 하위 문제를 해결한 다음 결과를 사용하여 전체 문제를 해결합니다.

상향식 알고리즘은 하향식 알고리즘보다 더 빠르고 더 적은 메모리를 사용할 수 있지만 이해하기 더 어려울 수 있습니다.

## 코드 예

다음은 JavaScript로 작성된 하향식 동적 프로그래밍 알고리즘의 간단한 예입니다.

```javascript
function fibonacci(n) {
  // Base case: Fib(0) = 0, Fib(1) = 1
  if (n <= 1) {
    return n;
  }
 
  // Recursive case: Fib(n) = Fib(n-1) + Fib(n-2)
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## 운동

피보나치 수열에 대한 상향식 동적 프로그래밍 알고리즘을 구현해 보십시오.

## 응답 코드

```javascript
function fibonacci(n) {
  // Base case: Fib(0) = 0, Fib(1) = 1
  if (n <= 1) {
    return n;
  }
 
  // Recursive case: Fib(n) = Fib(n-1) + Fib(n-2)
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## 해설

하향식 및 상향식 동적 프로그래밍 알고리즘은 모두 문제를 보다 효율적으로 해결하는 데 도움이 되는 강력한 도구입니다. 대부분의 경우 상향식 접근 방식이 더 효율적이지만 하향식 접근 방식이 이해하기 더 쉬울 수 있습니다.