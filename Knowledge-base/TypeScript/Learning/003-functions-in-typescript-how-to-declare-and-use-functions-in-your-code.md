---
title: 003: TypeScript의 함수: 코드에서 함수를 선언하고 사용하는 방법
description: 
published: true
date: 2023-03-06T10:32:52.473Z
tags: 
editor: markdown
dateCreated: 2023-03-06T10:32:45.314Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [003: Functions in TypeScript: How to Declare and Use Functions in Your Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/003-functions-in-typescript-how-to-declare-and-use-functions-in-your-code)
{.links-list}



TypeScript의 함수: 코드에서 함수를 선언하고 사용하는 방법

TypeScript에서 함수는 언어의 필수 부분입니다. 재사용 가능한 코드 조각을 캡슐화하고 코드를 보다 모듈화하는 데 사용됩니다. 이 기사에서는 TypeScript에서 함수를 선언하고 사용하는 방법을 살펴봅니다.

## TypeScript의 함수는 무엇인가요?

함수는 특정 작업을 수행하는 코드 블록입니다. TypeScript에서 함수는 여러 방법으로 선언될 수 있으며 매개변수와 반환 값을 가질 수 있습니다.

TypeScript의 함수는 두 가지 유형으로 분류할 수 있습니다.

1. 명명된 함수: 이들은 연관된 이름이 있는 함수입니다. `function` 키워드를 사용하여 선언할 수 있습니다.

2. 익명 함수: 연관된 이름이 없는 함수입니다. 변수에 할당하거나 다른 함수에 인수로 전달할 수 있습니다.

## TypeScript에서 함수 선언하기

TypeScript에서 함수를 선언하려면 함수 이름, 매개변수(있는 경우) 및 반환 유형(있는 경우)을 지정해야 합니다. 다음은 명명된 함수의 예입니다.

```typescript
function addNumbers(num1: number, num2: number): number {
  return num1 + num2;
}
```

위의 예에서 '숫자' 유형의 매개변수 두 개를 사용하고 '숫자' 유형의 값을 반환하는 'addNumbers'라는 함수를 선언했습니다.

다음은 익명 함수의 예입니다.

```typescript
let multiplyNumbers = function(num1: number, num2: number): number {
  return num1 * num2;
}
```

위의 예에서는 'multiplyNumbers'라는 변수에 익명 함수를 할당했습니다.

## TypeScript에서 함수 사용하기

TypeScript에서 함수를 선언하면 코드에서 사용할 수 있습니다. 다음은 앞에서 선언한 `addNumbers` 함수를 사용하는 방법의 예입니다.

```typescript
let result = addNumbers(10, 20);
console.log(result); // Output: 30
```

위의 예에서 `10`과 `20`이라는 두 개의 인수를 사용하여 `addNumbers` 함수를 호출하고 결과를 `result`라는 변수에 할당했습니다. 그런 다음 `result` 값을 콘솔에 기록했는데 `30`이 출력되어야 합니다.

다음은 앞에서 선언한 `multiplyNumbers` 함수를 사용하는 방법의 예입니다.

```typescript
let result = multiplyNumbers(10, 20);
console.log(result); // Output: 200
```

위의 예에서는 `10`과 `20`의 두 인수를 사용하여 `multiplyNumbers` 함수를 호출하고 결과를 `result`라는 변수에 할당했습니다. 그런 다음 `result` 값을 콘솔에 기록했는데 `200`이 출력되어야 합니다.

## 선택적 매개변수 및 기본 매개변수

TypeScript에서는 함수에서 선택적 매개변수와 기본 매개변수를 선언할 수 있습니다. 선택적 매개변수는 함수에 전달할 필요가 없는 매개변수인 반면 기본 매개변수는 인수가 전달되지 않은 경우 기본값을 갖는 매개변수입니다.

다음은 선택적 매개변수가 있는 함수의 예입니다.

```typescript
function greet(name?: string): void {
  if (name) {
    console.log(`Hello, ${name}!`);
  } else {
    console.log("Hello!");
  }
}
```

위의 예에서 `string` 유형의 `name`이라는 선택적 매개변수를 사용하는 `greet`라는 함수를 선언했습니다. `name` 매개변수가 전달되면 함수는 이름이 포함된 인사말을 기록합니다. `name` 매개변수가 전달되지 않으면 함수는 일반적인 인사말을 기록합니다.

다음은 기본 매개변수가 있는 함수의 예입니다.

```typescript
function greet(name: string = "World"): void {
  console.log(`Hello, ${name}!`);
}
```

위의 예에서 `string` 유형의 `name`이라는 기본 매개 변수를 사용하는 `greet`라는 함수를 선언했습니다. `name` 매개변수가 전달되지 않으면 함수는 `"World"`의 기본값을 사용합니다.

## 나머지 매개변수

TypeScript에서는 함수에서 나머지 매개변수를 선언할 수 있습니다. 나머지 매개변수는 가변 개수의 인수를 함수에 전달하는 데 사용됩니다.

다음은 나머지 매개변수가 있는 함수의 예입니다.

```typescript
function multiplyNumbers(...nums: number[]): number {
  return nums.reduce((total, num) => total * num);
}
```

위의 예에서 `number[]` 유형의 `nums`라는 나머지 매개변수를 사용하는 `multiplyNumbers`라는 함수를 선언했습니다. 이 함수는 `reduce` 메서드를 사용하여 인수로 전달된 모든 숫자를 곱합니다.

## 결론

이 기사에서는 TypeScript에서 함수를 선언하고 사용하는 방법을 살펴보았습니다. 명명된 함수, 익명 함수, 선택적 매개변수, 기본 매개변수 및 나머지 매개변수를 다루었습니다.

함수는 모든 프로그래밍 언어의 필수 부분이며 TypeScript도 예외는 아닙니다. 함수를 사용하면 코드를 보다 모듈화하고 재사용 가능하게 만들 수 있습니다. 이 기사를 통해 TypeScript에서 함수를 선언하고 사용하는 방법을 잘 이해할 수 있기를 바랍니다.

## 더 읽을 거리

- [TypeScript 핸드북: 함수](https://www.typescriptlang.org/docs/handbook/functions.html)
- [MDN 웹 문서: 함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)