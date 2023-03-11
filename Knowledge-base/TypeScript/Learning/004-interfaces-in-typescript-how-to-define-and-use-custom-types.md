---
title: 004: TypeScript의 인터페이스: 사용자 지정 유형을 정의하고 사용하는 방법
description: 
published: true
date: 2023-03-11T06:32:45.655Z
tags: 
editor: markdown
dateCreated: 2023-03-11T06:32:45.655Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [004: Interfaces in TypeScript: How to Define and Use Custom Types***English** document is available*](/en/Knowledge-base/TypeScript/Learning/004-interfaces-in-typescript-how-to-define-and-use-custom-types)
{.links-list}

TypeScript의 인터페이스: 사용자 지정 유형을 정의하고 사용하는 방법

TypeScript는 개발 프로세스를 개선하기 위해 유형 검사 및 기타 기능을 제공하는 JavaScript의 상위 집합입니다. TypeScript의 주요 기능 중 하나는 인터페이스를 통해 사용자 정의 유형을 정의하고 사용하는 기능입니다. 이 기사에서는 인터페이스가 무엇이며 TypeScript에서 인터페이스를 정의하고 사용하는 방법을 살펴봅니다.

## 인터페이스란?

TypeScript의 인터페이스는 사용자 정의 유형을 정의하는 데 사용됩니다. 속성 및 메서드를 포함하여 개체의 모양을 정의하는 방법을 제공합니다. 인터페이스는 함수 서명 및 클래스 유형을 정의하는 데에도 사용할 수 있습니다.

TypeScript에서 인터페이스는 순전히 컴파일 타임 구성이며 런타임 표현이 없습니다. TypeScript 컴파일러에서 컴파일 타임에 변수, 함수 매개변수 및 반환 값의 유형을 확인하는 데 사용됩니다.

## 인터페이스 정의

TypeScript에서 인터페이스를 정의하려면 'interface' 키워드 뒤에 인터페이스 이름과 인터페이스의 속성 및 메서드를 포함하는 중괄호 세트를 사용합니다.

```typescript
interface Person {
  firstName: string;
  lastName: string;
  age: number;
  sayHello(): void;
}
```

위의 예에서는 세 개의 속성(`firstName`, `lastName` 및 `age`)과 하나의 메서드(`sayHello`)가 있는 `Person`이라는 인터페이스를 정의합니다. `firstName` 및 `lastName` 속성은 `string` 유형이고 `age` 속성은 `number` 유형입니다. `sayHello` 메서드는 매개변수를 사용하지 않고 `void`를 반환합니다.

## 인터페이스 사용

인터페이스를 정의하고 나면 인터페이스를 사용하여 변수 유형, 함수 매개변수 및 반환 값을 정의할 수 있습니다.

```typescript
function greet(person: Person): void {
  console.log(`Hello, ${person.firstName} ${person.lastName}!`);
  person.sayHello();
}

const john: Person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30,
  sayHello: () => console.log('Hello!'),
};

greet(john);
```

위의 예에서 'Person' 유형의 매개변수를 사용하는 'greet'라는 함수를 정의합니다. 함수 내에서 `Person` 개체의 `firstName` 및 `lastName` 속성을 사용하여 인사말 메시지를 인쇄하고 `sayHello` 메서드를 호출합니다.

또한 `Person` 유형의 `john`이라는 변수를 정의하고 필요한 속성과 메서드가 있는 객체로 초기화합니다.

## 선택적 속성

인터페이스에서 이름 뒤에 물음표 `?`를 추가하여 속성을 선택 사항으로 표시할 수 있습니다.

```typescript
interface Person {
  firstName: string;
  lastName: string;
  age?: number;
  sayHello(): void;
}
```

위의 업데이트된 `Person` 인터페이스에서 `age` 속성을 선택 사항으로 표시합니다. 이것은 `Person` 유형의 객체가 age 속성을 가질 수 있는지 여부를 의미합니다.

## 읽기 전용 속성

인터페이스에서 이름 앞에 `readonly` 키워드를 추가하여 속성을 읽기 전용으로 표시할 수 있습니다.

```typescript
interface Person {
  readonly firstName: string;
  readonly lastName: string;
  age?: number;
  sayHello(): void;
}
```

위의 업데이트된 `Person` 인터페이스에서 `firstName` 및 `lastName` 속성을 읽기 전용으로 표시합니다. 즉, 일단 설정되면 값을 변경할 수 없습니다.

## 인터페이스 확장

TypeScript의 인터페이스를 확장하여 기존 인터페이스의 속성과 메서드를 상속하는 새 인터페이스를 만들 수도 있습니다.

```typescript
interface Animal {
  name: string;
  eat(food: string): void;
}

interface Dog extends Animal {
  bark(): void;
}

const dog: Dog = {
  name: 'Rex',
  eat: (food) => console.log(`Eating ${food}`),
  bark: () => console.log('Woof!'),
};

dog.eat('meat');
dog.bark();
```

위의 예에서 두 개의 속성(`name` 및 `eat`)이 있는 `Animal`이라는 인터페이스와 `Animal`을 확장하고 `bark` 메서드를 추가하는 `Dog` 인터페이스를 정의합니다.

그런 다음 'Dog' 유형의 'dog'라는 변수를 정의하고 필요한 속성과 메서드가 있는 객체로 초기화합니다.

## 결론

이 기사에서는 인터페이스가 무엇이며 TypeScript에서 인터페이스를 정의하고 사용하는 방법을 살펴보았습니다. 속성 및 메서드를 포함하여 개체의 모양을 정의하는 데 인터페이스를 사용하는 방법과 함수 시그니처 및 클래스 유형을 정의하는 데 사용하는 방법을 살펴보았습니다.

인터페이스는 코드의 유지 관리 및 가독성을 개선하는 데 도움이 되는 TypeScript의 강력한 기능입니다. 인터페이스를 사용하여 데이터 구조를 정확하게 반영하는 사용자 정의 유형을 정의하고 코드가 유형에 안전한지 확인할 수 있습니다.

## 추가 정보

- TypeScript 핸드북: 인터페이스 - https://www.typescriptlang.org/docs/handbook/interfaces.html
- TypeScript 심층 분석: 인터페이스 - https://basarat.gitbook.io/typescript/type-system/interfaces

## 경고 및 위험

- 인터페이스를 정의할 때 이해하고 유지하기 어려운 지나치게 복잡한 타입을 만들지 않도록 주의한다.
- 인터페이스는 컴파일 타임 구성일 뿐이며 런타임 표현이 없다는 점에 유의하십시오.