---
title: 013: TypeScript의 Type Guards: 조건문으로 유형 범위를 좁히는 방법
description: 
published: true
date: 2023-03-14T05:33:10.327Z
tags: 
editor: markdown
dateCreated: 2023-03-14T05:33:10.327Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [013: Type Guards in TypeScript: How to Narrow Down Types with Conditionals***English** document is available*](/en/Knowledge-base/TypeScript/Learning/013-type-guards-in-typescript-how-to-narrow-down-types-with-conditionals)
{.links-list}



TypeScript의 Type Guards: 조건부로 유형 범위를 좁히는 방법

TypeScript는 JavaScript로 컴파일되고 다른 기능과 함께 정적 유형 검사를 추가하는 강력한 언어입니다. TypeScript의 가장 유용한 기능 중 하나는 Type Guards를 사용하여 유형을 좁히는 기능입니다. 이 게시물에서는 Type Guards를 사용하여 조건부로 유형을 좁히는 방법을 배웁니다.

## 타입 가드란?

Type Guards는 TypeScript에서 유형을 좁히는 방법입니다. 런타임에 변수가 특정 유형인지 확인하는 데 사용됩니다. 이는 공용체 유형을 처리하거나 작업을 수행하기 전에 변수가 특정 유형인지 확인하려는 경우에 유용합니다.

Type Guard는 조건문을 사용하여 구현됩니다. 이러한 조건은 사용 사례에 따라 단순하거나 복잡할 수 있습니다.

## 타입 가드 사용

Type Guard는 `typeof` 연산자, `instanceof` 연산자 또는 사용자 정의 유형 술어를 사용하여 구현할 수 있습니다.

### typeof 타입 가드

`typeof` 연산자는 보유하고 있는 값의 유형에 따라 유형의 범위를 좁히는 데 사용할 수 있습니다. 예를 들어, 숫자나 문자열을 담을 수 있는 변수 `x`가 있다고 합시다:

```typescript
let x: number | string = 5;
```

`typeof` 연산자를 사용하여 `x`가 숫자인지 문자열인지 확인할 수 있습니다.

```typescript
if (typeof x === 'number') {
  // x is a number
} else {
  // x is a string
}
```

### type Guard의 인스턴스

`instanceof` 연산자는 생성자 함수를 기반으로 유형의 범위를 좁히는 데 사용할 수 있습니다. 예를 들어 `Person` 클래스가 있다고 가정해 보겠습니다.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
```

`Person`의 인스턴스를 만든 다음 `instanceof` 연산자를 사용하여 `Person`의 인스턴스인지 확인할 수 있습니다.

```typescript
let p = new Person('John', 30);

if (p instanceof Person) {
  // p is an instance of Person
} else {
  // p is not an instance of Person
}
```

### 사용자 정의 유형 술어

사용자 지정 유형 조건자는 부울 값을 반환하는 함수이며 변수가 특정 유형인지 확인하는 데 사용됩니다. 예를 들어 `Car` 유형이 있다고 가정해 보겠습니다.

```typescript
interface Car {
  make: string;
  model: string;
  year: number;
}
```

변수가 `Car` 유형인지 확인하기 위해 사용자 정의 유형 술어를 작성할 수 있습니다.

```typescript
function isCar(obj: any): obj is Car {
  return (
    typeof obj === 'object' &&
    'make' in obj &&
    'model' in obj &&
    'year' in obj
  );
}
```

그런 다음 이 사용자 지정 유형 조건자를 사용하여 변수가 `Car` 유형인지 확인할 수 있습니다.

```typescript
let myCar = { make: 'Honda', model: 'Civic', year: 2010 };

if (isCar(myCar)) {
  // myCar is of type Car
} else {
  // myCar is not of type Car
}
```

## 추가 정보

Type Guards는 코드에서 유형 안전을 보장하는 데 도움이 되는 TypeScript의 강력한 기능입니다. 유니온 유형을 처리하거나 작업을 수행하기 전에 변수가 특정 유형인지 확인하려는 경우에 특히 유용합니다.

Type Guards는 런타임에만 작동하고 컴파일 타임에는 작동하지 않는다는 점에 유의해야 합니다. 따라서 코드가 제대로 작동하는지 철저하게 테스트하는 것이 중요합니다.

## 결론

Type Guards는 코드에서 유형 안전을 보장하는 데 도움이 되는 TypeScript의 필수 기능입니다. 사용하기 쉽고 간단하거나 복잡한 조건을 사용하여 구현할 수 있습니다. Type Guards를 사용하면 코드가 올바르게 작동하고 형식이 안전하다는 것을 확신할 수 있습니다.

## 더 읽을거리

- [TypeScript Handbook: Type Guards 및 Differentiating Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html# type-guards-and-differentiating-types)
- [TypeScript 심층 분석: Type Guards](https://basarat.gitbook.io/typescript/type-system/typeguard)
- [TypeScript의 Type Guards](https://www.tutorialsteacher.com/typescript/typescript-type-guards)