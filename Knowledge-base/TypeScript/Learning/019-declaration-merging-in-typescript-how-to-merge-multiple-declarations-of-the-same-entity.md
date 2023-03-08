---
title: 019: TypeScript에서 선언 병합: 동일한 엔티티의 여러 선언을 병합하는 방법
description: 
published: true
date: 2023-03-04T15:32:33.534Z
tags: 
editor: markdown
dateCreated: 2023-03-04T15:32:32.182Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [019: Declaration Merging in TypeScript: How to Merge Multiple Declarations of the Same Entity***English** document is available*](/en/Knowledge-base/TypeScript/Learning/019-declaration-merging-in-typescript-how-to-merge-multiple-declarations-of-the-same-entity)
{.links-list}


## 소개

TypeScript에서 소프트웨어를 개발할 때 동일한 엔터티를 여러 번 선언해야 하는 시나리오를 접할 수 있습니다. 이는 외부 라이브러리로 작업하거나 기존 유형을 확장하려는 경우에 발생할 수 있습니다. 이러한 경우 TypeScript는 동일한 엔터티의 여러 선언을 단일 정의로 병합할 수 있는 "선언 병합"이라는 기능을 제공합니다.

이번 포스트에서는 TypeScript에서 Declaration Merging의 개념을 살펴보고 이를 효과적으로 사용하는 방법에 대해 알아보겠습니다.

## 선언 병합이란 무엇입니까?

선언 병합은 동일한 엔터티의 여러 선언을 단일 정의로 결합할 수 있는 TypeScript의 기능입니다. 이 기능은 자체 유형 정의가 있는 외부 라이브러리로 작업하거나 기존 유형을 확장하려는 경우에 유용합니다.

선언 병합은 동일한 엔터티의 선언을 집계하고 각 선언의 모든 속성과 메서드를 포함하는 단일 정의를 만드는 방식으로 작동합니다. 이는 인터페이스, 클래스, 함수 및 네임스페이스에 대해 수행할 수 있습니다.

## 선언 병합 사용 방법

TypeScript에서 선언 병합을 사용하려면 몇 가지 규칙을 따라야 합니다.

1. 모든 선언은 동일한 이름과 동일한 범위에 있어야 합니다.
2. 선언에는 호환 가능한 유형이 있어야 합니다.
3. 선언에는 private 또는 protected 멤버가 없어야 합니다.

선언 병합을 사용하는 방법을 이해하기 위해 몇 가지 예를 살펴보겠습니다.

### 인터페이스 병합

이름이 같은 두 개의 인터페이스가 있다고 가정합니다.

```typescript
interface Person {
  name: string;
}

interface Person {
  age: number;
}
```

이 경우 TypeScript는 자동으로 두 인터페이스를 단일 정의로 병합합니다.

```typescript
interface Person {
  name: string;
  age: number;
}
```

이제 `name` 및 `age` 속성과 함께 `Person` 인터페이스를 사용할 수 있습니다.

### 함수 병합

동일한 이름을 가진 두 개의 함수가 있다고 가정합니다.

```typescript
function greet(name: string): void {
  console.log(`Hello, ${name}!`);
}

function greet(message: number): void {
  console.log(`Your message has ${message} characters.`);
}
```

이 경우 TypeScript는 자동으로 두 함수를 단일 정의로 병합합니다.

```typescript
function greet(name: string): void;
function greet(message: number): void;
function greet(nameOrMessage: string | number): void {
  if (typeof nameOrMessage === 'string') {
    console.log(`Hello, ${nameOrMessage}!`);
  } else {
    console.log(`Your message has ${nameOrMessage} characters.`);
  }
}
```

이제 문자열 또는 숫자 인수를 사용하여 `greet` 함수를 호출할 수 있습니다.

### 네임스페이스 병합

동일한 이름을 가진 두 개의 네임스페이스가 있다고 가정합니다.

```typescript
namespace MyNamespace {
  export const name = 'John';
}

namespace MyNamespace {
  export const age = 30;
}
```

이 경우 TypeScript는 자동으로 두 네임스페이스를 단일 정의로 병합합니다.

```typescript
namespace MyNamespace {
  export const name = 'John';
  export const age = 30;
}
```

이제 `MyNamespace` 네임스페이스의 `name` 및 `age` 속성에 모두 액세스할 수 있습니다.

## 추가 정보

다음은 선언 병합 작업 시 유의해야 할 몇 가지 추가 사항입니다.

- `declare` 키워드를 사용하여 선언이 외부적이며 런타임에 제공될 것임을 TypeScript에 알릴 수 있습니다. 이는 자체 유형 정의가 있는 라이브러리로 작업할 때 유용합니다.
- `namespace` 키워드를 사용하여 관련 선언을 함께 그룹화할 수 있습니다. 이는 많은 수의 선언이 있고 이를 논리적 그룹으로 구성하려는 경우에 유용합니다.
- 선언 병합을 사용하여 기존 형식에 새 속성이나 메서드를 추가할 수 있습니다. 이는 원래 정의를 수정하지 않고 기존 유형을 확장하려는 경우에 유용합니다.

## 결론

선언 병합은 동일한 엔터티의 여러 선언을 단일 정의로 결합할 수 있는 TypeScript의 강력한 기능입니다. 이 기능은 외부 라이브러리로 작업하거나 기존 유형을 확장하려는 경우에 유용합니다.

이 게시물에 설명된 규칙과 지침을 따르면 Declaration Merging을 효과적으로 사용하고 TypeScript 코드의 품질을 향상시킬 수 있습니다.

## 더 읽을거리

- [TypeScript 핸드북: 선언 병합](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)
- [TypeScript 심층 분석: 선언 병합](https://basarat.gitbook.io/typescript/type-system/declaration-merging)