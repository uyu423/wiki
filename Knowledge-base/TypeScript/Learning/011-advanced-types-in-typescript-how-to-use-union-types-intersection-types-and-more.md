---
title: 011: TypeScript의 고급 유형: 공용체 유형, 교차 유형 등을 사용하는 방법
description: 
published: true
date: 2023-03-06T14:33:15.021Z
tags: 
editor: markdown
dateCreated: 2023-03-06T14:33:07.657Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [011: Advanced Types in TypeScript: How to Use Union Types, Intersection Types, and More***English** document is available*](/en/Knowledge-base/TypeScript/Learning/011-advanced-types-in-typescript-how-to-use-union-types-intersection-types-and-more)
{.links-list}



TypeScript의 고급 유형: 공용체 유형, 교차 유형 등을 사용하는 방법

TypeScript는 정적 타이핑 및 기타 기능을 제공하여 대규모 애플리케이션을 더 쉽게 작성하고 유지 관리할 수 있는 JavaScript의 상위 집합입니다. TypeScript의 가장 강력한 기능 중 하나는 공용체 유형, 교차 유형 등을 포함한 고급 유형에 대한 지원입니다. 이 게시물에서는 이러한 고급 유형과 이를 TypeScript 코드에서 효과적으로 사용하는 방법을 살펴보겠습니다.

## 조합 유형

TypeScript에서 공용체 유형을 사용하면 변수가 둘 이상의 유형을 가질 수 있습니다. 예를 들어 문자열 또는 숫자일 수 있는 변수가 있을 수 있습니다.

```typescript
let myVar: string | number;
```

이는 `myVar`에 `string` 유형 또는 `number` 유형의 값을 할당할 수 있음을 의미합니다. 공용체 유형을 사용하여 더 넓은 범위의 값을 처리할 수 있는 보다 유연하고 표현적인 유형을 만들 수 있습니다.

### 함수 매개변수에 공용체 유형 사용

공용체 유형의 일반적인 사용 사례 중 하나는 유연한 함수 매개변수를 만드는 것입니다. 예를 들어 문자열이나 숫자를 받을 수 있는 함수가 있을 수 있습니다.

```typescript
function myFunc(myParam: string | number) {
  // ...
}
```

이렇게 하면 문자열 또는 숫자 인수를 사용하여 `myFunc`를 호출할 수 있습니다.

```typescript
myFunc("hello");
myFunc(42);
```

### 반환 유형에 유니온 유형 사용

함수 반환 유형에 공용체 유형을 사용할 수도 있습니다. 예를 들어 문자열이나 숫자를 반환하는 함수가 있을 수 있습니다.

```typescript
function myOtherFunc(): string | number {
  // ...
}
```

이는 `myOtherFunc`의 반환 값이 문자열 또는 숫자일 수 있음을 의미합니다. 이를 사용하여 입력에 따라 다른 유형의 값을 반환할 수 있는 보다 유연한 함수를 만들 수 있습니다.

### 추가 정보

공용체 유형을 사용할 때 유형 검사에 주의하는 것이 중요합니다. 런타임 오류를 방지하려면 변수를 사용하기 전에 항상 변수 유형을 확인해야 합니다. 예를 들어:

```typescript
if (typeof myVar === "string") {
  // ...
} else if (typeof myVar === "number") {
  // ...
}
```

## 교차로 유형

TypeScript에서 교차 유형을 사용하면 변수가 한 번에 여러 유형을 가질 수 있습니다. 예를 들어 문자열이면서 객체인 변수가 있을 수 있습니다.

```typescript
let myVar: string & object;
```

즉, `myVar`는 문자열인 동시에 객체여야 합니다. 교차 유형을 사용하여 복잡한 데이터 구조를 처리할 수 있는 보다 정확하고 구체적인 유형을 만들 수 있습니다.

### 함수 매개변수에 대한 교차 유형 사용

교차 유형의 일반적인 사용 사례 중 하나는 보다 구체적인 함수 매개변수를 만드는 것입니다. 예를 들어, `name` 속성(문자열)과 `age` 속성(숫자)이 모두 있는 객체를 허용하는 함수가 있을 수 있습니다.

```typescript
function myFunc(myParam: { name: string } & { age: number }) {
  // ...
}
```

즉, `myParam`은 `name` 속성(`string` 유형 값 포함)과 `age` 속성(`number` 유형 값 포함)을 모두 가진 객체여야 합니다. 이를 사용하여 특정 유형의 입력만 허용하는 보다 정확한 함수 매개변수를 생성할 수 있습니다.

### 객체 유형에 대한 교차 유형 사용

