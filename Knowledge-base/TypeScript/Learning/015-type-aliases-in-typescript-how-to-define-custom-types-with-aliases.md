---
title: 015: TypeScript에서 유형 별칭: 별칭으로 사용자 정의 유형을 정의하는 방법
description: 
published: true
date: 2023-03-09T11:32:51.923Z
tags: 
editor: markdown
dateCreated: 2023-03-09T11:32:51.923Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [015: Type Aliases in TypeScript: How to Define Custom Types with Aliases***English** document is available*](/en/Knowledge-base/TypeScript/Learning/015-type-aliases-in-typescript-how-to-define-custom-types-with-aliases)
{.links-list}

TypeScript의 유형 별칭: 별칭으로 사용자 정의 유형을 정의하는 방법

TypeScript는 정적 타이핑을 언어에 추가하는 JavaScript의 상위 집합입니다. TypeScript를 사용하면 유형 별칭을 사용하여 사용자 지정 유형을 정의할 수 있습니다. 유형 별칭을 사용하면 모든 유형에 대한 사용자 지정 이름을 만들 수 있으므로 코드를 더 읽기 쉽고 유지 관리할 수 있습니다.

이 기사에서는 TypeScript의 유형 별칭을 살펴보고 별칭으로 사용자 정의 유형을 정의하는 방법을 배웁니다.

## 유형 별칭이란 무엇입니까?

유형 별칭은 유형에 기억하기 쉽고 더 설명적인 이름을 지정하는 방법입니다. 기본 유형, 객체 유형, 공용체 유형 및 교차 유형을 포함하여 모든 유형의 새 이름을 만들 수 있습니다.

유형 별칭은 다른 유형을 참조하는 이름이라는 점에서 변수와 유사합니다. 새 유형을 만들지는 않지만 보다 설명적인 이름으로 기존 유형을 참조하는 방법을 제공합니다.

다음은 사용자 지정 유형을 정의하는 유형 별칭의 예입니다.

```typescript
type Person = {
  name: string;
  age: number;
  address: string;
}
```

이 예제에서는 `name`, `age` 및 `address`의 세 가지 속성으로 개체를 설명하는 `Person`이라는 유형 별칭을 정의했습니다. 이제 이 유형 별칭을 사용하여 다음과 같이 이 유형의 변수를 정의할 수 있습니다.

```typescript
const john: Person = {
  name: "John",
  age: 30,
  address: "123 Main St."
}
```

## 유형 별칭 정의

TypeScript에서 유형 별칭을 정의하려면 `type` 키워드 뒤에 별칭 이름과 그것이 참조하는 유형을 사용하십시오. 다음은 사용자 지정 유형을 정의하는 유형 별칭의 예입니다.

```typescript
type MyString = string;
```

이 예제에서는 `string` 유형의 별칭인 `MyString`이라는 유형 별칭을 정의했습니다. 이제 이 유형 별칭을 사용하여 다음과 같이 이 유형의 변수를 정의할 수 있습니다.

```typescript
const myString: MyString = "Hello, world!";
```

유형 별칭은 개체 유형, 합집합 유형 및 교차 유형과 같은 보다 복잡한 유형을 참조할 수도 있습니다. 다음은 사용자 정의 개체 유형을 정의하는 유형 별칭의 예입니다.

```typescript
type Person = {
  name: string;
  age: number;
  address: string;
}
```

이 예제에서는 `name`, `age` 및 `address`의 세 가지 속성으로 개체를 설명하는 `Person`이라는 유형 별칭을 정의했습니다. 이제 이 유형 별칭을 사용하여 다음과 같이 이 유형의 변수를 정의할 수 있습니다.

```typescript
const john: Person = {
  name: "John",
  age: 30,
  address: "123 Main St."
}
```

## 유형 별칭 사용

유형 별칭은 함수 매개변수, 반환 유형 및 변수 선언을 포함하여 TypeScript에서 유형이 사용되는 모든 곳에서 사용할 수 있습니다. 다음은 매개변수 및 반환 유형에 대한 유형 별칭을 사용하는 함수의 예입니다.

```typescript
type Point = {
  x: number;
  y: number;
}

function distance(a: Point, b: Point): number {
  const dx = a.x - b.x;
  const dy = a.y - b.y;
  return Math.sqrt(dx * dx + dy * dy);
}
```

이 예제에서는 `x`와 `y`라는 두 가지 속성을 가진 객체를 설명하는 `Point`라는 유형 별칭을 정의했습니다. 그런 다음 이 유형 별칭을 사용하여 `distance` 함수의 매개변수 유형과 반환 유형을 정의했습니다.

## 유형 별칭 사용의 이점

유형 별칭은 TypeScript 코드로 작업할 때 다음과 같은 몇 가지 이점을 제공합니다.

- **가독성 향상**: 유형에 더 설명적인 이름을 지정하면 코드를 더 쉽게 읽고 이해할 수 있습니다.
- **간편한 유지 관리**: 유형 별칭을 사용하면 코드에 있는 유형의 모든 인스턴스가 아니라 별칭 정의만 업데이트하면 되므로 유형이 변경될 때 코드를 더 쉽게 업데이트할 수 있습니다.
- **더 나은 오류 메시지**: TypeScript는 코드에서 오류가 발생할 때 유형 별칭을 사용할 때 더 정확하고 유용한 오류 메시지를 제공할 수 있습니다. 별칭은 관련된 유형에 대한 더 많은 컨텍스트를 제공하기 때문입니다.

## 추가 정보

유형 별칭은 코드를 더 읽기 쉽고 유지 관리할 수 있게 만드는 TypeScript의 강력한 기능입니다. 그러나 유형 별칭이 너무 많으면 코드를 이해하기 어려워질 수 있으므로 이를 신중하게 사용하고 과도하게 사용하지 않는 것이 중요합니다.

## 결론

TypeScript의 유형 별칭은 설명이 포함된 이름으로 사용자 지정 유형을 정의하는 방법을 제공하므로 코드를 더 읽기 쉽고 유지 관리할 수 있습니다. 기본 유형, 객체 유형, 합집합 유형 및 교차 유형을 포함하여 모든 유형의 별칭을 정의하는 데 사용할 수 있습니다. 유형 별칭을 사용하면 코드의 가독성을 높이고 유지 관리를 더 쉽게 할 수 있으며 문제가 발생할 때 더 나은 오류 메시지를 얻을 수 있습니다.

## 더 읽을거리

- [유형 별칭에 대한 TypeScript 설명서](https://www.typescriptlang.org/docs/handbook/advanced-types.html# type-aliases)
- [인터페이스 대 유형 별칭에 대한 TypeScript 문서](https://www.typescriptlang.org/docs/handbook/2/objects.html# interfaces-vs-type-aliases)
- [유형 별칭에 대한 TypeScript 심층 분석](https://basarat.gitbook.io/typescript/type-system/typealiases)