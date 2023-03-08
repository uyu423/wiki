---
title: 005: JavaScript에서 고차 함수로 재사용 가능한 코드 작성
description: 
published: true
date: 2023-02-17T09:07:18.453Z
tags: 
editor: markdown
dateCreated: 2023-02-17T09:07:17.018Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [005: Building reusable code with higher-order functions in JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/005-building-reusable-code-with-higher-order-functions-in-javascript)
{.links-list}


# JavaScript에서 고차 함수로 재사용 가능한 코드 작성

JavaScript는 개발자가 복잡한 애플리케이션을 구축할 수 있게 해주는 강력한 프로그래밍 언어입니다. JavaScript의 주요 기능은 고차 함수에 대한 지원입니다.

고차 함수는 다른 함수를 인수로 받거나 함수를 결과로 반환하는 함수입니다. 이를 통해 개발자는 보다 모듈화되고 재사용하기 쉬운 코드를 작성할 수 있습니다.

이 기사에서는 고차 함수를 사용하여 JavaScript에서 재사용 가능한 코드를 작성하는 방법을 살펴봅니다.

## 고차함수란?

고차 함수는 하나 이상의 함수를 인수로 받거나 함수를 결과로 반환하는 함수입니다.

JavaScript에서 모든 함수는 일급 시민입니다. 즉, 다른 함수에 인수로 전달되고 함수의 결과로 반환될 수 있습니다.

다음 예를 고려하십시오.

```javascript
function add(x, y) {
  return x + y;
}

function subtract(x, y) {
  return x - y;
}

function multiply(x, y) {
  return x * y;
}

function divide(x, y) {
  return x / y;
}

function operate(operator, x, y) {
  return operator(x, y);
}

const result1 = operate(add, 1, 2);
// returns 3

const result2 = operate(subtract, 1, 2);
// returns -1

const result3 = operate(multiply, 1, 2);
// returns 2

const result4 = operate(divide, 1, 2);
// returns 0.5
```

위의 예에서 `operator` 함수와 두 개의 `x` 및 `y` 인수를 사용하는 `operate`라는 함수를 정의했습니다. 그런 다음 `operate` 함수는 `x` 및 `y` 인수를 사용하여 `operator` 함수를 호출하고 결과를 반환합니다.

우리는 또한 `add`, `subtract`, `multiply` 및 `divide`의 네 가지 다른 함수를 정의했습니다. 이러한 함수는 간단한 산술 연산을 수행합니다.

마지막으로 `operate` 함수를 네 번 호출하여 각 산술 함수를 `operator` 인수로 전달했습니다.

`operate` 함수는 고차 함수의 예입니다. 함수(`연산자` 인수)를 사용하고 해당 함수를 기반으로 결과를 반환합니다.

## 고차 함수 작성

이제 우리만의 고차 함수를 작성해 봅시다.

다음 예를 고려하십시오.

```javascript
function greeting(name) {
  return `Hello, ${name}!`;
}

function farewell(name) {
  return `Goodbye, ${name}!`;
}

function greetingFarewell(greeting, farewell, name) {
  return `${greeting(name)} ${farewell(name)}`;
}

const result = greetingFarewell(greeting, farewell, 'John');
// returns 'Hello, John! Goodbye, John!'
```

위의 예에서 `name` 인수를 사용하고 인사말 문자열을 반환하는 `greeting` 함수를 정의했습니다. 또한 `name` 인수를 받아 작별 문자열을 반환하는 `farewell` 함수도 정의했습니다.

마지막으로 `greeting` 함수, `farewell` 함수 및 `name` 인수를 사용하는 `greetingFarewell` 함수를 정의했습니다. `greetingFarewell` 함수는 `name` 인수를 사용하여 `greeting` 및 `farewell` 함수를 호출하고 연결된 결과를 반환합니다.

그런 다음 `greetingFarewell` 함수를 호출하여 `greeting` 및 `farewell` 함수를 인수로 전달했습니다.

`greetingFarewell` 함수는 고차 함수의 예입니다. 두 개의 함수(`greeting` 및 `farewell` 인수)를 사용하고 해당 함수를 기반으로 결과를 반환합니다.

## 고차 함수의 이점

고차 함수는 기존 함수에 비해 많은 이점을 제공합니다.

### 모듈성

고차 함수를 사용하면 개발자가 보다 모듈화된 코드를 작성할 수 있습니다.

모듈식 코드는 이해, 유지 및 재사용이 더 쉽습니다.

다음 예를 고려하십시오.

```javascript
function validate(value, validators) {
  for (const validator of validators) {
    const error = validator(value);
    if (error) {
      return error;
    }
  }
}

function required(value) {
  if (value === undefined || value === null || value === '') {
    return 'Required';
  }
}

function minLength(length) {
  return function(value) {
    if (value.length < length) {
      return `Must be at least ${length} characters`;
    }
  }
}

function maxLength(length) {
  return function(value) {
    if (value.length > length) {
      return `Must be at most ${length} characters`;
    }
  }
}

function email(value) {
  // email regex
}

const result = validate('john@example.com', [
  required,
  minLength(5),
  maxLength(10),
  email,
]);
// returns undefined
```

