---
title: 042: TypeScript에서 문자열 조작: 코드에서 문자열로 작업하는 방법
description: 
published: true
date: 2023-03-02T14:32:16.127Z
tags: 
editor: markdown
dateCreated: 2023-03-02T14:32:16.127Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [042: String Manipulation in TypeScript: How to Work with Strings in Your Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/042-string-manipulation-in-typescript-how-to-work-with-strings-in-your-code)
{.links-list}


문자열 조작은 모든 프로그래밍 언어의 필수 부분입니다. TypeScript에서 문자열은 텍스트 데이터로 작업할 수 있게 해주는 객체입니다. 이 게시물에서는 TypeScript에서 문자열을 조작하는 다양한 방법을 살펴보겠습니다.

## TypeScript의 문자열

TypeScript에서 문자열은 따옴표로 묶인 일련의 문자입니다. 작은따옴표나 큰따옴표를 사용하여 문자열을 정의할 수 있습니다. 예를 들어:

```typescript
let name: string = "John";
let message: string = 'Hello World!';
```

템플릿 리터럴을 사용하여 자리 표시자를 포함할 수 있는 문자열을 정의할 수도 있습니다. 예를 들어:

```typescript
let name: string = "John";
let message: string = `Hello ${name}!`;
```

### 문자열 속성 및 메서드

TypeScript의 문자열에는 문자열을 조작할 수 있는 여러 속성과 메서드가 있습니다. 다음은 가장 일반적으로 사용되는 몇 가지 속성 및 메서드입니다.

#### 길이

길이 속성은 문자열의 문자 수를 반환합니다. 예를 들어:

```typescript
let name: string = "John";
let length: number = name.length; // length is 4
```

#### toUpperCase 및 toLowerCase

toUpperCase 메서드는 모든 문자가 대문자로 변환된 새 문자열을 반환합니다. toLowerCase 메서드는 모든 문자가 소문자로 변환된 새 문자열을 반환합니다. 예를 들어:

```typescript
let name: string = "John";
let upperCaseName: string = name.toUpperCase(); // "JOHN"
let lowerCaseName: string = name.toLowerCase(); // "john"
```

#### indexOf 및 lastIndexOf

indexOf 메서드는 문자열에서 지정된 값이 처음 나타나는 인덱스를 반환합니다. lastIndexOf 메서드는 문자열에서 지정된 값이 마지막으로 나타나는 인덱스를 반환합니다. 예를 들어:

```typescript
let message: string = "Hello World!";
let index: number = message.indexOf("o"); // index is 4
let lastIndex: number = message.lastIndexOf("o"); // lastIndex is 7
```

#### 하위 문자열 및 슬라이스

하위 문자열 메서드는 문자열의 지정된 부분을 포함하는 새 문자열을 반환합니다. 슬라이스 메서드는 또한 문자열의 지정된 부분을 포함하는 새 문자열을 반환하지만 음수 값이 문자열 끝에서 위치를 나타낼 수 있도록 합니다. 예를 들어:

```typescript
let message: string = "Hello World!";
let substring: string = message.substring(0, 5); // "Hello"
let slice: string = message.slice(-6); // "World!"
```

#### 바꾸다

replace 메서드는 지정된 값을 문자열의 다른 값으로 바꿉니다. 예를 들어:

```typescript
let message: string = "Hello World!";
let newMessage: string = message.replace("World", "John"); // "Hello John!"
```

### 추가 정보

TypeScript의 문자열은 변경할 수 없습니다. 즉, 문자열을 생성하면 수정할 수 없습니다. 그러나 문자열 메서드를 사용하여 새 문자열을 만들 수 있습니다.

### 경고

TypeScript에서 문자열로 작업할 때 사용하는 변수 유형에 주의하세요. TypeScript는 강력한 유형의 언어이므로 변수에 올바른 유형을 지정해야 합니다. 잘못된 유형을 할당하면 예기치 않은 결과가 발생할 수 있습니다.

### 위험

사용자 입력 또는 외부 소스의 데이터가 포함된 문자열로 작업할 때 SQL 삽입 공격 또는 교차 사이트 스크립팅 공격과 같은 보안 취약점에 주의하십시오. 항상 사용자 입력을 삭제하고 외부 소스의 데이터를 검증하십시오.

## 결론

이 게시물에서는 TypeScript에서 문자열을 조작하는 다양한 방법을 살펴보았습니다. length, toUpperCase, toLowerCase, indexOf, lastIndexOf, substring, slice, replace와 같은 문자열 속성과 메소드를 다루었습니다. 사용하는 변수 유형에 주의하고 사용자 입력 또는 외부 소스의 데이터로 작업할 때 보안 취약점에 유의하십시오.

## 외부 리소스

- [TypeScript 문자열](https://www.tutorialsteacher.com/typescript/typescript-string)
- [MDN 웹 문서: 문자열](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)