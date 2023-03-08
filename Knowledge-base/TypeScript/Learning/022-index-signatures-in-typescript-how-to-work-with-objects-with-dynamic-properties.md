---
title: 022: TypeScript의 인덱스 서명: 동적 속성이 있는 개체로 작업하는 방법
description: 
published: true
date: 2023-03-04T16:32:41.776Z
tags: 
editor: markdown
dateCreated: 2023-03-04T16:32:34.638Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [022: Index Signatures in TypeScript: How to Work with Objects with Dynamic Properties***English** document is available*](/en/Knowledge-base/TypeScript/Learning/022-index-signatures-in-typescript-how-to-work-with-objects-with-dynamic-properties)
{.links-list}


TypeScript에서 개체로 작업하는 것은 개발자의 일반적인 작업입니다. 그러나 때로는 개체의 속성을 미리 알 수 없거나 동적으로 변경될 수 있습니다. 이것은 TypeScript의 인덱스 서명이 유용한 곳입니다. 이 게시물에서는 인덱스 서명에 대해 알아보고 동적 속성이 있는 개체를 사용하는 방법을 알아봅니다.

## 인덱스 서명이란 무엇입니까?

인덱스 서명은 컴파일 시간에 알려지지 않은 속성 유형을 정의할 수 있는 TypeScript 기능입니다. 이를 통해 사전 정의되지 않고 런타임에 결정되는 속성 집합으로 개체를 정의할 수 있습니다.

색인 서명은 대괄호 '[]'와 유형 주석을 사용하여 정의됩니다. 예를 들어 색인 서명이 있는 객체를 정의해 보겠습니다.

```typescript
interface MyObject {
  [key: string]: any;
}
```

위의 코드에서 색인 서명 `[key: string]: any;`을 사용하여 `MyObject` 인터페이스를 정의했습니다. 이는 문자열 키가 있는 모든 속성을 객체에 추가할 수 있고 해당 값이 모든 유형일 수 있음을 의미합니다.

## 색인 서명 사용

인덱스 서명이 무엇인지 알았으니 이제 TypeScript에서 인덱스 서명을 어떻게 사용할 수 있는지 살펴보겠습니다. 다음 예를 고려하십시오.

```typescript
interface MyObject {
  [key: string]: string;
}

const obj: MyObject = {
  name: 'John',
  age: '30',
  address: '123 Main St.',
};
```

위의 코드에서 색인 서명 `[key: string]: string;`을 사용하여 `MyObject` 인터페이스를 정의했습니다. 즉, 문자열 키가 있는 모든 속성을 개체에 추가할 수 있지만 해당 값은 문자열 유형이어야 합니다.

또한 `name`, `age` 및 `address`의 세 가지 속성이 있는 개체 `obj`를 정의했습니다. 속성이 인터페이스에 정의되지 않은 경우에도 오류가 발생하지 않습니다. 이는 문자열 키로 속성을 추가할 수 있는 인덱스 서명 때문입니다.

## 추가 정보

인덱스 서명은 주의해서 사용해야 한다는 점에 유의하는 것이 중요합니다. 특정 상황에서 유용할 수 있지만 유형 안전을 유지하기 어렵게 만들 수도 있습니다. 필요할 때만 사용하는 것이 좋습니다.

## 중첩 개체 작업

색인 서명은 중첩 개체와 함께 사용할 수도 있습니다. 다음 예를 고려하십시오.

```typescript
interface MyObject {
  [key: string]: {
    name: string;
    age: number;
  };
}

const obj: MyObject = {
  john: {
    name: 'John',
    age: 30,
  },
  jane: {
    name: 'Jane',
    age: 25,
  },
};
```

위의 코드에서 색인 서명 `[key: string]: { name: string; 연령: 숫자 }`. 즉, 문자열 키가 있는 모든 속성을 개체에 추가할 수 있으며 해당 값은 문자열 유형의 '이름'과 숫자 유형의 '나이'를 가진 개체여야 합니다.

또한 `john`과 `jane`의 두 가지 속성을 가진 객체 `obj`도 정의했습니다. 이러한 각 속성은 `name` 및 `age` 속성이 있는 개체입니다. 속성이 인터페이스에 정의되지 않은 경우에도 오류가 발생하지 않습니다. 이는 문자열 키와 중첩 개체로 속성을 추가할 수 있는 인덱스 서명 때문입니다.

## 경고

중첩 개체와 함께 인덱스 서명을 사용할 때 존재하지 않을 수 있는 속성에 액세스하지 않도록 주의해야 합니다. 예를 들어 다음 코드를 고려하십시오.

```typescript
interface MyObject {
  [key: string]: {
    name: string;
    age: number;
  };
}

const obj: MyObject = {
  john: {
    name: 'John',
    age: 30,
  },
  jane: {
    name: 'Jane',
    age: 25,
  },
};

const person = obj['jim'];
console.log(person.name);
```

위의 코드에서 우리는 존재하지 않는 사람의 `name` 속성에 액세스하려고 합니다. 이로 인해 런타임 오류가 발생합니다. 이를 방지하려면 속성에 액세스하기 전에 속성이 존재하는지 확인해야 합니다.

## 결론

인덱스 서명은 TypeScript의 강력한 기능으로 동적 속성이 있는 개체로 작업할 수 있습니다. 컴파일 타임에 알려지지 않은 속성을 가진 개체를 정의하는 데 사용할 수 있으며 중첩된 개체에도 사용할 수 있습니다. 그러나 주의해서 사용하고 잠재적인 위험을 인식하는 것이 중요합니다.

## 더 읽을 거리

- [TypeScript 문서: 인덱싱 가능한 유형](https://www.typescriptlang.org/docs/handbook/interfaces.html# indexable-types)
- [TypeScript 심층 분석: 인덱스 서명](https://basarat.gitbook.io/typescript/type-system/index-signatures)