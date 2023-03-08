---
title: 006: TypeScript의 상속과 다형성: 클래스를 확장하고 재정의하는 방법
description: 
published: true
date: 2023-03-06T15:33:05.743Z
tags: 
editor: markdown
dateCreated: 2023-03-06T15:32:58.467Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [006: Inheritance and Polymorphism in TypeScript: How to Extend and Override Classes***English** document is available*](/en/Knowledge-base/TypeScript/Learning/006-inheritance-and-polymorphism-in-typescript-how-to-extend-and-override-classes)
{.links-list}



TypeScript의 상속과 다형성: 클래스를 확장하고 재정의하는 방법

TypeScript는 선택적 정적 타이핑 및 클래스 기반 객체 지향 프로그래밍을 추가하여 JavaScript를 확장하는 객체 지향 프로그래밍 언어입니다. 객체 지향 프로그래밍의 가장 중요한 기능 중 하나는 상속입니다. 상속을 사용하면 기존 클래스를 기반으로 새 클래스를 생성하여 부모 클래스의 모든 속성과 메서드를 상속받을 수 있습니다. 이 게시물에서는 TypeScript의 상속과 다형성을 살펴보고 클래스를 확장하고 재정의하는 방법을 배웁니다.

## TypeScript의 상속

상속은 기존 클래스에서 새 클래스를 만들 수 있게 해주는 메커니즘입니다. 새 클래스를 파생 클래스 또는 하위 클래스라고 하고 기존 클래스를 기본 클래스 또는 슈퍼클래스라고 합니다. 파생 클래스는 기본 클래스의 모든 속성과 메서드를 상속하며 고유한 새 속성과 메서드를 추가할 수도 있습니다.

TypeScript에서 파생 클래스를 생성하려면 `extends` 키워드를 사용합니다. 예를 들면 다음과 같습니다.

```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof! Woof!');
  }
}
```

이 예제에는 `name` 속성과 `move` 메서드가 있는 기본 클래스 `Animal`이 있습니다. 또한 `Animal`을 확장하고 `bark` 메서드를 추가하는 파생 클래스 `Dog`도 있습니다. `Dog` 클래스는 `Animal` 클래스의 `name` 속성과 `move` 메서드를 상속합니다.

다음과 같이 `Dog` 클래스의 인스턴스를 만들고 해당 메서드를 호출할 수 있습니다.

```typescript
let dog = new Dog('Fido');
dog.move(10);
dog.bark();
```

그러면 다음이 출력됩니다.

```
Fido moved 10m.
Woof! Woof!
```

## TypeScript의 다형성

다형성(Polymorphism)은 서로 다른 클래스의 객체를 같은 클래스의 객체인 것처럼 취급할 수 있도록 하는 객체 지향 프로그래밍의 개념입니다. TypeScript에서 다형성은 상속 및 메서드 재정의를 통해 달성됩니다.

메서드 재정의는 파생 클래스가 기본 클래스에 이미 정의된 메서드의 특정 구현을 제공할 수 있도록 하는 기술입니다. 파생 클래스의 재정의된 메서드는 기본 클래스의 메서드와 이름 및 서명이 같지만 구현이 다릅니다.

다음은 TypeScript에서 메서드 재정의의 예입니다.

```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Snake extends Animal {
  move(distanceInMeters = 5) {
    console.log(`${this.name} slithered ${distanceInMeters}m.`);
  }
}

class Horse extends Animal {
  move(distanceInMeters = 45) {
    console.log(`${this.name} galloped ${distanceInMeters}m.`);
  }
}

let sam = new Snake('Sammy the Python');
let tom: Animal = new Horse('Tommy the Palomino');

sam.move();
tom.move(34);
```

이 예제에는 `name` 속성과 `move` 메서드가 있는 기본 클래스 `Animal`이 있습니다. 또한 자체 구현으로 `move` 메서드를 재정의하는 두 개의 파생 클래스 `Snake`와 `Horse`가 있습니다.

우리는 두 클래스의 인스턴스를 생성하고 그들의 `move` 메서드를 호출합니다. `Snake` 인스턴스는 `"Sammy the Python slithered 5m."`을 출력하는 재정의된 `move` 메소드를 호출합니다. `Horse` 인스턴스는 `"Tommy the Palomino galloped 34m."`을 출력하는 재정의된 `move` 메소드를 호출합니다.

## 클래스 확장 및 재정의

TypeScript에서는 클래스를 확장하고 재정의하여 보다 전문적인 클래스를 만들 수 있습니다. 클래스를 확장하면 기본 클래스의 모든 속성과 메서드를 상속할 수 있고, 메서드를 재정의하면 파생 클래스에서 해당 메서드를 보다 구체적으로 구현할 수 있습니다.

다음은 TypeScript에서 클래스를 확장하고 재정의하는 예입니다.

```typescript
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

class Programmer extends Person {
  greet() {
    console.log(`Hello, my name is ${this.name} and I'm a programmer.`);
  }
  code() {
    console.log(`${this.name} is coding...`);
  }
}

let john = new Person('John');
let jane = new Programmer('Jane');

john.greet();
jane.greet();
jane.code();
```

이 예제에는 `name` 속성과 `greet` 메서드가 있는 기본 클래스 `Person`이 있습니다. 또한 `Person`을 확장하고 `greet` 메서드를 보다 구체적인 구현으로 재정의하는 파생 클래스 `Programmer`도 있습니다. `Programmer` 클래스는 또한 새로운 `code` 메소드를 추가합니다.

두 클래스의 인스턴스를 만들고 `greet` 및 `code` 메서드를 호출합니다. `Person` 인스턴스는 `"Hello, my name is John."`을 출력하는 자체 `greet` 메서드를 호출합니다. `Programmer` 인스턴스는 `"Hello, my name is Jane and I'm aprogrammer."`를 출력하는 재정의된 `greet` 메서드를 호출합니다. `Programmer` 인스턴스는 `"Jane is coding..."`을 출력하는 자체 `code` 메서드도 호출합니다.

## 추가 정보

TypeScript에서는 인터페이스를 사용하여 객체의 모양을 정의할 수도 있습니다. 인터페이스는 클래스의 공용 API를 설명하거나 함수 매개변수 또는 반환 값의 유형을 정의하는 데 사용할 수 있습니다.

## 결론

상속과 다형성은 객체 지향 프로그래밍에서 중요한 개념이며 TypeScript는 이를 구현하기 위한 강력한 메커니즘을 제공합니다. 클래스를 확장하고 재정의함으로써 부모 클래스의 동작을 상속하고 수정하는 보다 전문화된 클래스를 만들 수 있습니다. 또한 인터페이스는 객체의 모양을 정의하고 코드에서 유형 안전성을 보장하는 방법을 제공합니다.

## 외부 리소스

- [TypeScript 핸드북: 상속](https://www.typescriptlang.org/docs/handbook/2/objects.html# inheritance)
- [TypeScript 핸드북: 다형성](https://www.typescriptlang.org/docs/handbook/2/classes.html# polymorphism)
- [TypeScript 핸드북: 인터페이스](https://www.typescriptlang.org/docs/handbook/interfaces.html)