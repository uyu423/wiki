---
title: 044: TypeScript의 부분 유형: 선택적 속성을 사용하여 유형을 만드는 방법
description: 
published: true
date: 2023-03-13T07:32:43.795Z
tags: 
editor: markdown
dateCreated: 2023-03-13T07:32:43.795Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [044: The Partial Type in TypeScript: How to Create Types with Optional Properties***English** document is available*](/en/Knowledge-base/TypeScript/Learning/044-the-partial-type-in-typescript-how-to-create-types-with-optional-properties)
{.links-list}



TypeScript의 부분 유형: 선택적 속성을 사용하여 유형을 만드는 방법

TypeScript는 개발자가 보다 유지 관리 및 확장 가능한 코드를 작성하는 데 도움이 되는 정적 유형 언어입니다. TypeScript의 가장 강력한 기능 중 하나는 사용자 정의 유형을 생성하는 기능입니다. 이 게시물에서는 TypeScript의 Partial 유형에 초점을 맞춰 선택적 속성이 있는 유형을 만들 수 있습니다.

## 부분 유형이란 무엇입니까?

Partial 유형은 기존 유형의 모든 속성이 optional로 설정된 새로운 유형을 생성할 수 있게 해주는 TypeScript의 내장 유틸리티 유형입니다. 즉, 수동으로 각 속성을 optional로 설정하지 않고도 선택적 속성이 있는 유형을 만들 수 있습니다.

다음은 예입니다.

```typescript
interface Person {
  name: string;
  age: number;
  email: string;
}

type PartialPerson = Partial<Person>;

const person: PartialPerson = {
  name: 'John',
  age: 30,
};
```

이 예제에서는 name, age 및 email의 세 가지 속성을 사용하여 Person이라는 인터페이스를 정의합니다. 그런 다음 Partial 유틸리티 유형을 사용하여 PartialPerson이라는 새 유형을 만듭니다. 이 유형에는 선택 사항으로 설정된 Person의 모든 속성이 있습니다.

그런 다음 name 및 age 속성만 설정된 person이라는 PartialPerson 유형의 새 개체를 만들 수 있습니다. 이메일 속성은 부분 유형에 의해 선택 사항으로 설정되었기 때문에 선택 사항입니다.

## 부분 유형 사용 방법

Partial 유형을 사용하려면 Partial 유틸리티 유형에 부분적으로 만들려는 유형을 전달하기만 하면 됩니다. 다음은 예입니다.

```typescript
interface Product {
  name: string;
  price: number;
  description: string;
  image?: string;
}

type PartialProduct = Partial<Product>;

const product: PartialProduct = {
  name: 'iPhone',
  price: 999,
};
```

이 예제에서는 이름, 가격, 설명 및 이미지의 네 가지 속성을 사용하여 Product라는 인터페이스를 정의합니다. 이미지 속성은 이름 뒤에 물음표(?)가 있기 때문에 선택 사항입니다.

그런 다음 Partial 유틸리티 유형을 사용하여 PartialProduct라는 새 유형을 만듭니다. 이 유형에는 Product의 모든 속성이 optional로 설정되어 있습니다.

그런 다음 이름 및 가격 속성만 설정된 제품이라는 PartialProduct 유형의 새 개체를 만들 수 있습니다. 설명 및 이미지 속성은 부분 유형에 의해 선택 사항으로 설정되었기 때문에 선택 사항입니다.

## 추가 정보

부분 유형은 속성을 옵션으로만 설정한다는 점에 유의해야 합니다. 유형에서 특성을 제거하지 않습니다. 유형에서 속성을 제거하려면 해당 속성을 포함하지 않는 새 유형을 만들어야 합니다.

## 결론

TypeScript의 부분 유형은 선택적 속성이 있는 유형을 만들 수 있는 강력한 유틸리티 유형입니다. 이는 모든 속성이 정의되지 않은 개체로 작업하거나 수동으로 각 속성을 optional로 설정하지 않고 선택적 속성이 있는 유형을 생성하려는 경우에 유용할 수 있습니다.

Partial 유형을 사용하면 TypeScript에서 더 유지 관리 및 확장 가능한 코드를 작성할 수 있습니다.

## 외부 리소스

- [TypeScript 핸드북: 유틸리티 유형](https://www.typescriptlang.org/docs/handbook/utility-types.html# partialtype)
- [TypeScript 심층 분석: 유틸리티 유형](https://basarat.gitbook.io/typescript/type-system/utility-types# partial)