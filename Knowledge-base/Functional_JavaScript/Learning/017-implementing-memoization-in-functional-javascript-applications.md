---
title: 017: 기능적 JavaScript 애플리케이션에서 메모이제이션 구현
description: 
published: true
date: 2023-02-17T15:06:53.521Z
tags: 
editor: markdown
dateCreated: 2023-02-17T15:06:52.052Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [017: Implementing memoization in functional JavaScript applications***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/017-implementing-memoization-in-functional-javascript-applications)
{.links-list}


# 기능적 JavaScript 애플리케이션에서 메모이제이션 구현

함수형 프로그래밍은 함수의 평가를 강조하는 프로그래밍 패러다임입니다. 보다 간결하고 유지 관리 가능한 코드를 작성하는 데 자주 사용되는 선언적 프로그래밍 스타일입니다.

함수형 프로그래밍의 핵심 개념 중 하나는 메모이제이션입니다. 메모이제이션은 함수 호출 결과를 캐싱하고, 같은 인자로 같은 함수를 다시 호출했을 때 캐싱된 결과를 재사용하는 기법이다.

이는 특히 함수 호출이 종종 동일한 인수로 수행되는 JavaScript 애플리케이션에서 강력한 최적화 기술이 될 수 있습니다. 이번 포스팅에서는 자바스크립트에서 메모이제이션을 구현하는 방법에 대해 알아보겠습니다.

## 메모이제이션이란?

메모이제이션은 함수 호출 결과를 캐싱하고, 같은 인자로 같은 함수를 다시 호출했을 때 캐싱된 결과를 재사용하는 기법이다.

이는 특히 함수 호출이 종종 동일한 인수로 수행되는 JavaScript 애플리케이션에서 강력한 최적화 기술이 될 수 있습니다.

예를 들어 숫자의 계승을 계산하는 함수를 생각해 보십시오. 이 함수는 재귀를 사용하여 구현할 수 있습니다.

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

동일한 인수로 이 함수를 여러 번 호출하면 매번 계승을 다시 계산합니다. 이는 특히 많은 수의 경우 비효율적일 수 있습니다.

매번 factorial을 다시 계산할 필요가 없도록 메모이제이션을 사용하여 함수의 결과를 캐시할 수 있습니다.

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

let memo = {};

function memoizedFactorial(n) {
    if (memo[n]) {
        return memo[n];
    }
    let result = factorial(n);
    memo[n] = result;
    return result;
}
```

이 예제에서는 캐시된 결과를 저장할 메모 개체를 만듭니다. memoizedFactorial 함수를 호출할 때 먼저 결과가 이미 캐시되었는지 확인합니다. 그렇다면 캐시된 결과를 반환합니다. 그렇지 않은 경우 결과를 계산하고 반환하기 전에 캐시합니다.

이는 특히 함수 호출이 종종 동일한 인수로 수행되는 JavaScript 애플리케이션에서 강력한 최적화 기술이 될 수 있습니다.

## 메모이제이션 구현

JavaScript에서 메모이제이션을 구현하는 몇 가지 방법이 있습니다. 이 섹션에서는 두 가지 접근 방식을 살펴보겠습니다.

### 접근법 1: 클로저 사용

메모이제이션을 구현하는 한 가지 방법은 클로저를 사용하는 것입니다. 클로저는 외부 범위의 변수에 액세스할 수 있는 함수입니다.

예를 들어 다음 코드를 고려하십시오.

```javascript
function outer() {
    let x = 10;
    
    function inner() {
        console.log(x);
    }
    
    inner();
}

outer(); // 10
```

이 코드에서 내부 함수는 외부 함수의 x 변수에 액세스할 수 있습니다. 이는 내부 함수가 외부 함수 내에 정의되어 있기 때문입니다.

이 개념을 사용하여 메모이제이션을 구현할 수 있습니다.

```javascript
function memoize(fn) {
    let memo = {};
    
    return function(...args) {
        if (memo[args]) {
            return memo[args];
        }
        
        let result = fn(...args);
        memo[args] = result;
        return result;
    }
}

