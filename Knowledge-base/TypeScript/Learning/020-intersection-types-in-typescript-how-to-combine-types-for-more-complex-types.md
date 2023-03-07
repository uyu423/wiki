---
title: 020: TypeScript의 교차 유형: 더 복잡한 유형을 위해 유형을 결합하는 방법
description: 
published: true
date: 2023-03-07T05:32:34.311Z
tags: 
editor: markdown
dateCreated: 2023-03-07T05:32:34.311Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [020: Intersection Types in TypeScript: How to Combine Types for More Complex Types***English** document is available*](/en/Knowledge-base/TypeScript/Learning/020-intersection-types-in-typescript-how-to-combine-types-for-more-complex-types)
{.links-list}



TypeScript의 교차 유형: 더 복잡한 유형을 위해 유형을 결합하는 방법

TypeScript는 JavaScript의 상위 집합입니다. 언어에 정적 타이핑을 추가하여 컴파일 시간에 오류를 더 쉽게 잡을 수 있습니다. TypeScript에는 교차 유형을 포함하여 개발자가 더 나은 코드를 작성하는 데 도움이 되는 많은 기능이 있습니다. 교차 유형을 사용하면 개발자가 여러 유형을 단일 유형으로 결합할 수 있습니다. 이는 복잡한 데이터 구조 또는 API로 작업할 때 유용할 수 있습니다.

이 게시물에서는 TypeScript의 교차 유형을 탐색하고 이를 사용하여 더 복잡한 유형을 만드는 방법을 배웁니다.

## 교차점 유형이란 무엇입니까?

교차 유형을 사용하면 개발자가 여러 유형을 단일 유형으로 결합할 수 있습니다. 이는 변수가 여러 유형의 모든 속성과 메서드를 가질 수 있음을 의미합니다. 예를 들어 `A`와 `B` 두 가지 유형이 있는 경우 `A`와 `B` 모두의 속성과 메서드를 모두 포함하는 새로운 유형 `C`를 만들 수 있습니다.

```typescript
type A = {
  foo: string;
};

type B = {
  bar: number;
};

type C = A & B;

const c: C = {
  foo: "Hello",
  bar: 42,
};
```

위의 예에는 'A'와 'B' 두 가지 유형이 있습니다. 그런 다음 `&` 연산자를 사용하여 `A`와 `B`의 속성을 결합하는 새로운 유형 `C`를 만듭니다. 마지막으로 `A`와 `B`의 모든 속성을 가진 `C` 유형의 변수 `c`를 만듭니다.

## 함수에서 교차 유형 사용

교차 유형은 함수에서도 사용할 수 있습니다. 이는 복잡한 데이터 구조를 반환하는 API로 작업할 때 유용할 수 있습니다. 예를 들어 다음 속성을 가진 사용자 개체를 반환하는 API가 있다고 가정해 보겠습니다.

```typescript
type User = {
  id: number;
  name: string;
  email: string;
};
```

또한 사용자 개체를 가져와서 사용자의 이름과 이메일을 기록하는 함수도 있습니다.

```typescript
function logUser(user: User) {
  console.log(`Name: ${user.name}, Email: ${user.email}`);
}
```

이제 추가 속성이 있는 사용자 개체를 반환하는 또 다른 API가 있다고 가정해 보겠습니다.

```typescript
type AdminUser = {
  id: number;
  name: string;
  email: string;
  isAdmin: boolean;
};
```

`logUser` 기능을 사용하여 `AdminUser` 객체의 이름과 이메일을 기록하려고 합니다. 교차 유형을 사용하여 이를 수행할 수 있습니다.

```typescript
type LogAdminUser = AdminUser & {
  isAdmin: never;
};

function logAdminUser(user: LogAdminUser) {
  logUser(user);
}
```

위의 예에서 `AdminUser` 속성과 속성이 없음을 의미하는 `never` 유형의 개체를 결합하는 새로운 유형 `LogAdminUser`를 생성합니다. 그런 다음 `LogAdminUser` 개체를 가져와 해당 개체로 `logUser` 함수를 호출하는 새 함수 `logAdminUser`를 만듭니다. 이를 통해 `User` 및 `AdminUser` 개체 모두에서 `logUser` 기능을 사용할 수 있습니다.

## 추가 정보

교차 유형을 사용할 때 결과 유형에는 두 유형의 모든 속성과 메서드가 포함된다는 점을 기억하는 것이 중요합니다. 두 형식에 이름이 같은 속성이나 메서드가 있으면 충돌이 발생할 수 있습니다. 이 경우 TypeScript는 오류를 생성합니다.

## 결론

교차 유형은 개발자가 여러 유형을 단일 유형으로 결합할 수 있는 TypeScript의 강력한 기능입니다. 이는 복잡한 데이터 구조 또는 API로 작업할 때 유용할 수 있습니다. 이 게시물에서는 교차 유형을 사용하여 더 복잡한 유형을 만들고 함수에서 사용하는 방법을 배웠습니다. 또한 교차 유형을 사용할 때 발생할 수 있는 충돌에 대해서도 배웠습니다.

TypeScript에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

- [TypeScript 핸드북](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript 심층 분석](https://basarat.gitbook.io/typescript/)
- [5분 안에 TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)