위의 예에서 `value`와 `validators`의 배열을 취하는 `validate` 함수를 정의했습니다. 그러면 'validate' 함수는 'validators'를 통해 루프를 돌고 각각을 'value'로 호출합니다. `validators` 중 하나라도 오류를 반환하면 `validate` 함수가 해당 오류를 반환합니다. 그렇지 않으면 `정의되지 않음`을 반환합니다.

또한 `required`, `minLength`, `maxLength` 및 `email`의 네 가지 다른 함수를 정의했습니다. 이러한 함수는 값의 유효성을 검사하는 데 사용됩니다. `required` 함수는 값이 `undefined`, `null` 또는 빈 문자열인지 확인합니다. `minLength` 및 `maxLength` 함수는 각각 값이 특정 길이보다 크거나 작은지 확인합니다. `email` 함수는 값이 유효한 이메일 주소인지 확인합니다.

마지막으로 `validate` 함수를 호출하여 문자열과 유효성 검사기 배열을 전달했습니다. 'validate' 함수는 유효성 검사기를 반복하고 발생하는 첫 번째 오류를 반환합니다.

'validate' 함수는 고차 함수의 예입니다. 함수 배열(`validators` 인수)을 사용하고 해당 함수를 기반으로 결과를 반환합니다.

### 결합성

고차 함수를 사용하면 개발자가 보다 구성 가능한 코드를 작성할 수 있습니다.

구성 가능한 코드는 더 복잡한 기능을 만들기 위해 결합할 수 있는 코드입니다.

다음 예를 고려하십시오.

```javascript
function map(array, transform) {
  const mapped = [];
  for (const element of array) {
    mapped.push(transform(element));
  }
  return mapped;
}

function filter(array, predicate) {
  const filtered = [];
  for (const element of array) {
    if (predicate(element)) {
      filtered.push(element);
    }
  }
  return filtered;
}

function reduce(array, reducer, accumulator) {
  for (const element of array) {
    accumulator = reducer(accumulator, element);
  }
  return accumulator;
}

const result = reduce(
  map(filter([1, 2, 3, 4, 5], x => x % 2 === 0), x => x * x),
  (acc, cur) => acc + cur,
  0,
);
// returns 20
```

위의 예에서는 `map`, `filter` 및 `reduce`의 세 가지 고차 함수를 정의했습니다.

`map` 함수는 배열과 `transform` 함수를 사용합니다. 그런 다음 `map` 함수는 배열의 각 요소에 대해 `transform` 함수를 호출하고 변환된 요소가 포함된 새 배열을 반환합니다.

`filter` 함수는 배열과 `predicate` 함수를 사용합니다. 그런 다음 `filter` 함수는 배열의 각 요소에 대해 `predicate` 함수를 호출하고 `predicate` 함수가 `true`를 반환한 요소만 있는 새 배열을 반환합니다.

`reduce` 함수는 배열, `reducer` 함수 및 `accumulator`를 사용합니다. 그런 다음 `reduce` 함수는 `accumulator`와 배열의 각 요소에서 `reducer` 함수를 호출합니다. 'reducer' 함수는 연산 결과로 'accumulator'를 업데이트하는 역할을 합니다. `reduce` 함수는 배열의 루프를 완료하면 `accumulator`를 반환합니다.

그런 다음 `reduce` 함수를 호출하여 `map` 함수, `filter` 함수 및 배열을 전달했습니다. `reduce` 함수는 먼저 `map` 함수를 호출하고 `filter` 함수를 호출합니다. '필터' 함수는 짝수만 있는 배열을 반환합니다. 그러면 `map` 함수는 짝수의 제곱 배열을 반환합니다. 그러면 `reduce` 함수가 배열의 요소를 합산하고 결과를 반환합니다.

'reduce' 함수는 고차 함수의 예입니다. 두 가지 함수(`map` 및 `filter` 함수)를 사용하고 해당 함수를 기반으로 결과를 반환합니다.

## 결론

이 기사에서는 고차 함수를 사용하여 JavaScript에서 재사용 가능한 코드를 작성하는 방법을 살펴보았습니다.

고차 함수는 모듈성 및 구성 가능성을 포함하여 기존 함수에 비해 많은 이점을 제공합니다.

고차 함수를 작성할 때 가독성과 재사용 간의 균형을 고려하는 것이 중요합니다. 고차 함수는 코드를 이해하기 어렵게 만들 수 있지만 코드를 재사용하기 쉽게 만들 수도 있습니다.

## 자원

- [일급 시민으로서 기능](https://en.wikipedia.org/wiki/First-class_function)
- [고차 함수](https://en.wikipedia.org/wiki/Higher-order_function)
- [JavaScript: 좋은 부분](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)