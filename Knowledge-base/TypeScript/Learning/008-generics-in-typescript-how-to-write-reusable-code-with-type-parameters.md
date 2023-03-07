---
title: 008: TypeScript의 제네릭: 유형 매개변수로 재사용 가능한 코드를 작성하는 방법
description: 
published: true
date: 2023-03-07T20:32:38.020Z
tags: 
editor: markdown
dateCreated: 2023-03-07T20:32:38.020Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [008: Generics in TypeScript: How to Write Reusable Code with Type Parameters***English** document is available*](/en/Knowledge-base/TypeScript/Learning/008-generics-in-typescript-how-to-write-reusable-code-with-type-parameters)
{.links-list}



TypeScript의 제네릭: 유형 매개변수로 재사용 가능한 코드를 작성하는 방법

다른 유형에 대해 동일한 코드를 반복해서 작성하는 자신을 발견한 적이 있습니까? 아니면 다른 유형의 데이터와 함께 작동할 수 있는 함수를 작성해야 하는 상황에 직면했습니까? 이것은 TypeScript의 제네릭이 유용한 곳입니다.

이 게시물에서는 제네릭이 무엇이며 TypeScript에서 제네릭을 사용하여 유형 매개변수로 재사용 가능한 코드를 작성하는 방법을 살펴보겠습니다.

## 제네릭이란 무엇입니까?

제네릭은 여러 유형에서 작동할 수 있는 코드를 작성하는 방법입니다. 작업할 데이터 유형에 대한 자리 표시자가 있는 유형 또는 함수를 정의할 수 있습니다. 이를 통해 재사용 가능성이 높고 유연한 코드를 작성할 수 있습니다.

TypeScript의 제네릭은 Java 및 C# 과 같은 다른 프로그래밍 언어의 제네릭과 유사합니다. 이를 통해 특정 유형에 의존하지 않고 대신 특정 요구 사항을 충족하는 모든 유형에서 작동하는 코드를 작성할 수 있습니다.

## 제네릭을 사용하는 이유

제네릭은 다양한 유형의 데이터로 작업할 수 있는 코드를 작성해야 하는 상황에서 유용합니다. 유사한 유형에 대한 중복 코드 작성을 피하고 코드를 보다 유연하고 재사용 가능하게 만드는 데 도움이 됩니다.

예를 들어 문자열 배열을 받아 첫 번째 요소를 반환하는 함수가 있다고 가정해 보겠습니다.

```typescript
function getFirstElement(arr: string[]): string {
  return arr[0];
}
```

숫자 배열의 첫 번째 요소를 가져와야 하는 경우 별도의 함수를 작성해야 합니다.

```typescript
function getFirstNumber(arr: number[]): number {
  return arr[0];
}
```

제네릭을 사용하면 모든 유형의 배열에서 작동할 수 있는 단일 함수를 작성할 수 있습니다.

```typescript
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}
```

함수 이름 뒤의 `<T>`는 모든 유형이 될 수 있는 유형 매개변수를 선언합니다. 나머지 함수는 실제 유형에 대한 자리 표시자로 'T'를 사용합니다.

## TypeScript에서 제네릭을 사용하는 방법

TypeScript에서 제네릭을 사용하려면 함수 또는 클래스 이름 뒤에 `<` 및 `>` 기호를 사용하여 유형 매개변수를 선언해야 합니다. 유형 매개변수에 임의의 이름을 사용할 수 있지만 관례적으로 'T'는 단일 유형 매개변수에 사용되고 'K' 및 'V'는 맵 및 사전의 키 및 값 유형에 사용됩니다.

다음은 동일한 유형의 두 인수를 사용하고 해당 값의 배열을 반환하는 일반 함수의 예입니다.

```typescript
function createArray<T>(a: T, b: T): T[] {
  return [a, b];
}
```

이 함수는 모든 유형이 될 수 있는 'T' 유형의 두 인수를 사용합니다. 이 함수는 인수와 동일한 유형인 `T`의 배열을 반환합니다.

단일 함수에서 여러 유형 매개변수를 사용할 수도 있습니다. 다음은 서로 다른 유형의 두 인수를 사용하고 해당 값을 가진 객체를 반환하는 함수의 예입니다.

```typescript
function createObject<K, V>(key: K, value: V): { [key: string]: V } {
  const obj = {};
  obj[key.toString()] = value;
  return obj;
}
```

이 함수는 `K` 및 `V` 유형의 두 인수를 사용합니다. 이 함수는 `문자열` 유형의 키와 `V` 유형의 값이 있는 객체를 반환합니다. 키는 `toString()` 메서드를 사용하여 문자열로 변환됩니다.

## 추가 정보

제네릭은 클래스, 인터페이스 및 함수와 함께 사용할 수 있습니다. 이를 통해 여러 유형에서 작동할 수 있는 재사용 가능성이 높은 코드를 작성할 수 있습니다.

제네릭을 사용할 때 형식 매개 변수의 제약 조건을 이해하는 것이 중요합니다. `extends` 키워드를 사용하여 유형 매개변수가 특정 유형의 하위 유형이어야 함을 지정할 수 있습니다.

예를 들어, `name` 속성이 있는 객체에서만 작동하는 함수가 있는 경우 type 매개변수가 `name` 속성이 있는 인터페이스를 확장해야 한다고 지정할 수 있습니다.

```typescript
interface Named {
  name: string;
}

function getName<T extends Named>(obj: T): string {
  return obj.name;
}
```

`<T extends Named>`는 `T`가 `name` 속성이 있는 `Named`의 하위 유형이어야 함을 선언합니다.

## 경고 및 위험

제네릭을 사용하면 코드가 더 복잡해지고 읽기 어려워질 수 있습니다. 필요할 때만 사용하고 코드를 최대한 단순하게 유지하는 것이 중요합니다.

제네릭을 사용할 때 너무 많은 유형 매개변수나 제약 조건을 만들지 않도록 주의하세요. 이로 인해 코드를 이해하고 유지하기가 더 어려워질 수 있습니다.

## 결론

제네릭은 유형 매개변수로 재사용 가능성이 높은 코드를 작성할 수 있게 해주는 TypeScript의 강력한 기능입니다. 코드를 더 유연하게 만들고 중복을 줄일 수 있습니다.

이 게시물에서는 TypeScript의 제네릭이 무엇인지, 제네릭을 사용해야 하는 이유 및 코드에서 사용하는 방법을 포함하여 TypeScript의 제네릭 기본 사항을 다뤘습니다. 이러한 지식을 바탕으로 TypeScript에서 보다 유연하고 재사용 가능한 코드 작성을 시작할 수 있습니다.

## 더 읽을 거리

- [TypeScript 제네릭](https://www.typescriptlang.org/docs/handbook/generics.html)
- [TypeScript Generics 튜토리얼](https://www.tutorialsteacher.com/typescript/typescript-generics)