교차 유형을 사용하여 더 구체적인 개체 유형을 만들 수도 있습니다. 예를 들어 이름과 나이가 있는 사람을 나타내는 개체 유형이 있을 수 있습니다.

```typescript
type Person = {
  name: string;
  age: number;
};
```

그런 다음 `grade` 및 `school`과 같은 추가 속성을 사용하여 학생을 나타내는 보다 구체적인 개체 유형을 만들 수 있습니다.

```typescript
type Student = Person & {
  grade: number;
  school: string;
};
```

이것은 `Student` 객체가 `Person` 객체의 모든 속성(`string` 유형의 값을 가진 `name` 속성과 `number` 유형의 값을 가진 `age` 속성)을 가져야 함을 의미합니다. 추가 속성 `grade`(숫자) 및 `school`(문자열).

### 추가 정보

교차 유형을 사용할 때 유형 호환성에 주의하는 것이 중요합니다. 결합하려는 유형이 서로 호환되는 경우에만 교차 유형을 사용해야 합니다. 예를 들어 `문자열`과 `숫자`는 호환되는 유형이 아니기 때문에 교차 유형을 만들 수 없습니다.

## 타입 가드

공용체 유형을 사용하는 경우 변수를 사용하기 전에 유형을 확인해야 하는 경우가 많습니다. TypeScript는 이를 쉽게 해주는 유형 가드라는 기능을 제공합니다.

유형 가드는 변수를 받아 변수가 특정 유형인지 여부를 나타내는 부울 값을 반환하는 함수입니다. 예를 들어 변수가 문자열인지 확인하는 유형 보호가 있을 수 있습니다.

```typescript
function isString(myVar: any): myVar is string {
  return typeof myVar === "string";
}
```

이 유형 가드는 `any` 유형(모든 유형일 수 있음)의 `myVar` 변수를 사용하고 `myVar`가 문자열인지 여부를 나타내는 부울 값을 반환합니다. `myVar is string` 구문은 TypeScript에 함수가 `true`를 반환하면 변수가 `string` 유형임을 알려주는 유형 조건자입니다.

그런 다음 이 유형 보호를 사용하여 변수를 사용하기 전에 유형을 확인할 수 있습니다.

```typescript
if (isString(myVar)) {
  // myVar is now of type `string`
  console.log(myVar.toUpperCase());
}
```

### 추가 정보

유형 가드는 공용체 유형뿐만 아니라 모든 유형과 함께 사용할 수 있습니다. TypeScript 코드에서 유형 안전성을 보장하는 강력한 도구입니다.

## 조건부 유형

TypeScript에서 조건부 유형을 사용하면 조건에 따라 유형을 정의할 수 있습니다. 예를 들어 18세 이상인 사람을 나타내는 유형과 18세 미만인 경우 다른 유형이 있을 수 있습니다.

```typescript
type Person<T> = T extends { age: number; } & { age: infer U; } ? (
  U extends 18 ? { name: string; age: U; } : { name: string; age: U; id: string; }
) : never;
```

이 유형 정의는 `extends` 키워드를 사용하여 조건을 정의합니다. `T` 유형에 `number` 유형의 `age` 속성이 있는 경우 조건 유형은 `U` 값에 따라 다른 유형을 반환합니다(추론된 '연령' 유형). `U`가 18이면 유형은 `{ name: string; 나이: U; }`이고 `U`가 18이 아닌 경우 유형은 `{ name: string; 나이: U; 아이디: 문자열; }`.

### 추가 정보

조건부 유형은 복잡하고 읽기 어려울 수 있습니다. 조건에 의존하는 유형을 생성하는 강력한 도구이지만, 드물게 주의해서 사용해야 합니다.

## 결론

공용체 유형, 교차 유형 및 조건부 유형과 같은 고급 유형은 TypeScript 코드를 보다 유연하고 표현력 있게 만들 수 있습니다. 이러한 형식을 효과적으로 사용하면 복잡한 데이터 구조를 처리하고 코드에서 형식 안전성을 보장할 수 있는 보다 정확하고 구체적인 형식을 만들 수 있습니다. 즐거운 코딩하세요!

## 외부 리소스

- [TypeScript 핸드북: 고급 유형](https://www.typescriptlang.org/docs/handbook/advanced-types.html)
- [TypeScript 심층 분석: 공용체 유형](https://basarat.gitbook.io/typescript/type-system/union-types)
- [TypeScript 심층 분석: 교차 유형](https://basarat.gitbook.io/typescript/type-system/intersection-types)
- [TypeScript 심층 분석: Type Guards](https://basarat.gitbook.io/typescript/type-system/typeguard)
- [TypeScript 심층 분석: 조건부 유형](https://basarat.gitbook.io/typescript/type-system/conditional-types)