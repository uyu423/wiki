---
title: 054: TypeScript의 유형 기반 테스트: 유형을 사용하여 테스트 전략을 개선하는 방법
description: 
published: true
date: 2023-03-06T19:32:50.358Z
tags: 
editor: markdown
dateCreated: 2023-03-06T19:32:50.358Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [054: Type-Driven Testing in TypeScript: How to Use Types to Improve Your Testing Strategy***English** document is available*](/en/Knowledge-base/TypeScript/Learning/054-type-driven-testing-in-typescript-how-to-use-types-to-improve-your-testing-strategy)
{.links-list}



TypeScript의 유형 기반 테스트: 유형을 사용하여 테스트 전략을 개선하는 방법

TypeScript는 개발자가 개발 프로세스 초기에 오류를 포착할 수 있도록 정적 타이핑을 제공하는 강력한 언어입니다. 그러나 TypeScript를 사용하여 테스트 전략을 개선할 수도 있다는 사실을 알고 계셨습니까? 이 게시물에서는 유형을 사용하여 테스트 노력을 촉진하여 보다 강력하고 안정적인 코드를 생성하는 방법을 살펴보겠습니다.

## 유형 기반 테스트란 무엇입니까?

유형 기반 테스트는 유형을 사용하여 코드의 예상 동작을 정의하는 테스트 접근 방식입니다. TypeScript의 유형 시스템을 활용하면 프로덕션에 적용되기 전에 오류를 포착하는 보다 정확하고 표현력이 풍부한 테스트를 만들 수 있습니다.

기존의 테스트 접근 방식은 코드가 어떻게 작동해야 하는지에 대한 가정을 기반으로 수동으로 테스트 사례를 만드는 방식에 의존합니다. Type-Driven Testing을 사용하면 TypeScript의 유형 시스템을 사용하여 코드의 예상 동작을 정의할 수 있습니다. 즉, 테스트가 코드로 항상 최신 상태를 유지하고 개발 프로세스 초기에 오류를 포착할 수 있습니다.

## TypeScript에서 유형 기반 테스트를 사용하는 방법

Type-Driven Testing의 핵심은 TypeScript의 유형 시스템을 사용하여 코드의 예상 동작을 정의하는 것입니다. 예를 들어 보겠습니다.

두 개의 숫자를 더하는 함수가 있다고 가정합니다.

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

이 기능을 테스트하기 위해 다음과 같은 테스트 사례를 작성할 수 있습니다.

```typescript
test('add function should return the sum of two numbers', () => {
  expect(add(2, 2)).toBe(4);
});
```

이 테스트 사례는 간단하고 간단하지만 제한적이기도 합니다. 2 + 2를 더하는 하나의 특정 사례만 테스트합니다. 음수, 소수 또는 문자열을 전달하면 어떻게 됩니까? 이러한 모든 시나리오를 다루려면 추가 테스트 사례를 작성해야 합니다.

Type-Driven Testing을 사용하면 TypeScript의 유형 시스템을 사용하여 `add` 함수의 예상 동작을 정의할 수 있습니다. 방법은 다음과 같습니다.

```typescript
type Add = (a: number, b: number) => number;

const add: Add = (a, b) => {
  return a + b;
};
```

이 예에서는 `add` 함수의 예상 동작을 설명하는 `Add`라는 `유형`을 정의했습니다. '추가' 유형은 두 개의 '숫자' 인수를 받아 '숫자'를 반환하는 함수입니다. 또한 `add` 함수를 `Add` 유형으로 정의했습니다.

이제 테스트 케이스를 작성할 때 `Add` 유형을 사용하여 테스트 케이스를 생성할 수 있습니다.

```typescript
type AddTestCases = [
  [a: number, b: number, expected: number],
  [a: number, b: number, expected: number],
  [a: number, b: number, expected: number]
];

const addTestCases: AddTestCases = [
  [2, 2, 4],
  [-2, 2, 0],
  [0.1, 0.2, 0.3]
];

test.each(addTestCases)(
  'add function should return the sum of %p and %p',
  (a, b, expected) => {
    expect(add(a, b)).toBe(expected);
  }
);
```

이 테스트 케이스에서는 `addTestCases`라는 테스트 케이스 배열을 정의했습니다. 각 테스트 케이스는 `a`, `b` 및 `expected`의 세 값 배열입니다. 또한 `addTestCases` 배열의 구조를 설명하는 `AddTestCases`라는 `유형`도 정의했습니다.

마지막으로 Jest 테스트 라이브러리의 `test.each` 함수를 사용하여 `addTestCases` 배열의 각 항목에 대한 테스트 케이스를 생성합니다. 테스트 사례 문자열의 `%p` 자리 표시자는 테스트 사례 배열의 해당 값으로 대체됩니다.

이 접근 방식으로 TypeScript의 유형 시스템을 사용하여 `add` 함수의 예상 동작을 정의했습니다. 또한 수동으로 각 시나리오를 작성할 필요 없이 다양한 시나리오를 다루는 여러 테스트 사례를 생성했습니다.

## 유형 기반 테스트의 이점

TypeScript에서 Type-Driven Testing을 사용하면 다음과 같은 몇 가지 이점이 있습니다.

- **더 정확하고 표현력이 풍부한 테스트:** TypeScript의 유형 시스템을 사용하여 코드의 예상 동작을 정의하면 테스트가 더 정확하고 표현력이 높아집니다. 즉, 테스트에서 엣지 케이스나 예기치 않은 동작을 놓칠 가능성이 적습니다.
- **작성할 테스트 사례 감소:** Type-Driven Testing을 사용하면 정의한 유형을 기반으로 테스트 사례를 자동으로 생성할 수 있습니다. 즉, 더 적은 수의 테스트 사례를 작성해야 하므로 시간과 노력을 절약할 수 있습니다.
- **초기 오류 감지:** 개발 프로세스 초기에 오류를 포착하여 버그 수정에 드는 시간과 비용을 줄일 수 있습니다. Type-Driven Testing을 사용하면 오류가 프로덕션에 적용되기 전에 오류를 포착하여 보다 안정적이고 강력한 코드를 생성할 수 있습니다.

## 추가 정보

- Type-Driven Testing은 기존의 테스트 접근 방식을 대체하지 않습니다. 오히려 오류를 더 빠르고 안정적으로 파악하는 데 도움이 되는 보완적인 접근 방식입니다.
- TypeScript의 유형 시스템은 강력하지만 완벽하지는 않습니다. 에지 케이스와 예상치 못한 동작을 다루기 위해 추가 테스트 케이스를 작성하는 것은 여전히 중요합니다.

## 결론

Type-Driven Testing은 TypeScript의 유형 시스템을 활용하여 코드의 예상 동작을 정의하는 강력한 테스트 접근 방식입니다. 유형을 사용하여 테스트 노력을 주도하면 개발 프로세스 초기에 오류를 포착하는 보다 정확하고 표현력이 풍부한 테스트를 만들 수 있습니다. Type-Driven Testing을 사용하면 더 적은 수의 테스트 사례를 작성하고 오류를 조기에 발견하여 더 안정적이고 강력한 코드를 생성할 수 있습니다.

## 추가 리소스

- [TypeScript를 이용한 Type-Driven Development](https://www.typescriptlang.org/docs/handbook/type-driven-development.html)
- [Jest로 TypeScript 테스트하기](https://jestjs.io/docs/en/getting-started# using-typescript)
- [Haskell의 유형 기반 테스팅](https://www.fpcomplete.com/blog/type-driven-testing-in-haskell/)