function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

let memoizedFactorial = memoize(factorial);

memoizedFactorial(5); // 120
memoizedFactorial(5); // 120 (cached)
```

이 코드에서는 함수를 인수로 사용하는 memoize 함수를 만듭니다. 이 함수는 외부 범위의 메모 변수에 액세스할 수 있는 새 함수를 반환합니다.

새 함수를 호출하면 먼저 결과가 이미 캐시되었는지 확인합니다. 그렇다면 캐시된 결과를 반환합니다. 그렇지 않은 경우 결과를 계산하고 반환하기 전에 캐시합니다.

이 메모라이즈 기능을 사용하여 모든 기능을 메모할 수 있습니다.

### 접근법 2: 고차 함수 사용

메모이제이션을 구현하는 또 다른 방법은 고차 함수를 사용하는 것입니다. 고차 함수는 하나 이상의 함수를 인수로 취하는 함수입니다.

예를 들어 다음 코드를 고려하십시오.

```javascript
function higherOrder(fn, x) {
    return fn(x);
}

function foo(x) {
    return x + 1;
}

higherOrder(foo, 10); // 11
```

이 코드에는 함수와 인수를 받는 고차 함수가 있습니다. 인수를 사용하여 함수를 호출하고 결과를 반환합니다.

이 개념을 사용하여 메모이제이션을 구현할 수 있습니다.

```javascript
function memoize(fn) {
    let memo = {};
    
    return function(...args) {
        if (memo[args]) {
            return memo[args];
        }
        
        let result = fn(...args);
        memo[args] = result;
        return result;
    }
}

function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

let memoizedFactorial = memoize(factorial);

memoizedFactorial(5); // 120
memoizedFactorial(5); // 120 (cached)
```

이 코드에서는 함수를 인수로 사용하는 memoize 함수를 만듭니다. 이 함수는 함수와 인수를 사용하여 memoize 함수를 호출하는 새 함수를 반환합니다.

새 함수를 호출하면 먼저 결과가 이미 캐시되었는지 확인합니다. 그렇다면 캐시된 결과를 반환합니다. 그렇지 않은 경우 결과를 계산하고 반환하기 전에 캐시합니다.

이 메모라이즈 기능을 사용하여 모든 기능을 메모할 수 있습니다.

## 메모이제이션을 사용하는 경우

메모이제이션은 강력한 최적화 기술이 될 수 있지만 항상 최선의 선택은 아닙니다. 이 섹션에서는 메모이제이션 사용의 장단점을 살펴보겠습니다.

### 장점

- 메모이제이션은 비용이 많이 드는 함수 호출의 결과를 캐시하는 데 사용할 수 있습니다. 이렇게 하면 불필요한 재계산을 방지하여 애플리케이션의 성능을 향상시킬 수 있습니다.

- 메모이제이션은 중복 함수 호출을 피함으로써 코드를 더 간결하게 만들 수 있습니다.

- 메모이제이션은 코드의 의도를 더 명확하게 하여 코드를 더 읽기 쉽게 만들 수 있습니다.

### 단점

- 메모이제이션은 메모하지 않은 코드보다 더 많은 메모리를 사용할 수 있습니다. 메모이제이션 코드는 함수 호출 결과를 메모리에 저장하기 때문입니다.

- 메모화는 코드를 디버그하기 어렵게 만들 수 있습니다. 캐시된 결과로 인해 코드 실행을 추적하기 어려울 수 있기 때문입니다.

- 메모화는 코드를 이해하기 어렵게 만들 수 있습니다. 메모이제이션을 사용하면 코드가 더 복잡해질 수 있기 때문입니다.

## 결론

이번 포스팅에서는 메모이제이션과 이를 자바스크립트로 구현하는 방법에 대해 알아보았습니다. 메모이제이션은 강력한 최적화 기술이 될 수 있지만 항상 최선의 선택은 아닙니다. 애플리케이션에서 메모이제이션을 사용할지 여부를 결정하기 전에 메모이제이션 사용의 장단점을 따져봐야 합니다.