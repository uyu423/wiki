---
title: 014: TypeScript의 열거형: 열거형을 정의하고 사용하는 방법
description: 
published: true
date: 2023-03-06T17:32:46.013Z
tags: 
editor: markdown
dateCreated: 2023-03-06T17:32:38.671Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [014: Enums in TypeScript: How to Define and Use Enumerated Types***English** document is available*](/en/Knowledge-base/TypeScript/Learning/014-enums-in-typescript-how-to-define-and-use-enumerated-types)
{.links-list}



TypeScript의 열거형: 열거형을 정의하고 사용하는 방법

TypeScript는 선택적 정적 타이핑, 클래스 및 인터페이스를 제공하는 널리 사용되는 프로그래밍 언어입니다. 언어의 가장 강력한 기능 중 하나는 개발자가 열거 유형을 정의하고 사용할 수 있게 해주는 열거형입니다. 이 게시물에서는 Enum이 무엇인지, Enum을 정의하는 방법 및 TypeScript 코드에서 Enum을 사용하는 방법을 살펴봅니다.

## Enum이 무엇인가요?

열거형은 TypeScript에서 명명된 상수 집합을 정의하는 방법입니다. 숫자 또는 문자열 값에 친숙한 이름을 지정하여 코드를 더 읽기 쉽고 이해하기 쉽게 만드는 방법을 제공합니다. 열거형은 매직 넘버 또는 문자열 리터럴 대신 사용할 수 있으므로 코드를 보다 유지 관리하기 쉽고 오류가 덜 발생하도록 할 수 있습니다.

## TypeScript에서 열거형 정의하기

TypeScript에서 Enum을 정의하려면 'enum' 키워드 뒤에 Enum 이름을 사용합니다. Enum 값의 이름은 중괄호 안에 정의되며 쉼표로 구분됩니다. 예를 들면 다음과 같습니다.

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right
}
```

이 예제에서는 `Up`, `Down`, `Left` 및 `Right`의 네 가지 값을 사용하여 `Direction`이라는 열거형을 정의합니다. 기본적으로 TypeScript는 0부터 시작하여 각 Enum 값에 숫자 값을 할당합니다. 따라서 `Up`의 값은 0이고 `Down`의 값은 1입니다.

다음과 같이 값을 Enum 값에 명시적으로 할당할 수도 있습니다.

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}
```

이 예에서는 각 Enum 값에 문자열 값을 할당합니다.

## TypeScript에서 열거형 사용

TypeScript에서 Enum을 사용하려면 간단히 이름으로 참조하면 됩니다. 예를 들면 다음과 같습니다.

```typescript
let direction: Direction = Direction.Up;
console.log(direction); // Output: 0
```

이 예제에서는 `Direction` 유형의 `direction`이라는 변수를 선언하고 `Direction.Up` 값을 할당합니다. `방향` 값을 콘솔에 기록하면 숫자 값 0을 얻습니다.

다음과 같이 switch 문에서 열거형을 사용할 수도 있습니다.

```typescript
switch (direction) {
  case Direction.Up:
    console.log("Going up!");
    break;
  case Direction.Down:
    console.log("Going down!");
    break;
  case Direction.Left:
    console.log("Going left!");
    break;
  case Direction.Right:
    console.log("Going right!");
    break;
  default:
    console.log("Invalid direction.");
}
```

이 예에서는 switch 문을 사용하여 `direction` 값을 기반으로 메시지를 기록합니다.

## 추가 정보

- 숫자 및 문자열 값 모두와 함께 열거형을 사용할 수 있습니다.
- 여러 값을 단일 값으로 결합할 수 있는 비트 플래그와 함께 열거형을 사용할 수도 있습니다.

## 경고

- Enum에 숫자 값을 할당할 때 값이 고유하지 않은 경우 예기치 않은 동작이 발생할 수 있으므로 주의하십시오.
- 열거형을 비트 플래그와 함께 사용할 때는 코드를 더 복잡하고 이해하기 어렵게 만들 수 있으므로 주의하십시오.

## 결론

열거형은 열거형 유형을 정의하고 사용할 수 있게 해주는 TypeScript의 강력한 기능입니다. 숫자 또는 문자열 값에 친숙한 이름을 지정하여 코드를 더 읽기 쉽고 이해하기 쉽게 만드는 방법을 제공합니다. TypeScript 코드에서 열거형을 사용하면 코드를 유지 관리하기 쉽고 오류가 덜 발생하도록 만들 수 있습니다.

## 더 읽을 거리

- [TypeScript 핸드북: Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [TypeScript의 열거형: 기본 사항](https://blog.logrocket.com/enums-in-typescript-the-basics-9fd96b0efa8a/)
- [TypeScript의 Enum 이해하기](https://www.sitepoint.com/understanding-enums-in-typescript/)