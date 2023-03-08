---
title: 051: TypeScript의 Type-Safe API: API 설계에서 Type Safety를 보장하는 방법
description: 
published: true
date: 2023-03-03T15:32:32.711Z
tags: 
editor: markdown
dateCreated: 2023-03-03T15:32:25.560Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [051: Type-Safe APIs in TypeScript: How to Ensure Type Safety in Your API Design***English** document is available*](/en/Knowledge-base/TypeScript/Learning/051-type-safe-apis-in-typescript-how-to-ensure-type-safety-in-your-api-design)
{.links-list}
TypeScript는 최근 몇 년 동안 특히 코드에서 형식 안전성을 보장하려는 개발자 사이에서 점점 인기를 얻고 있습니다. 이 기사에서는 TypeScript를 사용하여 API 설계에서 유형 안전성을 보장하는 방법을 살펴봅니다.

## Type-Safe API란 무엇입니까?

유형 안전 API는 클라이언트와 서버 간에 전달되는 데이터가 올바른 유형인지 확인하는 API입니다. 이는 API가 지정된 유형을 준수하지 않는 모든 데이터를 거부함을 의미합니다. 이렇게 하면 런타임 오류를 방지하고 디버깅이 훨씬 쉬워집니다.

## 유형 안전성이 중요한 이유는 무엇입니까?

형식 안전성은 오류가 발생하기 전에 오류를 잡는 데 도움이 되므로 중요합니다. 클라이언트와 서버 간에 전달되는 데이터가 올바른 유형인지 확인하면 런타임 오류를 방지하고 코드에 버그가 발생할 가능성을 줄일 수 있습니다. 이렇게 하면 장기적으로 시간과 비용을 절약할 수 있습니다.

## API 디자인에서 유형 안전성을 보장하는 방법

TypeScript를 사용하여 API 설계에서 유형 안전성을 보장하는 방법에는 여러 가지가 있습니다. 이 섹션에서는 가장 일반적인 몇 가지 방법을 살펴보겠습니다.

### 인터페이스를 사용하여 데이터 유형 정의

API 설계에서 유형 안전성을 보장하는 가장 쉬운 방법 중 하나는 인터페이스를 사용하여 데이터 유형을 정의하는 것입니다. 인터페이스는 객체의 모양을 정의하는 TypeScript 구조입니다. 예를 들면 다음과 같습니다.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}
```

이 예에서는 "id", "name" 및 "email"의 세 가지 속성이 있는 "User"라는 인터페이스를 정의했습니다. 이 인터페이스를 사용하여 API로 전달되거나 API에서 전달되는 모든 데이터가 이 모양을 준수하는지 확인할 수 있습니다.

### 열거형을 사용하여 상수 정의

열거형은 API 디자인에서 형식 안전성을 보장하는 데 도움이 되는 또 다른 TypeScript 구조입니다. 열거형은 변수에 할당할 수 있는 명명된 상수 집합입니다. 예를 들면 다음과 같습니다.

```typescript
enum HttpMethod {
  GET,
  POST,
  PUT,
  DELETE,
}
```

이 예제에서는 "GET", "POST", "PUT" 및 "DELETE"라는 4개의 상수가 있는 "HttpMethod"라는 열거형을 정의했습니다. 이 열거형을 사용하여 API에서 사용되는 모든 HTTP 메서드가 이 네 가지 값 중 하나를 준수하는지 확인할 수 있습니다.

### Union 유형을 사용하여 여러 유형 허용

경우에 따라 단일 속성에 대해 여러 유형을 허용해야 할 수 있습니다. 예를 들어 속성은 문자열 또는 숫자일 수 있습니다. 이 경우 공용체 유형을 사용하여 두 유형을 모두 허용할 수 있습니다. 예를 들면 다음과 같습니다.

```typescript
interface User {
  id: number | string;
  name: string;
  email: string;
}
```

이 예에서는 "id" 속성이 숫자 또는 문자열이 되도록 "사용자" 인터페이스를 수정했습니다.

### 제네릭을 사용하여 재사용 가능한 코드 만들기

제네릭은 여러 유형에서 작동하는 재사용 가능한 코드를 생성할 수 있는 TypeScript의 강력한 기능입니다. 예를 들어 문자열과 숫자 모두에서 작동하는 함수가 있을 수 있습니다. 제네릭을 사용하여 함수가 모든 유형에서 작동하는지 확인할 수 있습니다. 예를 들면 다음과 같습니다.

```typescript
function toArray<T>(input: T): T[] {
  return [input];
}
```

이 예제에서는 제네릭 유형 "T"를 사용하고 해당 유형의 배열을 반환하는 "toArray"라는 함수를 정의했습니다. 이 함수는 문자열, 숫자 또는 사용자 정의 유형 등 모든 유형에서 작동합니다.

## 추가 정보

TypeScript에는 유형 보호, 유형 어설션 및 유형 별칭과 같이 API 설계에서 유형 안전성을 보장하는 데 도움이 되는 다른 많은 기능이 있습니다. 자세히 알아보려면 TypeScript 설명서를 읽어보세요.

## 경고

TypeScript는 API 설계에서 유형 안전성을 보장하는 데 도움이 될 수 있지만 묘책이 아니라는 점을 기억하는 것이 중요합니다. 여전히 코드에 버그와 오류가 발생할 수 있으므로 코드를 철저하게 테스트해야 합니다.

## 결론

유형 안전성은 API 설계의 중요한 측면이며 TypeScript는 유형 안전성을 보장하는 데 도움이 되는 많은 기능을 제공합니다. 인터페이스, 열거형, 공용체 유형 및 제네릭을 사용하여 더 강력하고 오류가 덜 발생하는 코드를 만들 수 있습니다.