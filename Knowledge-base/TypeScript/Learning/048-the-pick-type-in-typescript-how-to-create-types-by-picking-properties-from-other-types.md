---
title: 048: TypeScript에서 유형 선택: 다른 유형에서 속성을 선택하여 유형을 만드는 방법
description: 
published: true
date: 2023-03-06T21:32:46.365Z
tags: 
editor: markdown
dateCreated: 2023-03-06T21:32:39.043Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [048: The Pick Type in TypeScript: How to Create Types by Picking Properties from Other Types***English** document is available*](/en/Knowledge-base/TypeScript/Learning/048-the-pick-type-in-typescript-how-to-create-types-by-picking-properties-from-other-types)
{.links-list}



TypeScript의 유형 선택: 다른 유형에서 속성을 선택하여 유형을 만드는 방법

TypeScript는 확장 가능하고 유지 관리 가능한 애플리케이션을 구축하는 데 널리 사용되는 언어입니다. TypeScript의 주요 기능 중 하나는 유형을 정의하고 사용하는 기능입니다. 이 게시물에서는 다른 유형에서 속성을 선택하여 새 유형을 생성할 수 있는 TypeScript의 Pick 유형을 살펴보겠습니다.

## 선택 유형이 무엇인가요?

Pick 유형은 기존 유형에서 속성을 선택하여 새 유형을 생성할 수 있는 TypeScript의 내장 유틸리티 유형입니다. 두 가지 유형 인수를 사용합니다. 첫 번째 인수는 소스 유형이고 두 번째 인수는 선택할 속성의 이름을 나타내는 문자열 리터럴 또는 문자열 리터럴의 합집합입니다.

다음은 선택 유형을 사용하는 방법의 예입니다.

```typescript
type Person = {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
    country: string;
  };
};

type PersonName = Pick<Person, 'name'>;
```

이 예제에서는 이름, 나이 및 주소의 세 가지 속성을 사용하여 Person 유형을 정의했습니다. 그런 다음 Pick 유형을 사용하고 Person 유형을 소스 유형으로 지정하고 문자열 리터럴 'name'을 선택할 속성으로 지정하여 PersonName이라는 새 유형을 만듭니다. 결과 유형은 Person 유형의 이름 속성만 있는 새 유형입니다.

## Pick을 사용하여 하위 유형 만들기

Pick 유형은 기존 유형의 하위 유형을 만들 때 특히 유용합니다. 예를 들어 많은 속성이 있는 사용자 유형이 있지만 특정 사용 사례에 대해 해당 속성의 하위 집합만 필요하다고 가정합니다. Pick 유형을 사용하여 필요한 속성만 포함하는 새 유형을 만들 수 있습니다.

예를 들면 다음과 같습니다.

```typescript
type User = {
  id: number;
  name: string;
  email: string;
  createdAt: Date;
  updatedAt: Date;
};

type UserSummary = Pick<User, 'id' | 'name'>;
```

이 예제에서는 id, name, email, createdAt 및 updatedAt를 포함하여 5개의 속성을 사용하여 User 유형을 정의합니다. 그런 다음 Pick 유형을 사용하고 User 유형을 소스 유형으로 지정하고 선택할 속성으로 문자열 리터럴('id' 및 'name')의 합집합을 지정하여 UserSummary라는 새 유형을 만듭니다. 결과 유형은 User 유형의 id 및 name 속성만 포함하는 새 유형입니다.

## 추가 정보

Pick 유형은 지정된 속성만 포함하는 새 유형을 생성한다는 점에 유의해야 합니다. 소스 유형의 다른 특성은 새 유형에 포함되지 않습니다. 하위 유형을 만들 때 유용할 수 있지만 주의하지 않으면 예기치 않은 동작이 발생할 수도 있습니다.

## 중첩 속성과 함께 Pick 사용

Pick 유형은 중첩 속성과 함께 사용할 수도 있습니다. 예를 들어 거리, 도시 및 국가에 대한 중첩된 속성을 포함하는 address 속성이 있는 Person 유형이 있다고 가정합니다. Pick 유형을 사용하여 거리 및 도시 속성만 포함하는 새 유형을 만들 수 있습니다.

예를 들면 다음과 같습니다.

```typescript
type Person = {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
    country: string;
  };
};

type PersonAddress = Pick<Person['address'], 'street' | 'city'>;
```

이 예제에서는 Pick 유형을 사용하고 Person 유형의 주소 속성을 소스 유형으로 지정하고 문자열 리터럴('street' 및 'city')의 합집합을 선택할 속성으로 지정하여 PersonAddress라는 새 유형을 만듭니다. 결과 유형은 Person 유형의 주소 속성에서 거리 및 도시 속성만 포함하는 새 유형입니다.

## 경고

중첩 속성과 함께 Pick 유형을 사용하는 경우 결과 유형에는 전체 중첩 개체가 아니라 지정된 속성만 포함된다는 점을 기억하는 것이 중요합니다. 전체 중첩 개체를 사용해야 하는 경우 선택한 유형 대신 원래 유형을 사용해야 합니다.

## 결론

TypeScript의 Pick 유형은 기존 유형에서 속성을 선택하여 새 유형을 생성하는 강력한 도구입니다. 하위 유형을 만들거나 중첩된 속성으로 작업할 때 특히 유용할 수 있습니다. 그러나 Pick 유형을 신중하게 사용하고 결과 유형에 지정된 속성만 포함한다는 점을 기억하는 것이 중요합니다.

## 더 읽을거리

- TypeScript 핸드북: [유틸리티 유형](https://www.typescriptlang.org/docs/handbook/utility-types.html# picktypekeys)
- TypeScript 심층 분석: [유형 유틸리티 함수](https://basarat.gitbook.io/typescript/type-system/typeutilityfunctions)