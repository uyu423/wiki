---
title: 053: TypeScript의 필수 유형: 필수 속성으로 유형을 만드는 방법
description: 
published: true
date: 2023-03-04T08:32:36.740Z
tags: 
editor: markdown
dateCreated: 2023-03-04T08:32:29.499Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [053: The Required Type in TypeScript: How to Create Types with Required Properties***English** document is available*](/en/Knowledge-base/TypeScript/Learning/053-the-required-type-in-typescript-how-to-create-types-with-required-properties)
{.links-list}


TypeScript의 필수 유형: 필수 속성이 있는 유형을 만드는 방법

TypeScript는 개발자에게 깨끗하고 유지 관리 가능한 코드를 작성할 수 있는 기능을 제공하는 강력한 언어입니다. TypeScript가 제공하는 기능 중 하나는 필수 속성으로 유형을 정의하는 기능입니다. 이 게시물에서는 필수 유형이 무엇인지, 필수 속성을 사용하여 유형을 만드는 방법에 대해 알아봅니다.

## 필수 유형 이해

필수 유형은 개발자가 필수 속성이 있는 유형을 정의할 수 있도록 하는 TypeScript의 기본 제공 유형입니다. 속성이 필수로 정의되면 속성이 개체에 있어야 하며 정의되지 않거나 null일 수 없음을 의미합니다.

예를 들어, `name`과 `age`라는 두 가지 속성을 가진 `Person`이라는 객체가 있다고 가정해 보겠습니다. `name` 속성을 필수로 만들기 위해 다음과 같이 `Person` 유형을 정의할 수 있습니다.

```typescript
type Person = {
  name: string;
  age?: number;
}
```

이 예에서 `age` 속성은 선택 사항이지만 `name` 속성은 필수입니다. `name` 속성 없이 `Person` 객체를 만들려고 하면 TypeScript에서 오류가 발생합니다.

```typescript
const person = {
  age: 30
} // Error: Property 'name' is missing in type '{ age: number; }' but required in type 'Person'.
```

## 필수 속성으로 유형 만들기

필수 속성이 있는 유형을 생성하려면 `필수` 유틸리티 유형을 사용할 수 있습니다. `필수` 유형은 개체 유형을 인수로 사용하고 모든 속성이 필수로 설정된 새 유형을 반환합니다.

```typescript
type RequiredPerson = Required<Person>;
```

이 예제에서는 `Person` 유형에 `Required` 유틸리티 유형을 적용하여 `RequiredPerson` 유형을 생성합니다. 결과 유형에는 `name` 속성을 포함하여 모든 속성이 필수로 설정됩니다.

```typescript
const requiredPerson: RequiredPerson = {
  name: 'John',
  age: 30
} // OK

const missingName: RequiredPerson = {
  age: 30
} // Error: Property 'name' is missing in type '{ age: number; }' but required in type 'RequiredPerson'.
```

## 깊게 중첩된 객체로 작업하기

`Required` 유형은 깊게 중첩된 개체에서 필수 속성이 있는 유형을 만드는 데 사용할 수도 있습니다. `street`와 `city`라는 두 가지 속성을 가진 `Address`라는 객체가 있다고 가정해 봅시다. `street` 및 `city` 속성을 포함하여 모든 속성이 필수로 설정된 `RequiredAddress`라는 새 유형을 만들 수 있습니다.

```typescript
type Address = {
  street?: string;
  city?: string;
}

type Person = {
  name: string;
  age?: number;
  address?: Address;
}

type RequiredPerson = Required<Person>;
```

이 예제에서는 `Address` 유형의 개체인 선택적 `address` 속성을 사용하여 `Person` 유형을 정의합니다. 그런 다음 `Required` 유틸리티 유형을 `Person` 유형에 적용하여 모든 속성이 required로 설정된 `RequiredPerson` 유형을 생성합니다.

```typescript
const requiredPerson: RequiredPerson = {
  name: 'John',
  age: 30,
  address: {
    street: '123 Main St',
    city: 'New York'
  }
} // OK

const missingAddress: RequiredPerson = {
  name: 'John',
  age: 30
} // Error: Property 'address' is missing in type '{ name: string; age: number; }' but required in type 'RequiredPerson'.
```

## 추가 정보

필수 속성이 있는 유형을 정의할 때 사용 사례를 고려하고 필수로 설정된 속성이 개체가 올바르게 작동하는 데 필요한지 확인하는 것이 중요합니다. 필수 속성을 과도하게 사용하면 불필요한 오류가 발생하고 코드 유지 관리가 어려워질 수 있습니다.

## 결론

이 게시물에서는 TypeScript에서 필요한 유형과 필수 속성이 있는 유형을 만드는 방법을 살펴보았습니다. 모든 속성이 필수로 설정된 새 유형을 만들기 위해 '필수' 유틸리티 유형을 사용하는 방법과 깊게 중첩된 개체로 작업하는 방법을 배웠습니다. 필요한 유형을 사용하여 개체가 올바르게 작동하고 깨끗하고 유지 관리 가능한 코드를 작성하는 데 필요한 속성을 갖도록 할 수 있습니다.

## 더 읽을 거리

- [TypeScript 핸드북: 필수 속성](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html# optional-props-become-readonly-when-used-in-interfaces -및 유형 리터럴)
- [TypeScript 핸드북: 유틸리티 유형](https://www.typescriptlang.org/docs/handbook/utility-types.html# required)