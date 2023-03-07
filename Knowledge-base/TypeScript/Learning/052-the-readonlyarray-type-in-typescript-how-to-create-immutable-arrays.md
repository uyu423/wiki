---
title: 052: TypeScript의 ReadonlyArray 유형: 불변 배열을 만드는 방법
description: 
published: true
date: 2023-03-07T14:32:38.537Z
tags: 
editor: markdown
dateCreated: 2023-03-07T14:32:38.537Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [052: The ReadonlyArray Type in TypeScript: How to Create Immutable Arrays***English** document is available*](/en/Knowledge-base/TypeScript/Learning/052-the-readonlyarray-type-in-typescript-how-to-create-immutable-arrays)
{.links-list}



TypeScript의 ReadonlyArray 유형: 불변 배열을 만드는 방법

배열은 프로그래밍에서 가장 일반적으로 사용되는 데이터 구조 중 하나이며 TypeScript는 배열을 사용할 수 있는 많은 기능을 제공합니다. 그러나 때때로 우리는 일단 생성되면 수정할 수 없는 불변 배열을 생성해야 합니다. 이 게시물에서는 ReadonlyArray 유형을 사용하여 TypeScript에서 불변 배열을 만드는 방법을 살펴보겠습니다.

## ReadonlyArray 유형이 무엇인가요?

ReadonlyArray 유형은 TypeScript에 내장된 유형으로, 일단 생성되면 요소를 수정할 수 없는 배열을 나타냅니다. Array 유형과 비슷하지만 한 가지 중요한 차이점이 있습니다. ReadonlyArray 유형은 배열 요소에 대한 읽기 전용 액세스를 제공합니다.

다음은 TypeScript에서 ReadonlyArray를 만드는 방법의 예입니다.

```typescript
const myArray: ReadonlyArray<string> = ["foo", "bar", "baz"];
```

이 예제에서는 세 개의 요소가 있는 문자열의 ReadonlyArray를 만듭니다. 일단 생성되면 배열의 요소를 수정할 수 없습니다.

## 배열에서 ReadonlyArray 만들기

ReadonlyArray를 만드는 한 가지 방법은 기존 배열을 ReadonlyArray로 변환하는 것입니다. TypeScript는 이를 위한 편리한 방법인 `as const` 어설션을 제공합니다.

다음은 예입니다.

```typescript
const myArray = ["foo", "bar", "baz"] as const;
```

이 예제에서는 문자열 배열을 만든 다음 `as const` 어설션을 사용하여 ReadonlyArray로 변환합니다. 일단 생성되면 배열의 요소를 수정할 수 없습니다.

## ReadonlyArrays 및 가변성

ReadonlyArray 유형은 배열 요소에 대한 읽기 전용 액세스만 제공한다는 점에 유의해야 합니다. 배열이 다른 방식으로 수정되는 것을 막지는 않습니다. 예를 들어 ReadonlyArray에서 요소를 계속 추가하거나 제거할 수 있습니다.

```typescript
const myArray: ReadonlyArray<string> = ["foo", "bar", "baz"];

// This will throw a TypeError:
myArray[0] = "qux";

// This is allowed:
myArray.push("qux");
```

이 예제에서는 TypeError를 발생시키는 ReadonlyArray의 첫 번째 요소를 수정하려고 시도합니다. 그러나 `push` 메서드를 사용하여 배열에 요소를 계속 추가할 수 있습니다.

## ReadonlyArrays 및 유형 추론

TypeScript에는 탁월한 유형 추론 기능이 있으며 이는 ReadonlyArrays로 확장됩니다. `as const` 어설션을 사용하여 ReadonlyArray를 만들 때 TypeScript는 배열 요소에 대한 올바른 유형을 유추합니다.

다음은 예입니다.

```typescript
const myArray = ["foo", "bar", "baz"] as const;

// TypeScript infers that myArray is a ReadonlyArray<string>.
```

이 예에서 TypeScript는 `myArray`가 문자열의 ReadonlyArray라고 추론합니다.

## ReadonlyArray 작업

ReadonlyArray로 작업하는 것은 일반 배열로 작업하는 것과 비슷합니다. 대괄호 표기법을 사용하여 요소에 액세스하고 for 루프 또는 `forEach` 메서드를 사용하여 요소를 반복할 수 있습니다.

다음은 예입니다.

```typescript
const myArray: ReadonlyArray<string> = ["foo", "bar", "baz"];

// Accessing elements:
const firstElement = myArray[0]; // "foo"

// Iterating over elements:
myArray.forEach((element) => {
  console.log(element);
});
```

이 예제에서는 대괄호 표기법을 사용하여 ReadonlyArray의 첫 번째 요소에 액세스하고 `forEach` 메서드를 사용하여 요소를 반복합니다.

## 추가 정보

- ReadonlyArray 유형은 TypeScript 3.4 이상에서만 사용할 수 있습니다.
- ReadonlyArray 유형은 깊은 읽기 전용 유형입니다. 즉, 모든 중첩 개체 또는 배열도 읽기 전용입니다.

## 결론

이 게시물에서는 ReadonlyArray 유형을 사용하여 TypeScript에서 불변 배열을 만드는 방법을 살펴보았습니다. 배열에서 ReadonlyArray를 생성하는 방법, ReadonlyArray가 가변성과 함께 작동하는 방법 및 ReadonlyArray로 작동하는 방법을 배웠습니다. 이 지식을 통해 TypeScript 프로젝트에서 보다 강력하고 예측 가능한 코드를 만들 수 있습니다.

## 더 읽을거리

- [TypeScript 핸드북: ReadonlyArray](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html# readonlyarrayt)
- [TypeScript 심층 읽기 전용](https://devblogs.microsoft.com/typescript/announcing-typescript-3-4-rc/# deep-readonly)