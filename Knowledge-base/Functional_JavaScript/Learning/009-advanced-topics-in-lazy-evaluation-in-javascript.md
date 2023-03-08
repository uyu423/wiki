---
title: 009: JavaScript의 지연 평가에 대한 고급 주제
description: 
published: true
date: 2023-02-17T11:07:00.448Z
tags: 
editor: markdown
dateCreated: 2023-02-17T11:06:53.743Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [009: Advanced topics in lazy evaluation in JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/009-advanced-topics-in-lazy-evaluation-in-javascript)
{.links-list}


## 지연 평가란?
게으른 평가는 표현식의 결과가 필요할 때까지 계산되지 않는 계산의 한 형태입니다. 이는 표현식이 변수에 바인딩되자마자 평가되는 즉시 평가와 대조될 수 있습니다.

JavaScript에서 지연 평가는 여러 위치에서 사용됩니다.

- `&&` 및 `||` 연산자는 왼쪽이 결과를 결정하지 않는 경우에만 오른쪽을 평가합니다.
- `? :` 연산자는 왼쪽이 참인 경우에만 오른쪽을 평가합니다.
- `.` 연산자는 왼쪽이 객체인 경우에만 오른쪽을 평가합니다.
- 함수 인수는 함수가 호출될 때만 평가됩니다.
- 개체 속성은 액세스할 때만 평가됩니다.

지연 평가는 불필요한 작업을 피함으로써 성능을 향상시키는 데 사용할 수 있습니다. 무한 데이터 구조를 만드는 데에도 사용할 수 있습니다.

## 지연 평가 및 무한 데이터 구조
지연 평가는 종종 무한 데이터 구조를 만들기 위해 재귀와 함께 사용됩니다.

다음 예를 고려하십시오.

```javascript
function createRange(start, end) {
  if (start === end) {
    return [start];
  } else {
    return [start, ...createRange(start + 1, end)];
  }
}
```

이 함수는 `start`에서 시작하여 `end`에서 끝나는 숫자 배열을 만듭니다. `...` 스프레드 연산자는 배열을 연결하는 데 사용됩니다.

`createRange(1, Infinity)`를 호출하면 함수는 호출 스택이 오버플로될 때까지 배열을 계속 생성합니다. 그러나 `createRange(1, 10)`을 호출하면 이 함수는 10개의 배열만 생성합니다.

이는 함수가 유한한 `end` 인수로 호출될 때만 `...` 연산자가 평가되기 때문입니다. `end`가 `Infinity`이면 `...` 연산자는 평가되지 않습니다.

## 게으른 평가 및 성능
게으른 평가는 불필요한 작업을 피함으로써 성능을 향상시킬 수 있습니다.

다음 예를 고려하십시오.

```javascript
function isEven(n) {
  if (n === 0) {
    return true;
  } else if (n === 1) {
    return false;
  } else {
    return isEven(n - 2);
  }
}

isEven(1000000); // false
```

이 함수는 `n`이 짝수이면 `true`를 반환하고 `n`이 홀수이면 `false`를 반환합니다. 재귀를 사용하여 결과를 계산합니다.

`isEven(1000000)`을 호출하면 호출 스택이 오버플로될 때까지 함수가 재귀합니다. 그러나 `isEven(10)`을 호출하면 함수는 10번만 재귀합니다.

이는 함수가 유한한 `n` 인수로 호출될 때만 `if` 문이 평가되기 때문입니다. `n`이 `1000000`이면 `if` 문은 평가되지 않습니다.

## 게으른 평가와 메모이제이션
지연 평가는 비용이 많이 드는 함수 호출의 결과를 메모하여 성능을 향상시키는 데 사용할 수 있습니다.

다음 예를 고려하십시오.

```javascript
function Fibonacci(n) {
  if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1;
  } else {
    return Fibonacci(n - 1) + Fibonacci(n - 2);
  }
}

Fibonacci(10); // 55
```

이 함수는 `n`번째 피보나치 수를 계산합니다. 재귀를 사용하여 결과를 계산합니다.

`Fibonacci(10)`을 호출하면 함수는 10번 재귀합니다. 그러나 `Fibonacci(100)`을 호출하면 함수가 100번 재귀합니다.

이는 함수가 유한한 `n` 인수로 호출될 때만 `if` 문이 평가되기 때문입니다. `n`이 `100`이면 `if` 문이 평가되지 않습니다.

값비싼 함수 호출의 결과를 메모하여 이 함수의 성능을 향상시킬 수 있습니다.

```javascript
function Fibonacci(n, memo = {}) {
  if (n in memo) {
    return memo[n];
  } else if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1;
  } else {
    memo[n] = Fibonacci(n - 1, memo) + Fibonacci(n - 2, memo);
    return memo[n];
  }
}

Fibonacci(10); // 55
Fibonacci(100); // 354224848179261915075
```

이 버전의 함수에서는 빈 개체를 메모로 전달합니다. 이 함수는 `n`번째 피보나치 수가 메모에 있는지 확인합니다. 그렇다면 함수는 메모된 값을 반환합니다. 그렇지 않은 경우 함수는 `n`번째 피보나치 수를 계산하고 결과를 메모합니다.

이 개선은 중요합니다. 원래 함수는 `100`번째 피보나치 수를 계산하는 데 `10`밀리초가 걸립니다. 메모이제이션 함수는 `0`밀리초가 걸립니다.

## 추가 정보
- 게으른 평가는 필요에 의한 호출이라고도 합니다.
- Eager 평가는 call-by-value라고도 합니다.
- JavaScript에서 지연 평가가 항상 보장되는 것은 아닙니다. 예를 들어, `.` 연산자는 왼쪽이 객체가 아닌 경우 오른쪽을 간절히 평가합니다.

## 자원
- [Wikipedia - 지연 평가](https://en.wikipedia.org/wiki/Lazy_evaluation)
- [MDN - 지연 평가](https://developer.mozilla.org/en-US/docs/Glossary/Lazy_evaluation)
- [ExploringJS - 지연 평가](https://exploringjs.com/es6/ch_operators.html# sec_lazy-evaluation)