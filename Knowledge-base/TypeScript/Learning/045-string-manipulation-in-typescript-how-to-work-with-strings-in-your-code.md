---
title: 045: TypeScript에서 문자열 조작: 코드에서 문자열로 작업하는 방법
description: 
published: true
date: 2023-03-03T18:32:29.604Z
tags: 
editor: markdown
dateCreated: 2023-03-03T18:32:22.335Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [045: String Manipulation in TypeScript: How to Work with Strings in Your Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/045-string-manipulation-in-typescript-how-to-work-with-strings-in-your-code)
{.links-list}


문자열 조작은 모든 프로그래밍 언어의 필수 부분입니다. TypeScript에서 문자열은 기본 데이터 유형이며 다양한 방식으로 조작할 수 있습니다. 이 게시물에서는 TypeScript에서 가장 유용한 문자열 조작 기술 중 일부를 살펴보겠습니다.

## 문자열 리터럴

문자열 리터럴은 큰따옴표 또는 작은따옴표로 묶인 일련의 문자입니다. TypeScript에서는 큰따옴표나 작은따옴표를 사용하여 문자열 리터럴을 선언할 수 있습니다.

```typescript
const name: string = "John";
const message: string = 'Hello World!';
```

## 문자열 연결

문자열 연결은 둘 이상의 문자열을 하나로 결합하는 프로세스입니다. TypeScript에서는 `+` 연산자를 사용하여 문자열을 연결할 수 있습니다.

```typescript
const firstName: string = "John";
const lastName: string = "Doe";
const fullName: string = firstName + " " + lastName;
console.log(fullName); // Output: John Doe
```

`+=` 연산자를 사용하여 기존 문자열에 문자열을 추가할 수도 있습니다.

```typescript
let message: string = "Hello";
message += " World!";
console.log(message); // Output: Hello World!
```

## 문자열 보간

문자열 보간은 문자열 리터럴 내부에 식을 삽입하는 방법입니다. TypeScript에서는 `${}` 구문을 사용하여 문자열 리터럴 내에서 표현식을 보간할 수 있습니다.

```typescript
const name: string = "John";
const age: number = 30;
const message: string = `My name is ${name} and I am ${age} years old.`;
console.log(message); // Output: My name is John and I am 30 years old.
```

## 문자열 메서드

TypeScript는 문자열 조작을 위한 몇 가지 기본 제공 메서드를 제공합니다. 다음은 가장 일반적으로 사용되는 몇 가지 방법입니다.

### `charAt()`

`charAt()` 메서드는 문자열의 지정된 인덱스에 있는 문자를 반환합니다.

```typescript
const str: string = "Hello World!";
console.log(str.charAt(0)); // Output: H
console.log(str.charAt(6)); // Output: W
```

### `하위문자열()`

`substring()` 메서드는 지정된 두 인덱스 사이의 문자열 일부를 반환합니다.

```typescript
const str: string = "Hello World!";
console.log(str.substring(0, 5)); // Output: Hello
console.log(str.substring(6)); // Output: World!
```

### `교체()`

`replace()` 메서드는 지정된 값을 문자열의 다른 값으로 바꿉니다.

```typescript
const str: string = "Hello World!";
console.log(str.replace("World", "Universe")); // Output: Hello Universe!
```

### `toLowerCase()` 및 `toUpperCase()`

`toLowerCase()` 메서드는 문자열을 소문자로 변환하고 `toUpperCase()` 메서드는 문자열을 대문자로 변환합니다.

```typescript
const str: string = "Hello World!";
console.log(str.toLowerCase()); // Output: hello world!
console.log(str.toUpperCase()); // Output: HELLO WORLD!
```

### `트림()`

`trim()` 메서드는 문자열의 양쪽 끝에서 공백을 제거합니다.

```typescript
const str: string = "   Hello World!   ";
console.log(str.trim()); // Output: Hello World!
```

## 추가 정보

TypeScript의 문자열은 변경할 수 없습니다. 즉, 문자열이 생성되면 수정할 수 없습니다. 대신 문자열 조작 메서드는 수정된 값이 포함된 새 문자열을 반환합니다.

## 결론

이 게시물에서는 TypeScript에서 가장 유용한 문자열 조작 기술 중 일부를 살펴보았습니다. 문자열 리터럴, 연결, 보간 및 일부 내장 문자열 메서드에 대해 배웠습니다. 이러한 기술을 마스터하면 보다 효율적이고 효과적인 TypeScript 코드를 작성할 수 있습니다.

## 외부 리소스

- [TypeScript 문자열](https://www.tutorialsteacher.com/typescript/typescript-string)
- [TypeScript 문자열 메서드](https://www.tutorialsteacher.com/typescript/typescript-string-methods)