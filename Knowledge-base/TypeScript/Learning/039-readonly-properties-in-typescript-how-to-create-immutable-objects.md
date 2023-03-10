---
title: 039: TypeScript의 읽기 전용 속성: 불변 객체를 만드는 방법
description: 
published: true
date: 2023-03-10T17:32:42.080Z
tags: 
editor: markdown
dateCreated: 2023-03-10T17:32:42.080Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [039: Readonly Properties in TypeScript: How to Create Immutable Objects***English** document is available*](/en/Knowledge-base/TypeScript/Learning/039-readonly-properties-in-typescript-how-to-create-immutable-objects)
{.links-list}



TypeScript는 보다 강력하고 유지 관리 가능한 코드를 작성하는 데 도움이 되는 여러 기능을 제공하는 JavaScript의 상위 집합입니다. 이러한 기능 중 하나는 개발자가 변경할 수 없는 개체를 만들 수 있도록 하는 읽기 전용 속성입니다. 불변 객체는 일단 생성되면 상태를 변경할 수 없는 객체로, 실수로 객체 상태를 변경하여 발생하는 버그를 방지하는 데 도움이 될 수 있습니다.

이 게시물에서는 TypeScript에서 읽기 전용 속성을 사용하여 불변 개체를 만드는 방법을 살펴보겠습니다.

## 읽기 전용 속성이란 무엇입니까?

읽기 전용 속성은 개체 초기화 중에만 값을 할당할 수 있는 속성입니다. 일단 할당되면 값을 변경할 수 없습니다. 이 기능은 생성 후 상태가 변경되지 않아야 하는 개체를 생성하려는 경우에 유용합니다.

TypeScript에서 읽기 전용 속성을 생성하려면 속성 이름 앞에 `readonly` 키워드를 사용할 수 있습니다. 예를 들면 다음과 같습니다.

```typescript
class Person {
  readonly name: string;
  readonly age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

const person = new Person("John", 30);
person.name = "Jane"; // Error: Cannot assign to 'name' because it is a read-only property.
```

이 예제에서는 `name` 및 `age`라는 두 가지 읽기 전용 속성을 사용하여 `Person` 클래스를 정의합니다. 생성자는 이러한 속성을 초기화하며 일단 초기화되면 해당 값을 변경할 수 없습니다.

## 읽기 전용 속성의 이점

읽기 전용 속성을 사용하면 다음과 같은 몇 가지 이점이 있습니다.

### 우발적인 변경 방지

읽기 전용 속성의 주요 이점 중 하나는 객체 상태가 우발적으로 변경되는 것을 방지한다는 것입니다. 위의 예에서 `name` 및 `age` 속성을 읽기 전용으로 만들지 않은 경우 개체 초기화 후 해당 값을 변경할 수 있으며 이로 인해 예기치 않은 동작 및 버그가 발생할 수 있습니다.

### 코드 가독성 향상

읽기 전용 속성은 개체 초기화 후 변경해서는 안 되는 속성을 명확하게 하여 코드 가독성을 향상시킬 수도 있습니다. 이는 복잡한 개체로 작업하거나 다른 개발자와 공동 작업할 때 유용할 수 있습니다.

### 설계 결정 시행

읽기 전용 속성은 특정 속성이 개체 초기화 중에만 설정되도록 하는 것과 같은 디자인 결정을 적용하는 데 도움이 될 수도 있습니다. 이는 여러 개발자와 함께 대규모 프로젝트를 진행하거나 라이브러리 또는 프레임워크를 개발할 때 유용할 수 있습니다.

## 읽기 전용 속성의 제한 사항

읽기 전용 속성은 개체 상태가 실수로 변경되는 것을 방지하는 데 도움이 될 수 있지만 몇 가지 제한 사항이 있습니다.

### 얕은 불변성

읽기 전용 속성은 얕은 불변성만 제공합니다. 즉, 개체에 읽기 전용이 아닌 속성이 포함된 경우 해당 속성을 계속 변경할 수 있습니다. 예를 들어:

```typescript
class Person {
  readonly name: string;
  address: { street: string; city: string };

  constructor(name: string, street: string, city: string) {
    this.name = name;
    this.address = { street, city };
  }
}

const person = new Person("John", "123 Main St", "Anytown");
person.address.street = "456 Main St"; // No error
```

이 예에서 `Person` 클래스에는 읽기 전용 `name` 속성과 읽기 전용이 아닌 `address` 속성이 있습니다. 개체 초기화 후에는 `name` 속성을 변경할 수 없지만 `address` 속성은 여전히 수정할 수 있습니다.

### 물체 봉인

읽기 전용 속성은 개체를 봉인하지 않습니다. 즉, 초기화 후에도 개체에 새 속성을 추가할 수 있습니다. 예를 들어:

```typescript
class Person {
  readonly name: string;
  readonly age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
    Object.seal(this);
  }
}

const person = new Person("John", 30);
person.address = "123 Main St"; // No error
```

이 예제에서는 초기화 후 `Person` 개체에 새 속성이 추가되지 않도록 `Object.seal`을 사용합니다. 그러나 읽기 전용 속성은 개체를 봉인하지 않기 때문에 여전히 새 속성을 개체에 추가할 수 있습니다.

## 결론

TypeScript의 읽기 전용 속성은 불변 객체를 생성하는 방법을 제공하여 객체 상태를 실수로 변경하여 발생하는 버그를 방지할 수 있습니다. 읽기 전용 속성에는 몇 가지 제한 사항이 있지만 코드 가독성을 개선하고 디자인 결정을 적용하는 데 도움이 될 수 있습니다.

TypeScript에 대해 자세히 알아보려면 아래 리소스를 확인하세요.

- [TypeScript 핸드북](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript 심층 분석](https://basarat.gitbook.io/typescript/)
- [5분 안에 TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)