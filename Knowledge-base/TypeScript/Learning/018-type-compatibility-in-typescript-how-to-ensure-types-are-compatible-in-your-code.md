---
title: 018: TypeScript의 유형 호환성: 코드에서 유형이 호환되는지 확인하는 방법
description: 
published: true
date: 2023-03-02T16:32:19.003Z
tags: 
editor: markdown
dateCreated: 2023-03-02T16:32:17.563Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [018: Type Compatibility in TypeScript: How to Ensure Types Are Compatible in Your Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/018-type-compatibility-in-typescript-how-to-ensure-types-are-compatible-in-your-code)
{.links-list}
TypeScript의 유형 호환성: 코드에서 유형이 호환되는지 확인하는 방법

TypeScript는 대규모 애플리케이션 개발에 널리 사용되는 인기 있는 오픈 소스 프로그래밍 언어입니다. TypeScript는 개발자가 더 안전하고 유지 관리하기 쉬운 코드를 작성하는 데 도움이 되는 유형 주석을 지원합니다. 그러나 TypeScript에서 유형이 호환되는지 확인하는 것은 어려울 수 있습니다. 이 게시물은 TypeScript의 유형 호환성과 코드에서 유형이 호환되는지 확인하는 방법을 안내합니다.

## TypeScript의 유형 호환성이란 무엇입니까?

TypeScript의 유형 호환성은 한 유형이 다른 유형에 할당되는 기능을 나타냅니다. 예를 들어 다음 코드를 고려하십시오.

```typescript
let x: boolean = true;
let y: boolean | number = x;
```

이 코드에서는 `boolean` 유형의 `x` 변수와 `boolean | 번호`. `|` 기호는 공용체 유형을 나타내며, 이는 `y`가 `부울` 또는 `숫자`일 수 있음을 의미합니다. 그런 다음 `x` 값을 `y`에 할당합니다. `boolean`은 `boolean | number`, 할당이 유효합니다.

TypeScript는 구조적 타이핑을 사용합니다. 즉, 내부 구조가 호환되는 경우 두 가지 유형이 호환됩니다. 이는 이름이나 선언을 기반으로 유형을 비교하는 명목 유형 지정과 다릅니다.

## TypeScript에서 유형 호환성 보장

TypeScript에서 유형 호환성을 보장하려면 유형 호환성 규칙을 이해해야 합니다. TypeScript에는 다음과 같은 유형 호환성에 대한 몇 가지 규칙이 있습니다.

### 기능 할당 가능성

TypeScript의 함수는 매개변수 목록과 반환 유형이 호환되는 경우 호환됩니다. 예를 들어 다음 코드를 고려하십시오.

```typescript
type Adder = (a: number, b: number) => number;
let add: Adder = (a, b) => a + b;

type Multiplier = (a: number, b: number) => number;
let multiply: Multiplier = (a, b) => a * b;

let operation: Adder = multiply;
```

이 코드에서는 '숫자' 유형의 두 매개변수를 사용하고 '숫자' 유형의 값을 반환하는 함수인 두 가지 유형 '가산기' 및 '승수'를 선언합니다. 그런 다음 각각 `Adder` 및 `Multiplier` 유형의 두 변수 `add` 및 `multiply`를 선언합니다. 마지막으로 `Adder` 유형의 `operation` 변수를 선언하고 `multiply` 값을 할당합니다. `multiply`의 매개변수 유형과 반환 유형은 `Adder`와 호환되므로 할당이 유효합니다.

### 객체 할당 가능성

TypeScript의 객체는 속성이 호환되는 경우 호환됩니다. 예를 들어 다음 코드를 고려하십시오.

```typescript
interface Person {
  name: string;
  age: number;
}

let person: Person = {
  name: 'John',
  age: 30,
};

let employee = {
  name: 'John',
  age: 30,
  salary: 50000,
};

person = employee;
```

이 코드에서는 `string` 유형의 `name` 속성과 `number` 유형 `age` 속성이 있는 `Person` 인터페이스를 선언합니다. 그런 다음 `Person` 유형의 `person` 변수를 선언하고 `name` 및 `age` 속성을 가진 개체를 할당합니다. 그런 다음 `name`, `age` 및 `salary` 속성이 있는 변수 `employee`를 선언합니다. 마지막으로 `employee` 값을 `person`에 할당합니다. `employee`는 `Person`의 모든 속성을 가지므로 할당이 유효합니다.

### 제네릭 할당 가능성

TypeScript의 제네릭은 유형이 호환되는 경우 호환됩니다. 예를 들어 다음 코드를 고려하십시오.

```typescript
interface Box<T> {
  value: T;
}

let stringBox: Box<string> = { value: 'hello' };
let anyBox: Box<any> = stringBox;
```

이 코드에서는 일반 유형 `T`와 `T` 유형의 속성 `value`를 사용하여 인터페이스 `Box`를 선언합니다. 그런 다음 `Box<string>` 유형의 `stringBox` 변수를 선언하고 `string` 유형의 `value` 속성을 가진 객체를 할당합니다. 그런 다음 `Box<any>` 유형의 `anyBox` 변수를 선언하고 여기에 `stringBox` 값을 할당합니다. `string`은 `any`의 하위 유형이므로 할당이 유효합니다.

## 추가 정보

TypeScript에는 다음과 같은 유형 비호환성에 대한 규칙도 있습니다.

- 선택적 매개변수 및 나머지 매개변수로 기능 할당 가능
- 다른 arity로 기능 할당 가능
- 초과 속성을 가진 개체의 할당 가능성
- 속성이 누락된 객체 할당 가능성

이러한 규칙에 대해 자세히 알아보려면 TypeScript 설명서를 확인하세요.

## 경고

TypeScript는 유형 비호환성에 대한 경고를 제공합니다. 호환되지 않는 유형의 값을 할당하려고 하면 TypeScript에서 경고를 표시합니다. 예를 들어 다음 코드를 고려하십시오.

```typescript
let x: string = 'hello';
let y: number = x;
```

이 코드에서 `string` 유형의 `x` 변수를 선언하고 여기에 `'hello'` 값을 할당합니다. 그런 다음 '숫자' 유형의 변수 'y'를 선언하고 여기에 'x' 값을 할당합니다. `문자열`은 `숫자`와 호환되지 않으므로 TypeScript는 경고를 표시합니다.

## 위험

TypeScript는 모든 유형 오류를 포착할 수 없습니다. 오류 없이 컴파일되지만 런타임에 예기치 않은 결과를 생성하는 코드를 작성할 수 있습니다. 따라서 테스트를 작성하고 올바른 코딩 방법을 사용하여 코드가 올바른지 확인하는 것이 중요합니다.

## 결론

TypeScript의 형식 호환성은 개발자가 더 안전하고 유지 관리하기 쉬운 코드를 작성하는 데 도움이 되는 중요한 개념입니다. TypeScript에서 유형 호환성을 보장하려면 유형 호환성 규칙을 이해하고 좋은 코딩 방법을 사용해야 합니다. TypeScript는 유형 비호환성에 대한 경고를 제공하지만 코드가 올바른지 확인하기 위해 테스트를 작성하는 것이 중요합니다.

## 더 읽을 거리

- [유형 호환성에 대한 TypeScript 문서](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
- [구조적 타이핑에 대한 TypeScript 문서](https://www.typescriptlang.org/docs/handbook/type-compatibility.html# structural-typing)
- [명목 타이핑에 대한 TypeScript 문서](https://www.typescriptlang.org/docs/handbook/type-compatibility.html# nominal-typing)