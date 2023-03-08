---
title: 002: TypeScript의 기본 유형: 변수 및 데이터 유형 이해
description: 
published: true
date: 2023-03-02T08:41:23.879Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:41:16.759Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [002: Basic Types in TypeScript: Understanding Variables and Data Types***English** document is available*](/en/Knowledge-base/TypeScript/Learning/002-basic-types-in-typescript-understanding-variables-and-data-types)
{.links-list}


TypeScript의 기본 유형: 변수 및 데이터 유형 이해

TypeScript는 선택적 정적 타이핑 및 클래스 기반 객체 지향 프로그래밍 기능을 추가하는 JavaScript의 상위 집합입니다. 대규모 웹 응용 프로그램을 보다 쉽게 관리하고 유지 관리할 수 있도록 설계되었습니다. TypeScript의 가장 기본적인 개념 중 하나는 변수 및 데이터 유형의 개념입니다. 이 게시물에서는 TypeScript의 기본 유형과 이를 코드에서 사용하는 방법에 대해 설명합니다.

## TypeScript의 변수

TypeScript의 변수는 `let` 키워드를 사용하여 선언됩니다. 모든 유형의 값을 할당할 수 있지만 변수에 특정 유형의 값을 할당하면 다른 유형의 값을 할당할 수 없습니다. 이는 TypeScript가 정적으로 유형이 지정되는 언어이기 때문입니다. 즉, 변수의 유형은 런타임이 아닌 컴파일 타임에 결정됩니다.

### 예

```typescript
let age: number;
age = 30;
```

이 예에서는 '숫자' 유형의 변수 '나이'를 선언하고 값 '30'을 할당합니다. 변수의 유형은 명시적으로 유형을 지정하기 때문에 `숫자`로 유추됩니다.

### 유형 추론

TypeScript에는 유형 유추라는 기능이 있어 변수의 유형을 해당 값에서 유추할 수 있습니다. 즉, 항상 변수 유형을 명시적으로 지정할 필요는 없습니다.

### 예

```typescript
let name = "John";
```

이 예제에서는 `name` 변수를 선언하고 `"John"` 값을 할당합니다. 변수의 값이 문자열이기 때문에 변수의 유형은 `문자열`로 유추됩니다.

### 상수

상수는 초기화되면 재할당할 수 없는 변수입니다. 그것들은 `const` 키워드를 사용하여 선언됩니다.

### 예

```typescript
const pi = 3.14;
```

이 예에서는 상수 `pi`를 선언하고 값 `3.14`를 할당합니다. 상수에 값이 할당되면 다시 할당할 수 없습니다.

## TypeScript의 기본 유형

TypeScript는 변수를 선언하는 데 사용할 수 있는 몇 가지 기본 유형을 제공합니다. 여기에는 다음이 포함됩니다.

- `숫자`
- `문자열`
- `부울`
- `널`
- `정의되지 않음`

### 숫자

`숫자` 유형은 숫자 값을 나타내는 데 사용됩니다. 여기에는 정수와 부동 소수점 숫자가 모두 포함됩니다.

### 예

```typescript
let age: number = 30;
let height: number = 1.75;
```

이 예에서는 '숫자' 유형의 두 변수 '나이'와 '높이'를 선언합니다.

### 끈

`문자열` 유형은 텍스트 데이터를 나타내는 데 사용됩니다. 여기에는 작은따옴표와 큰따옴표 문자열이 모두 포함됩니다.

### 예

```typescript
let name: string = "John";
let message: string = 'Hello, world!';
```

이 예제에서는 `string` 유형의 `name` 및 `message` 변수 두 개를 선언합니다.

### 부울

`boolean` 유형은 논리 값을 나타내는 데 사용됩니다. 여기에는 'true'와 'false'의 두 가지 가능한 값만 포함됩니다.

### 예

```typescript
let isDone: boolean = false;
```

이 예에서는 `boolean` 유형의 `isDone` 변수를 선언합니다.

### Null 및 정의되지 않음

`null` 및 `undefined` 유형은 값이 없음을 나타내는 데 사용됩니다.

### 예

```typescript
let x: null = null;
let y: undefined = undefined;
```

이 예제에서는 각각 `null` 및 `undefined` 유형의 두 변수 `x` 및 `y`를 선언합니다.

### 유형 어설션

TypeScript를 사용하면 유형 어설션이라는 구문을 사용하여 변수의 유형을 명시적으로 지정할 수 있습니다. 이는 변수의 유형을 자동으로 유추할 수 없을 때 유용합니다.

### 예

```typescript
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```

이 예제에서는 `any` 유형의 `someValue` 변수를 선언하고 `"this is a string"` 값을 할당합니다. 그런 다음 유형 어설션을 사용하여 `someValue`가 문자열임을 지정하고 길이를 `strLength` 변수에 할당합니다.

## 결론

이 게시물에서는 TypeScript의 기본 유형과 이를 코드에서 사용하는 방법에 대해 논의했습니다. 변수, 유형 유추, 상수 및 유형 어설션을 다루었습니다. 이러한 개념을 이해하는 것은 TypeScript로 작업하는 데 필수적이며 보다 강력하고 유지 관리 가능한 코드를 작성하는 데 도움이 됩니다.

## 추가 정보

- [TypeScript 설명서](https://www.typescriptlang.org/docs/)
- [타입스크립트 플레이그라운드](https://www.typescriptlang.org/play)