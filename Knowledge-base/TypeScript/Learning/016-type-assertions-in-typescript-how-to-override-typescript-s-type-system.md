---
title: 016: TypeScript의 유형 어설션: TypeScript의 유형 시스템을 재정의하는 방법
description: 
published: true
date: 2023-03-02T11:32:22.593Z
tags: 
editor: markdown
dateCreated: 2023-03-02T11:32:15.430Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [016: Type Assertions in TypeScript: How to Override TypeScript's Type System***English** document is available*](/en/Knowledge-base/TypeScript/Learning/016-type-assertions-in-typescript-how-to-override-typescript-s-type-system)
{.links-list}


TypeScript는 선택적 정적 타이핑을 제공하고 개발자가 더 안전하고 유지 관리하기 쉬운 코드를 작성할 수 있도록 하는 JavaScript의 상위 집합입니다. TypeScript의 주요 기능 중 하나는 컴파일 타임에 오류를 포착하고 코드 품질을 향상시키는 유형 시스템입니다. 그러나 특정 기능을 달성하기 위해 TypeScript의 유형 시스템을 재정의해야 하는 상황이 있을 수 있으며 여기서 유형 어설션이 필요합니다.

이 게시물에서는 TypeScript의 유형 어설션을 살펴보고 이를 사용하여 TypeScript의 유형 시스템을 재정의하는 방법을 배웁니다. 다음 주제를 다룰 것입니다.

- 유형 어설션이란 무엇입니까?
- TypeScript에서 타입 어설션을 사용하는 방법
- 타입 어설션 사용 예시
- 추가 정보

## 타입 어서션이 무엇인가요?

TypeScript의 유형 어설션은 값 유형에 대해 실제보다 더 많이 알고 있음을 컴파일러에 알리는 방법입니다. TypeScript의 유형 검사기가 동의하지 않더라도 유형 시스템을 재정의하고 TypeScript에 값을 다른 유형으로 처리하도록 지시하는 방법입니다.

유형 어설션은 유형 캐스팅이 아닙니다. 유형 캐스팅은 한 유형의 값을 다른 유형으로 변환하는 방법인 반면, 유형 어설션은 값을 변경하지 않고 값을 다른 유형으로 취급하도록 TypeScript에 지시할 뿐입니다.

유형 어설션은 특정 유형의 값을 알고 있지만 TypeScript는 그렇지 않은 경우에 유용합니다. 유형 때문에 TypeScript가 허용하지 않는 방식으로 값을 사용하려는 경우에도 유용합니다.

## TypeScript에서 타입 어설션을 사용하는 방법

TypeScript는 꺾쇠 괄호 구문과 as 구문의 두 가지 유형 어설션 구문을 제공합니다.

### 꺾쇠괄호 구문

꺾쇠 괄호 구문은 TypeScript의 유형 어설션에 대한 원래 구문입니다. 다음과 같습니다.

```typescript
let value: any = "hello world";
let length: number = (<string>value).length;
```

이 예제에서는 `any` 유형의 `value` 변수를 선언하고 `"hello world"` 값을 할당합니다. 그런 다음 꺽쇠 괄호 구문을 사용하여 `value`가 문자열임을 확인하고 길이를 변수 `length`에 할당합니다.

### 구문으로

as 구문은 TypeScript의 유형 어설션을 위한 최신 구문입니다. 다음과 같습니다.

```typescript
let value: any = "hello world";
let length: number = (value as string).length;
```

이 예제에서는 as 구문을 사용하여 `value`가 문자열임을 확인하고 길이를 변수 `length`에 할당합니다.

두 구문은 동일하며 서로 교환하여 사용할 수 있습니다. 그러나 as 구문은 JSX 구문과 충돌할 가능성이 적기 때문에 TypeScript 팀에서 권장합니다.

## 타입 어설션 사용 예시

TypeScript에서 유형 어설션을 사용하는 몇 가지 예를 살펴보겠습니다.

### 예제 1: 값의 유형 어설션

```typescript
let value: any = "hello world";
let length: number = (value as string).length;
```

이 예제에서는 `value`가 문자열임을 확인하고 길이를 변수 `length`에 할당합니다.

### 예제 2: 개체 속성의 유형 어설션

```typescript
interface Person {
    name: string;
    age: number;
}

let person: any = { name: "John", age: 30 };
let nameLength: number = (person as Person).name.length;
```

이 예제에서는 `name` 및 `age` 속성이 있는 `Person` 인터페이스를 선언합니다. 그런 다음 `any` 유형의 `person` 변수를 선언하고 `Person`과 동일한 속성을 가진 개체를 할당합니다. as 구문을 사용하여 `person`이 `Person` 유형임을 확인하고 `name` 속성의 길이를 `nameLength` 변수에 할당합니다.

### 예제 3: 함수 반환 값의 유형 어설션

```typescript
function getLength(value: any): number {
    return (value as string).length;
}

let length: number = getLength("hello world");
```

이 예제에서는 'any' 유형의 값을 사용하고 해당 길이를 숫자로 반환하는 함수 'getLength'를 선언합니다. as 구문을 사용하여 값이 문자열임을 확인하고 길이를 반환합니다. 그런 다음 `"hello world"` 값으로 함수를 호출하고 반환 값을 `length` 변수에 할당합니다.

## 추가 정보

어설션된 유형이 잘못된 경우 런타임 오류가 발생할 수 있으므로 유형 어설션은 주의해서 사용해야 합니다. 컴파일 타임에 오류를 포착하기 위해 가능할 때마다 TypeScript의 유형 시스템을 사용하는 것이 항상 좋습니다.

형식 어설션은 코드를 읽고 유지 관리하기 어렵게 만들 수 있으므로 드물게 사용해야 합니다. 유형 어설션을 자주 사용하는 경우 코드를 리팩토링해야 한다는 신호일 수 있습니다.

## 결론

TypeScript의 유형 어설션은 개발자가 필요할 때 TypeScript의 유형 시스템을 재정의할 수 있는 강력한 도구입니다. 특정 문제를 해결하는 데 사용할 수 있지만 신중하고 드물게 사용해야 합니다. 유형 어설션을 올바르게 사용하면 TypeScript에서 더 안전하고 유지 관리하기 쉬운 코드를 작성할 수 있습니다.

## 더 읽을거리

- [TypeScript 핸드북: 유형 어설션](https://www.typescriptlang.org/docs/handbook/basic-types.html# type-assertions)
- [TypeScript 심층 분석: 유형 어설션](https://basarat.gitbook.io/typescript/type-system/typeassertion)