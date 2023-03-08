---
title: 033: TypeScript의 This 유형: 클래스와 함수에서 'this' 키워드로 작업하는 방법
description: 
published: true
date: 2023-03-04T02:32:40.937Z
tags: 
editor: markdown
dateCreated: 2023-03-04T02:32:39.550Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [033: This Types in TypeScript: How to Work with the 'this' Keyword in Classes and Functions***English** document is available*](/en/Knowledge-base/TypeScript/Learning/033-this-types-in-typescript-how-to-work-with-the-this-keyword-in-classes-and-functions)
{.links-list}


TypeScript의 This 유형: 클래스 및 함수에서 'this' 키워드로 작업하는 방법

TypeScript로 작업할 때 'this' 키워드를 접했을 수 있습니다. 'this' 키워드는 개체 또는 클래스의 현재 인스턴스를 참조하는 데 사용됩니다. 특히 함수와 클래스를 다룰 때 작업하기가 약간 혼란스러울 수 있습니다. 이 게시물에서는 'this' 키워드와 TypeScript에서 이를 사용하는 방법을 살펴봅니다.

## TypeScript에서 'this' 이해하기

TypeScript에서 'this' 키워드는 개체 또는 클래스의 현재 인스턴스를 참조하는 데 사용됩니다. 클래스의 함수나 메서드 내에서 사용될 때 'this'는 해당 클래스의 인스턴스를 나타냅니다. 클래스의 일부가 아닌 함수 내에서 사용될 때 'this'는 전역 개체(브라우저의 창 또는 Node.js의 전역)를 나타냅니다.

예를 들어 다음 클래스를 고려하십시오.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person('John', 30);
person.greet(); // Output: Hello, my name is John and I am 30 years old.
```

이 예제에는 생성자와 Greeting 메서드가 있는 Person 클래스가 있습니다. welcome 메서드 내에서 'this' 키워드를 사용하여 Person 클래스의 현재 인스턴스를 참조합니다. Person 클래스의 새 인스턴스를 생성하고 greet 메서드를 호출하면 출력은 "Hello, my name is John and I am 30 years old."입니다.

## 함수에서 'this' 사용하기

클래스의 일부가 아닌 함수 내에서 'this' 키워드를 사용하면 전역 개체를 참조합니다. 특정 개체를 참조하기 위해 'this'를 사용하려는 경우 문제가 될 수 있습니다. 이 문제를 해결하기 위해 호출, 적용 또는 바인드 메소드를 사용할 수 있습니다.

### 호출 방법

call 메서드는 지정된 'this' 값과 개별적으로 제공된 인수를 사용하여 함수를 호출하는 데 사용됩니다.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const person = {
  name: 'John',
  age: 30
};

greet.call(person); // Output: Hello, my name is John and I am 30 years old.
```

이 예제에는 'this' 키워드를 사용하여 개체의 이름 및 연령 속성을 참조하는 greeting 함수가 있습니다. name 및 age 속성을 가진 person 개체를 만든 다음 call 메서드를 사용하여 person 개체를 'this' 값으로 하는 greeting 함수를 호출합니다.

### 적용 방법

적용 방법은 호출 방법과 유사하지만 인수를 배열로 사용합니다.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const person = {
  name: 'John',
  age: 30
};

greet.apply(person); // Output: Hello, my name is John and I am 30 years old.
```

이 예제에서는 이전과 동일한 Greeting 함수와 person 객체를 사용하지만 call 메서드 대신 apply 메서드를 사용합니다.

### 바인드 방법

bind 메서드는 지정된 'this' 값으로 새 함수를 만드는 데 사용됩니다.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const person = {
  name: 'John',
  age: 30
};

const greetPerson = greet.bind(person);
greetPerson(); // Output: Hello, my name is John and I am 30 years old.
```

이 예제에서는 bind 메서드를 사용하여 greetPerson이라는 새 함수를 만듭니다. welcomePerson 함수는 person 개체의 'this' 값을 가집니다.

## 클래스에서 'this' 사용하기

클래스 내에서 'this' 키워드를 사용하면 해당 클래스의 인스턴스를 참조합니다. 그러나 이벤트 리스너를 사용하거나 메서드를 콜백으로 전달하는 경우와 같이 'this'가 문제가 될 수 있는 경우가 있습니다.

### 화살표 함수 사용

클래스에서 'this'와 관련된 문제를 피하는 한 가지 방법은 화살표 함수를 사용하는 것입니다. 화살표 함수에는 자체 'this' 값이 없으므로 둘러싸는 어휘 범위의 'this' 값을 사용합니다.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;

    document.addEventListener('click', () => {
      this.greet();
    });
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person('John', 30);
```

이 예제에는 문서에 이벤트 리스너를 추가하는 생성자가 포함된 Person 클래스가 있습니다. 이벤트 리스너 내에서 화살표 함수를 사용하여 Person 클래스의 인스턴스를 참조하기 위해 'this' 키워드를 사용하는 Person 클래스의 greet 메서드를 호출합니다.

### 바인드 사용

클래스에서 'this'와 관련된 문제를 해결하는 또 다른 방법은 바인드 방법을 사용하는 것입니다.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;

    document.addEventListener('click', this.greet.bind(this));
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person('John', 30);
```

이 예제에서는 bind 메서드를 사용하여 Greeting 메서드의 'this' 값을 Person 클래스의 인스턴스에 바인딩합니다.

## 결론

이 게시물에서는 TypeScript의 'this' 키워드와 함수 및 클래스에서 이를 사용하는 방법을 살펴보았습니다. 호출, 적용 및 바인딩을 사용하여 함수의 'this' 값을 지정하는 방법과 클래스에서 'this'의 문제를 피하기 위해 화살표 함수 및 바인딩을 사용하는 방법을 살펴보았습니다. TypeScript에서 'this'로 작업하는 방법을 이해하면 보다 효과적이고 효율적인 코드를 작성할 수 있습니다.

## 추가 정보

- [MDN 웹 문서 - this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [TypeScript 문서 - 클래스](https://www.typescriptlang.org/docs/handbook/classes.html)
- [TypeScript 설명서 - 함수](https://www.typescriptlang.org/docs/handbook/functions.html)

## 경고

- 기본적으로 전역 개체를 참조하므로 클래스의 일부가 아닌 함수 내에서 'this'를 사용할 때 주의하십시오.
- 클래스에서 화살표 함수를 사용할 때 자체 'this' 값을 가지고 있지 않고 둘러싸는 어휘 범위의 'this' 값을 사용한다는 점에 유의하십시오.

## 위험

- 'this'를 잘못 사용하면 코드에서 예기치 않은 동작 및 버그가 발생할 수 있습니다. 이것을 사용하기 전에 항상 'this'가 어떻게 작동하는지 이해했는지 확인하십시오.