---
title: 024: TypeScript에서 클래스가 있는 Type Guard: 클래스 및 인터페이스에서 Type Guard를 사용하는 방법
description: 
published: true
date: 2023-03-03T01:32:23.562Z
tags: 
editor: markdown
dateCreated: 2023-03-03T01:32:22.111Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [024: Type Guards with Classes in TypeScript: How to Use Type Guards with Classes and Interfaces***English** document is available*](/en/Knowledge-base/TypeScript/Learning/024-type-guards-with-classes-in-typescript-how-to-use-type-guards-with-classes-and-interfaces)
{.links-list}
TypeScript에서 클래스가 있는 유형 가드: 클래스 및 인터페이스와 함께 유형 가드를 사용하는 방법

TypeScript는 선택적 정적 타이핑을 언어에 추가하는 JavaScript의 상위 집합입니다. 이를 통해 개발자는 보다 강력하고 유지 관리가 가능하며 이해하기 쉬운 코드를 작성할 수 있습니다. TypeScript의 기능 중 하나는 개발자가 런타임에 변수의 유형을 확인하는 코드를 작성할 수 있도록 하는 유형 가드입니다. 이 기사에서는 TypeScript에서 클래스 및 인터페이스와 함께 유형 가드를 사용하는 방법을 살펴봅니다.

## 타입 가드란?

유형 가드는 런타임에 변수의 유형을 확인하는 방법입니다. 작업을 수행하기 전에 변수가 특정 유형인지 확인하는 데 사용됩니다. 이는 TypeScript가 변수의 유형을 유추할 수 없거나 런타임 중에 변수 유형이 변경되는 경우에 유용합니다.

유형 가드는 `typeof` 연산자, `instanceof` 연산자, 사용자 정의 유형 가드 등을 사용하여 구현할 수 있습니다.

## 클래스가 있는 타입 가드

타입 가드는 변수가 특정 클래스의 인스턴스인지 확인하기 위해 클래스와 함께 사용할 수 있습니다. 이는 클래스가 다른 클래스에서 상속되는 클래스 계층 구조로 작업할 때 유용합니다.

다음 예를 고려하십시오.

```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  breed: string;
  constructor(name: string, breed: string) {
    super(name);
    this.breed = breed;
  }
}

function isAnimal(obj: any): obj is Animal {
  return obj instanceof Animal;
}

const dog = new Dog("Fido", "Labrador");
const animal: Animal = dog;

if (isAnimal(animal)) {
  console.log(animal.name); // Output: Fido
}
```

위의 예에서는 `Animal`과 `Dog`라는 두 개의 클래스를 정의합니다. 또한 주어진 객체가 `Animal` 클래스의 인스턴스인지 확인하는 `isAnimal` 함수를 정의합니다. 이 함수는 부울 값을 반환하지만 함수가 `true`를 반환하면 객체가 `Animal` 클래스의 인스턴스임을 TypeScript에 알려주는 유형 조건자 `obj is Animal`도 있습니다.

그런 다음 `Dog` 클래스의 인스턴스를 만들고 `Animal` 유형의 변수에 할당합니다. 그런 다음 `isAnimal` 함수를 사용하여 변수가 `Animal` 클래스의 인스턴스인지 확인합니다. 그렇다면 `Animal` 클래스의 `name` 속성에 안전하게 액세스할 수 있습니다.

## 인터페이스가 있는 유형 가드

타입 가드는 변수가 특정 인터페이스를 준수하는지 확인하기 위해 인터페이스와 함께 사용할 수도 있습니다. 이는 특정 모양을 가진 개체로 작업할 때 유용합니다.

다음 예를 고려하십시오.

```typescript
interface Person {
  name: string;
  age: number;
}

function isPerson(obj: any): obj is Person {
  return obj && typeof obj.name === "string" && typeof obj.age === "number";
}

const person = { name: "Alice", age: 30 };

if (isPerson(person)) {
  console.log(person.name); // Output: Alice
}
```

위의 예에서 `string` 유형의 `name`과 `number` 유형의 `age`라는 두 가지 속성이 있는 인터페이스 `Person`을 정의합니다. 또한 주어진 객체가 `Person` 인터페이스를 준수하는지 확인하는 `isPerson` 함수를 정의합니다.

그런 다음 `Person` 인터페이스와 모양이 같은 개체를 만들고 변수에 할당합니다. 그런 다음 `isPerson` 함수를 사용하여 변수가 `Person` 인터페이스를 준수하는지 확인합니다. 그렇다면 객체의 `name` 속성에 안전하게 액세스할 수 있습니다.

## 추가 정보

유형 가드는 변수 유형의 범위를 좁히기 위해 공용체 유형과 함께 사용할 수도 있습니다. 이는 둘 이상의 유형을 가질 수 있는 변수로 작업할 때 유용합니다.

다음 예를 고려하십시오.

```typescript
interface Square {
  kind: "square";
  size: number;
}

interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}

interface Circle {
  kind: "circle";
  radius: number;
}

type Shape = Square | Rectangle | Circle;

function isSquare(shape: Shape): shape is Square {
  return shape.kind === "square";
}

const square: Square = { kind: "square", size: 10 };

if (isSquare(square)) {
  console.log(square.size); // Output: 10
}
```

위의 예에서는 `Square`, `Rectangle` 및 `Circle`의 세 가지 인터페이스를 정의합니다. 또한 세 인터페이스 중 하나가 될 수 있는 공용체 유형 'Shape'를 정의합니다.

그런 다음 주어진 `Shape`가 `Square`인지 확인하는 함수 `isSquare`를 정의합니다. 이 함수는 부울 값을 반환하지만 함수가 `true`를 반환하면 변수가 `Square`임을 TypeScript에 알리는 유형 조건자 `shape is Square`도 있습니다.

그런 다음 `Square` 인터페이스의 인스턴스를 만들고 `Shape` 유형의 변수에 할당합니다. 그런 다음 `isSquare` 함수를 사용하여 변수가 `Square`인지 확인합니다. 그렇다면 `Square`의 `size` 속성에 안전하게 액세스할 수 있습니다.

## 경고 및 위험

타입 가드는 특히 복잡한 개체와 함께 사용할 때 성능 측면에서 비용이 많이 들 수 있습니다. 필요한 경우에만 신중하게 사용하는 것이 중요합니다.

유형 가드는 악성 코드에 의해 우회될 수도 있으므로 항상 서버 측에서 사용자 입력의 유효성을 검사하는 것이 중요합니다.

## 결론

TypeScript의 유형 가드는 코드에서 유형 안전을 보장하는 강력한 방법을 제공합니다. 변수 유형을 좁히기 위해 클래스, 인터페이스 및 공용체 유형과 함께 사용할 수 있습니다. 올바르게 사용하면 코드를 보다 강력하고 유지 관리 가능하며 이해하기 쉽게 만들 수 있습니다.

## 외부 리소스

- [TypeScript Handbook: Type Guards 및 Differentiating Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html# type-guards-and-differentiating-types)
- [TypeScript 심층 분석: Type Guards 및 Type Assertions](https://basarat.gitbook.io/typescript/type-system/typeguard)
- [타입스크립트 플레이그라운드](https://www.typescriptlang.org/play)