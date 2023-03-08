---
title: 028: TypeScript의 선택적 연결: 중첩된 속성 및 메서드에 안전하게 액세스하는 방법
description: 
published: true
date: 2023-03-02T22:32:19.515Z
tags: 
editor: markdown
dateCreated: 2023-03-02T22:32:12.437Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [028: Optional Chaining in TypeScript: How to Safely Access Nested Properties and Methods***English** document is available*](/en/Knowledge-base/TypeScript/Learning/028-optional-chaining-in-typescript-how-to-safely-access-nested-properties-and-methods)
{.links-list}


## 소개

TypeScript에서 중첩된 속성 및 메서드에 액세스하는 것은 특히 선택적 값을 처리할 때 약간 까다로울 수 있습니다. 다행스럽게도 TypeScript는 이 작업을 단순화하는 선택적 연결이라는 기능을 제공합니다. 이 글에서는 옵셔널 체이닝이 무엇인지, 어떻게 작동하는지, TypeScript에서 어떻게 사용하는지 살펴보겠습니다.

## 옵셔널 체이닝이란?

선택적 연결은 TypeScript 버전 3.7에 도입된 기능으로, 일부 중간 값이 null이거나 정의되지 않은 경우에도 개발자가 개체의 중첩된 속성 및 메서드에 안전하게 액세스할 수 있도록 합니다.

옵셔널 체이닝이 도입되기 전에 개발자는 액세스하기 전에 각 중간 속성이나 메서드가 존재하는지 확인하기 위해 길고 오류가 발생하기 쉬운 코드를 작성해야 했습니다. 옵셔널 체이닝을 통해 개발자는 단순히 ? 연산자는 속성이나 메서드가 존재하지 않을 수 있음을 나타내며 TypeScript는 null 또는 정의되지 않은 검사를 자동으로 처리합니다.

## 옵셔널 체이닝은 어떻게 작동하나요?

선택적 연결은 액세스하기 전에 속성 액세스 체인의 각 중간 속성 또는 메서드가 존재하는지 확인하여 작동합니다. 중간 값이 null이거나 정의되지 않은 경우 전체 표현식이 정의되지 않은 것으로 평가됩니다.

다음은 옵셔널 체이닝이 어떻게 작동하는지 보여주는 예입니다.

```typescript
interface Person {
  name: string;
  address?: {
    street: string;
    city: string;
  };
}

const person: Person = {
  name: "John Doe",
};

const city = person.address?.city;
console.log(city); // Output: undefined
```

위의 예에서 `street`와 `city`라는 두 개의 중첩된 속성이 있는 선택적 `address` 속성이 있는 `Person` 인터페이스가 있습니다. 그런 다음 `name` 속성만 설정된 `person` 개체를 만듭니다.

다음으로, 선택적 체이닝을 사용하여 `address` 개체의 `city` 속성에 액세스하려고 시도합니다. `address` 속성이 설정되지 않았으므로 `person.address?.city` 표현식은 `undefined`로 평가됩니다.

## TypeScript에서 옵셔널 체이닝 사용하기

TypeScript에서 선택적 연결을 사용하려면 존재하지 않을 수 있는 속성 또는 메서드 뒤에 `?` 연산자를 추가하기만 하면 됩니다. 예를 들면 다음과 같습니다.

```typescript
const street = person.address?.street;
console.log(street); // Output: undefined
```

위의 예에서 선택적 연결을 사용하여 `address` 개체의 `street` 속성에 액세스하려고 합니다. `address` 속성이 설정되지 않았으므로 `person.address?.street` 표현식은 `undefined`로 평가됩니다.

메서드 호출과 함께 선택적 연결을 사용할 수도 있습니다. 예를 들면 다음과 같습니다.

```typescript
interface User {
  name: string;
  getAddress?(): string;
}

const user: User = {
  name: "Jane Doe",
};

const address = user.getAddress?.();
console.log(address); // Output: undefined
```

위의 예에는 문자열을 반환하는 선택적 메소드 `getAddress`가 있는 `User` 인터페이스가 있습니다. 그런 다음 `name` 속성만 설정된 `user` 개체를 만듭니다.

다음으로 선택적 체이닝을 사용하여 `getAddress` 메서드를 호출하려고 합니다. `getAddress` 메서드가 설정되지 않았으므로 `user.getAddress?.()` 표현식은 `undefined`로 평가됩니다.

## 추가 정보

- 선택적 연결은 TypeScript 버전 3.7 이상에서 지원됩니다.
- 옵셔널 체이닝은 JavaScript에서도 지원되지만 이전 브라우저에서는 작동하지 않을 수 있습니다.

## 결론

옵셔널 체이닝은 특히 옵셔널 값을 다룰 때 중첩된 속성과 메소드에 접근하는 것을 단순화하는 TypeScript의 유용한 기능입니다. 옵셔널 체이닝을 사용함으로써 개발자는 오류가 덜 발생하는 보다 깨끗하고 간결한 코드를 작성할 수 있습니다.

## 더 읽을 거리

- [TypeScript 문서: 선택적 연결](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html# optional-chaining)
- [MDN 웹 문서: 선택적 연결](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)