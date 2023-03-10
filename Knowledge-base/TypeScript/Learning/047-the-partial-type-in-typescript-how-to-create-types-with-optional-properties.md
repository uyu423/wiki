---
title: 047: TypeScript의 부분 유형: 선택적 속성을 사용하여 유형을 만드는 방법
description: 
published: true
date: 2023-03-10T16:32:42.685Z
tags: 
editor: markdown
dateCreated: 2023-03-10T16:32:42.685Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [047: The Partial Type in TypeScript: How to Create Types with Optional Properties***English** document is available*](/en/Knowledge-base/TypeScript/Learning/047-the-partial-type-in-typescript-how-to-create-types-with-optional-properties)
{.links-list}



TypeScript의 부분 유형: 선택적 속성을 사용하여 유형을 만드는 방법

TypeScript는 코드에 유형 주석을 추가하는 JavaScript의 상위 집합입니다. 개발자가 런타임이 아닌 컴파일 타임에 오류를 포착하여 코드 유지 및 리팩터링이 더 쉬워집니다. TypeScript의 가장 유용한 기능 중 하나는 사용자 정의 유형을 생성하는 기능입니다.

이 게시물에서는 TypeScript의 Partial 유형을 탐색하여 선택적 속성이 있는 유형을 만들 수 있습니다. 부분 유형 생성의 기본 사항, 함수에서 부분 유형을 사용하는 방법 및 작업을 위한 몇 가지 모범 사례를 다룰 것입니다.

## 부분 유형이란 무엇입니까?

TypeScript의 부분 유형은 기존 유형의 모든 속성이 선택 사항으로 설정된 새 유형을 만들 수 있는 내장 유틸리티 유형입니다. 이는 일부 필수 속성과 선택적 속성이 있는 유형을 만들 수 있음을 의미합니다.

다음은 TypeScript의 간단한 인터페이스 예입니다.

```typescript
interface Person {
    name: string;
    age: number;
    email: string;
}
```

이름과 이메일만 필요한 유형을 만들려면 Partial 유형을 사용하여 age 속성을 선택 사항으로 만들 수 있습니다.

```typescript
type PartialPerson = Partial<Person>;

const person: PartialPerson = {
    name: 'John Doe',
    email: 'john.doe@example.com'
};
```

이 예에서는 Partial 유틸리티 유형을 사용하여 PartialPerson이라는 새 유형을 만들었습니다. 그런 다음 name 및 email 속성만 포함하는 person이라는 유형의 개체를 만들었습니다.

## 함수에서 부분 유형 사용

부분 유형은 개체를 인수로 사용하는 함수로 작업할 때 특히 유용합니다. 예를 살펴보겠습니다.

```typescript
function updatePerson(person: Person, updates: Partial<Person>): Person {
    return { ...person, ...updates };
}

const originalPerson: Person = {
    name: 'John Doe',
    age: 30,
    email: 'john.doe@example.com'
};

const updatedPerson = updatePerson(originalPerson, { age: 31 });
```

이 예제에서는 두 개의 인수인 Person 개체와 Partial<Person> 개체를 사용하는 updatePerson이라는 함수를 정의했습니다. 이 함수는 업데이트가 적용된 새 Person 개체를 반환합니다.

그런 다음 이름, 나이 및 이메일이 포함된 originalPerson 개체를 만들었습니다. 이 개체와 age 속성만 있는 Partial<Person> 개체를 updatePerson 함수에 전달했습니다. 이 함수는 업데이트된 age 속성이 있는 새 Person 개체를 반환합니다.

## 부분 유형 작업을 위한 모범 사례

부분 유형으로 작업할 때 염두에 두어야 할 몇 가지 모범 사례가 있습니다.

- 부분 유형을 아껴서 사용: 부분 유형이 유용할 수 있지만 과도하게 사용하면 코드를 읽고 유지 관리하기가 더 어려워집니다. 필요한 경우에만 사용하십시오.

- 가능한 경우 필수 속성 사용: 속성이 필수인 경우 Partial 유형으로 선택 사항으로 만드는 대신 필수 속성을 사용합니다.

- 복잡한 객체에 부분 유형 사용 금지: 부분 유형은 단순 객체에 가장 적합합니다. 개체에 복잡한 중첩 속성이 있는 경우 대신 사용자 지정 유형을 만드는 것이 더 나을 수 있습니다.

## 결론

TypeScript의 부분 유형은 선택적 속성이 있는 유형을 생성하기 위한 강력한 도구입니다. 특히 개체를 인수로 사용하는 함수로 작업할 때 보다 유연하고 재사용 가능한 코드를 만들 수 있습니다.

Partial 유형은 필요한 경우에만 드물게 사용하십시오. 가능한 경우 필수 속성을 사용하고 복잡한 객체에 부분 유형을 사용하지 마십시오.

추가 정보:
- 부분 유형에 대한 공식 TypeScript 문서: https://www.typescriptlang.org/docs/handbook/utility-types.html# partialtype
- 부분 유형을 실험하기 위한 TypeScript 플레이그라운드: https://www.typescriptlang.org/play?# code/PTAEBcDWAIFoEsB2BvApgWwM4BnALgQwE8gG8oBvKAvhPABQAdgJxwBQwK4BzgF4A7gBzA4uAL4Amg4uALZLgD4sAFAFwABwA1IA
- 부분 유형에 대한 TypeScript 심층 분석 책: https://basarat.gitbook.io/typescript/type-system/utility-types# partial