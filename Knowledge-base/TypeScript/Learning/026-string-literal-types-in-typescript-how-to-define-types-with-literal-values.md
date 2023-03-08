---
title: 026: TypeScript의 문자열 리터럴 유형: 리터럴 값으로 유형을 정의하는 방법
description: 
published: true
date: 2023-03-08T11:32:29.498Z
tags: 
editor: markdown
dateCreated: 2023-03-08T11:32:29.498Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [026: String Literal Types in TypeScript: How to Define Types with Literal Values***English** document is available*](/en/Knowledge-base/TypeScript/Learning/026-string-literal-types-in-typescript-how-to-define-types-with-literal-values)
{.links-list}



TypeScript의 문자열 리터럴 유형: 리터럴 값으로 유형을 정의하는 방법

TypeScript는 정적 타이핑 지원을 추가하는 JavaScript의 확장입니다. 주요 기능 중 하나는 유형을 정의하는 기능입니다. 이 게시물에서는 리터럴 값으로 유형을 정의할 수 있는 TypeScript의 문자열 리터럴 유형을 살펴보겠습니다.

## 문자열 리터럴 유형이란 무엇입니까?

문자열 리터럴 유형은 TypeScript의 유형 리터럴 유형입니다. 유형 리터럴은 런타임에 계산되거나 유추되지 않고 코드에서 직접 정의되는 값을 나타내는 유형입니다.

문자열 리터럴 유형의 경우 값은 문자열 리터럴입니다. 문자열 리터럴은 큰따옴표 또는 작은따옴표를 사용하여 정의되는 문자열입니다. 예를 들면 다음과 같습니다.

```typescript
const myString = "hello";
const myOtherString = 'world';
```

## 문자열 리터럴 유형 정의

문자열 리터럴 유형을 정의하기 위해 `type MyStringLiteral = 'value';` 구문을 사용합니다. 여기서 `MyStringLiteral`은 유형의 이름이고 `value`는 문자열 리터럴 값입니다. 예를 들어:

```typescript
type MyStringLiteral = 'hello';
```

이는 값 `'hello'`만 가질 수 있는 `MyStringLiteral`이라는 유형을 정의합니다.

`|` 연산자를 사용하여 문자열 리터럴 유형의 합집합을 정의할 수도 있습니다. 예를 들어:

```typescript
type MyUnion = 'hello' | 'world';
```

이는 `'hello'` 또는 `'world'` 값을 가질 수 있는 `MyUnion`이라는 유형을 정의합니다.

## 문자열 리터럴 유형 사용

문자열 리터럴 유형을 정의하면 이를 사용하여 변수 및 함수 매개변수의 유형을 정의할 수 있습니다. 예를 들어:

```typescript
const myString: MyStringLiteral = 'hello';

function sayHello(name: MyStringLiteral) {
  console.log(`Hello, ${name}!`);
}
```

이 예제에서는 `MyStringLiteral` 유형의 `myString` 변수와 `MyStringLiteral` 유형의 `name` 매개변수가 있는 `sayHello` 함수를 정의합니다.

문자열 리터럴 유형을 사용하여 함수의 반환 유형을 정의할 수도 있습니다. 예를 들어:

```typescript
function getGreeting(name: MyStringLiteral): string {
  return `Hello, ${name}!`;
}
```

이 예제에서는 `MyStringLiteral` 유형의 `name` 매개변수를 사용하고 문자열을 반환하는 `getGreeting` 함수를 정의합니다.

## 추가 정보

- 속성 및 메소드 유형을 정의하기 위해 인터페이스 및 클래스에서 문자열 리터럴 유형을 사용할 수도 있습니다.
- 문자열 리터럴 유형을 유형 별칭과 함께 사용하여 더 복잡한 유형을 만들 수 있습니다.

## 결론

TypeScript의 문자열 리터럴 유형을 사용하면 리터럴 값으로 유형을 정의할 수 있습니다. 변수 유형, 함수 매개변수 및 반환 유형을 정의하는 데 사용할 수 있습니다. 문자열 리터럴 유형을 사용하면 코드를 보다 표현력 있고 이해하기 쉽게 만들 수 있습니다.

## 외부 리소스

- [TypeScript 핸드북: 문자열 리터럴 유형](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html# string-literal-types)
- [TypeScript 심층 분석: 리터럴 유형](https://basarat.gitbook.io/typescript/type-system/literal-types)