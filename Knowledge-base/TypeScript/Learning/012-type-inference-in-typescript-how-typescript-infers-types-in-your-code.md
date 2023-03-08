---
title: 012: TypeScript에서 유형 추론: TypeScript가 코드에서 유형을 추론하는 방법
description: 
published: true
date: 2023-03-04T06:32:31.063Z
tags: 
editor: markdown
dateCreated: 2023-03-04T06:32:29.701Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [012: Type Inference in TypeScript: How TypeScript Infers Types in Your Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/012-type-inference-in-typescript-how-typescript-infers-types-in-your-code)
{.links-list}


유형 유추는 컴파일러가 코드에서 변수 및 표현식의 유형을 자동으로 유추할 수 있도록 하는 TypeScript의 강력한 기능입니다. 이 기능을 사용하면 모든 변수 또는 함수 매개변수에 대한 유형을 수동으로 지정할 필요가 없으므로 코드를 작성하고 유지 관리하기가 더 쉽습니다.

이 게시물에서는 TypeScript에서 유형 추론이 작동하는 방식과 자신의 코드에서 이를 활용할 수 있는 방법을 자세히 살펴보겠습니다.

## 유형 추론이란 무엇입니까?

유형 유추는 코드에서의 사용을 기반으로 변수 또는 식의 유형을 결정하는 프로세스입니다. 즉, TypeScript는 변수나 표현식을 사용하는 방식을 보고 자동으로 해당 유형을 결정할 수 있습니다.

예를 들어 문자열로 초기화된 `name` 변수가 있다고 가정해 보겠습니다.

```typescript
let name = "John";
```

TypeScript는 문자열 값으로 초기화되고 있다는 사실을 기반으로 `name`의 유형이 `string`임을 유추할 수 있습니다.

마찬가지로 'age' 매개변수를 사용하고 나이가 18세 이상인지 여부에 따라 부울을 반환하는 함수가 있는 경우:

```typescript
function isAdult(age: number) {
  return age > 18;
}
```

TypeScript는 비교 작업에 사용되고 있다는 사실을 기반으로 `age` 유형이 `number`임을 추론할 수 있습니다.

## 유형 추론은 어떻게 작동합니까?

TypeScript는 "컨텍스트 타이핑"이라는 프로세스를 사용하여 코드에서 유형을 추론합니다. 이는 변수 또는 식의 유형이 사용되는 컨텍스트를 기반으로 유추됨을 의미합니다.

예를 들어 `person` 매개변수를 사용하여 이름을 반환하는 함수가 있다고 가정해 보겠습니다.

```typescript
function getName(person: { name: string }) {
  return person.name;
}
```

이 경우 TypeScript는 `person` 유형이 `string` 유형의 `name` 속성을 가진 객체라고 추론할 수 있습니다. 이것은 함수가 `name` 속성을 가진 객체를 예상하고 있고 return 문에서 `name` 속성을 사용하고 있기 때문입니다.

## 제네릭을 사용한 타입 추론

유형 유추는 TypeScript의 제네릭에서도 작동합니다. 제네릭을 사용하면 정확한 유형을 미리 알지 않고도 다양한 유형으로 작동할 수 있는 코드를 작성할 수 있습니다.

예를 들어 값의 배열을 받아 첫 번째 값을 반환하는 함수가 있다고 가정해 보겠습니다.

```typescript
function getFirst<T>(arr: T[]): T {
  return arr[0];
}
```

이 경우 함수 서명의 'T'는 모든 유형이 될 수 있는 일반 유형을 나타냅니다. TypeScript는 전달된 배열의 유형을 기반으로 `T` 유형을 유추할 수 있습니다.

예를 들어 문자열 배열로 함수를 호출하는 경우:

```typescript
const first = getFirst(["hello", "world"]);
```

TypeScript는 `getFirst`에 전달된 배열이 문자열 배열이라는 사실을 기반으로 `first`의 유형이 `string`이라고 추론할 수 있습니다.

## 타입 추론의 한계

유형 유추는 작성해야 하는 코드의 양을 줄이는 데 매우 유용할 수 있지만 TypeScript가 유형을 올바르게 유추하는 것이 항상 가능한 것은 아니라는 점에 유의해야 합니다.

경우에 따라 변수 또는 표현식의 유형이 모호하거나 유추할 수 있는 가능한 유형이 여러 개 있을 수 있습니다. 이러한 경우 유형 주석을 사용하여 수동으로 유형을 지정해야 할 수 있습니다.

예를 들어 숫자 문자열로 초기화된 `age` 변수가 있다고 가정해 보겠습니다.

```typescript
let age = "20";
```

이 경우 TypeScript는 `age` 유형을 숫자로 의도했음에도 불구하고 `string`으로 유추할 수 있습니다. 이 문제를 해결하려면 유형 주석을 사용하여 수동으로 유형을 지정할 수 있습니다.

```typescript
let age: number = parseInt("20");
```

## 결론

유형 유추는 컴파일러가 코드에서 변수 및 표현식의 유형을 자동으로 유추할 수 있도록 하는 TypeScript의 강력한 기능입니다. 유형 추론이 작동하는 방식을 이해하면 더 간결하고 유지 관리 가능한 코드를 작성할 수 있습니다.

유형 추론이 항상 완벽하지는 않지만 코드를 작성하고 유지 관리하는 데 많은 시간과 노력을 절약할 수 있습니다. TypeScript에 더 익숙해지면 언제 유형 추론에 의존하고 언제 유형 주석을 사용해야 하는지 더 잘 이해할 수 있습니다.

## 추가 정보

- TypeScript 핸드북: [Type Inference](https://www.typescriptlang.org/docs/handbook/type-inference.html)
- TypeScript 심층 분석: [유형 추론](https://basarat.gitbook.io/typescript/type-system/type-inference)
- TypeScript 공식 문서: [Type Inference](https://www.typescriptlang.org/docs/handbook/type-inference.html)

## 경고

- 유형 추론에만 의존할 때는 항상 100% 정확하지 않으므로 주의하십시오.
- 변수 또는 표현식의 유형이 확실하지 않은 경우 유형 주석을 사용하여 유형을 지정하는 것이 좋습니다.

## 위험

- 유형 추론을 잘못 사용하면 코드에서 버그 및 예기치 않은 동작이 발생할 수 있습니다. 항상 코드를 철저하게 테스트하여 예상대로 작동하는지 확인하십시오.