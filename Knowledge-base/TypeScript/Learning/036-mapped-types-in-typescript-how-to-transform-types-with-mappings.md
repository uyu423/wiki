---
title: 036: TypeScript의 매핑된 유형: 매핑으로 유형을 변환하는 방법
description: 
published: true
date: 2023-03-03T07:32:25.941Z
tags: 
editor: markdown
dateCreated: 2023-03-03T07:32:24.540Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [036: Mapped Types in TypeScript: How to Transform Types with Mappings***English** document is available*](/en/Knowledge-base/TypeScript/Learning/036-mapped-types-in-typescript-how-to-transform-types-with-mappings)
{.links-list}


TypeScript의 매핑된 유형: 매핑을 사용하여 유형을 변환하는 방법

TypeScript는 JavaScript의 상위 집합인 오픈 소스 언어입니다. 코드를 보다 안정적으로 만들고 오류를 방지하는 데 도움이 되는 정적 타이핑을 제공합니다. TypeScript의 주요 기능 중 하나는 매핑된 유형입니다. 매핑된 유형은 한 유형의 속성을 다른 유형에 매핑하여 유형을 변환하는 방법을 제공합니다. 이 게시물에서는 TypeScript에서 매핑된 유형을 살펴보고 사용 방법을 배웁니다.

## 매핑된 유형 소개

매핑된 유형은 한 유형에서 다른 유형으로 속성을 매핑하여 유형을 변환할 수 있는 TypeScript의 기능입니다. 이는 기존 유형을 기반으로 하지만 약간의 수정이 필요한 새 유형을 생성해야 할 때 유용할 수 있습니다. 예를 들어 기존 유형의 모든 속성이 있지만 일부 속성은 선택 사항인 새 유형을 만들 수 있습니다. 매핑된 유형은 이를 달성하는 데 도움이 될 수 있습니다.

## 기본 매핑 유형

가장 기본적인 매핑 유형은 `Partial` 유형입니다. `Partial` 유형은 모든 속성을 선택 사항으로 만들어 유형을 변환합니다. 다음은 예입니다.

```typescript
interface Person {
  name: string;
  age: number;
}

type PartialPerson = Partial<Person>;

const partialPerson: PartialPerson = { name: "John" };
```

이 예제에서는 `name`과 `age`라는 두 가지 속성을 사용하여 `Person` 인터페이스를 정의합니다. 그런 다음 `Partial` 매핑 유형을 사용하여 새 유형 `PartialPerson`을 정의합니다. 이 유형은 `Person`과 동일한 속성을 갖지만 모든 속성이 선택 사항입니다. 그런 다음 `PartialPerson` 유형의 `partialPerson` 변수를 만들고 `name` 속성만 지정된 개체에 할당합니다.

## 제약 조건이 있는 매핑된 유형

매핑된 유형은 제약 조건과 함께 사용할 수도 있습니다. 제약 조건을 사용하면 매핑할 수 있는 속성을 제한할 수 있습니다. 예를 들어 제외하려는 몇 가지 속성을 제외하고 기존 유형의 모든 속성을 포함하는 새 유형을 만들 수 있습니다. 다음은 예입니다.

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type ExcludeAddress<T> = {
  [P in keyof T as Exclude<P, "address">]: T[P];
};

const person: Person = { name: "John", age: 30, address: "123 Main St." };
const personWithoutAddress: ExcludeAddress<Person> = person;
```

이 예제에서는 `name`, `age` 및 `address`의 세 가지 속성을 사용하여 인터페이스 `Person`을 정의합니다. 그런 다음 제약 조건이 있는 매핑된 유형을 사용하여 새 유형 `ExcludeAddress`를 정의합니다. 제약 조건은 유형의 키를 공용체 유형으로 반환하는 'keyof' 키워드를 사용하여 지정됩니다. 그런 다음 'Exclude' 유틸리티 유형을 사용하여 통합 유형에서 'address' 속성을 제외합니다. 결과 유형은 `address` 속성을 제외한 `Person`의 모든 속성을 가진 새로운 유형입니다.

그런 다음 `Person` 유형의 `person` 변수를 만들고 세 가지 속성이 모두 지정된 객체를 할당합니다. 그런 다음 `ExcludeAddress<Person>` 유형의 `personWithoutAddress` 변수를 만들고 `person` 객체에 할당합니다. `personWithoutAddress` 객체는 `address` 속성을 제외하고 `person`의 모든 속성을 가집니다.

## 선택적 속성이 있는 매핑된 유형

매핑된 유형을 사용하여 선택적 속성이 있는 유형을 만들 수도 있습니다. 다음은 예입니다.

```typescript
interface Person {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
    state: string;
  };
}

type PartialAddress<T> = {
  [P in keyof T]: P extends "address" ? Partial<T[P]> : T[P];
};

const person: Person = {
  name: "John",
  age: 30,
  address: { street: "123 Main St.", city: "Anytown", state: "CA" },
};

const personWithPartialAddress: PartialAddress<Person> = {
  name: "John",
  age: 30,
  address: { street: "123 Main St." },
};
```

이 예제에서는 `name`, `age` 및 `address`의 세 가지 속성을 사용하여 인터페이스 `Person`을 정의합니다. `address` 속성은 `street`, `city` 및 `state`의 세 가지 속성을 가진 개체입니다. 그런 다음 선택적 속성이 있는 매핑된 유형을 사용하여 새 유형 `PartialAddress`를 정의합니다. `Partial` 유틸리티 유형은 `address` 속성을 선택 사항으로 만드는 데 사용됩니다. 결과 유형은 `Person`의 모든 속성을 포함하는 새로운 유형이며 `address` 속성은 선택 사항입니다.

그런 다음 `Person` 유형의 `person` 변수를 만들고 세 가지 속성이 모두 지정된 객체를 할당합니다. 그런 다음 `PartialAddress<Person>` 유형의 `personWithPartialAddress` 변수를 만들고 `name` 및 `age` 속성만 지정하고 `address` 속성은 선택 사항인 개체에 할당합니다.

## 결론

매핑된 유형은 한 유형에서 다른 유형으로 속성을 매핑하여 유형을 변환할 수 있는 TypeScript의 강력한 기능입니다. 선택적 속성, 제외 속성 등을 사용하여 새 유형을 만드는 데 사용할 수 있습니다. 매핑된 유형을 사용하면 코드를 보다 유연하고 쉽게 사용할 수 있습니다.

## 추가 정보

- 매핑된 유형에 대한 TypeScript 핸드북: https://www.typescriptlang.org/docs/handbook/2/mapped-types.html

## 경고

- 매핑된 타입을 사용할 때 순환 참조를 만들지 않도록 주의한다. 이로 인해 TypeScript가 무한 루프에 들어가 충돌이 발생할 수 있습니다.

## 위험

- 매핑된 유형은 복잡하고 이해하기 어려울 수 있습니다. 코드에서 사용하기 전에 설명서를 읽고 예제를 이해하는 것이 중요합니다.

