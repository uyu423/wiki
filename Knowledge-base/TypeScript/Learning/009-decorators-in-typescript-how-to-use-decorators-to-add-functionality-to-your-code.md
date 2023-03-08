---
title: 009: TypeScript의 데코레이터: 데코레이터를 사용하여 코드에 기능을 추가하는 방법
description: 
published: true
date: 2023-03-07T04:32:46.297Z
tags: 
editor: markdown
dateCreated: 2023-03-07T04:32:38.723Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [009: Decorators in TypeScript: How to Use Decorators to Add Functionality to Your Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/009-decorators-in-typescript-how-to-use-decorators-to-add-functionality-to-your-code)
{.links-list}



TypeScript의 데코레이터: 데코레이터를 사용하여 코드에 기능을 추가하는 방법

TypeScript 개발자라면 데코레이터에 대해 들어봤을 것입니다. 데코레이터는 원래 코드를 수정하지 않고 코드에 기능을 추가할 수 있는 강력한 기능입니다. 이 게시물에서는 데코레이터가 무엇인지, 어떻게 사용하는지, 몇 가지 실용적인 예를 살펴보겠습니다.

### 데코레이터란?

데코레이터는 런타임에 개체나 함수에 기능을 추가할 수 있게 해주는 디자인 패턴입니다. Java의 주석 및 C# 의 속성과 유사합니다. 데코레이터는 TypeScript에서 사용할 수 있는 언어 기능이며 ECMAScript에도 제안되고 있습니다.

TypeScript에서 데코레이터는 클래스, 메서드, 속성 및 매개 변수에 적용할 수 있는 함수입니다. 데코레이터가 클래스에 적용되면 클래스의 생성자 함수를 유일한 인수로 받습니다. 데코레이터가 메서드, 속성 또는 매개 변수에 적용될 때 대상 개체, 메서드 이름, 속성 또는 매개 변수, 선택적으로 메서드, 속성 또는 매개 변수의 설명자를 받습니다.

### 데코레이터를 사용하는 방법?

TypeScript에서 데코레이터를 사용하려면 `tsconfig.json` 파일에서 `experimentalDecorators` 플래그를 활성화해야 합니다. 예를 들면 다음과 같습니다.

```json
{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}
```

`experimentalDecorators` 플래그를 활성화하면 코드에서 데코레이터를 사용할 수 있습니다.

### 실용적인 예

#### 클래스 데코레이터

클래스 데코레이터의 예부터 시작하겠습니다. 클래스 `Person`이 있다고 가정합니다.

```typescript
class Person {
  constructor(public name: string) {}
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

이 클래스에 클래스 이름을 기록하는 데코레이터를 추가할 수 있습니다.

```typescript
function logName(constructor: Function) {
  console.log(`Class name: ${constructor.name}`);
}

@logName
class Person {
  constructor(public name: string) {}
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

`Person` 클래스의 인스턴스를 생성하면 콘솔에 다음과 같은 출력이 표시됩니다.

```
Class name: Person
```

#### 메서드 데코레이터

이제 메서드 데코레이터의 예를 살펴보겠습니다. 클래스 `Calculator`가 있다고 가정합니다.

```typescript
class Calculator {
  add(a: number, b: number) {
    return a + b;
  }
}
```

메서드의 인수와 반환 값을 기록하는 `add` 메서드에 데코레이터를 추가할 수 있습니다.

```typescript
function logMethod(target: any, methodName: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;
  descriptor.value = function(...args: any[]) {
    const result = originalMethod.apply(this, args);
    console.log(`Method ${methodName} called with arguments ${JSON.stringify(args)} and returned ${result}`);
    return result;
  }
  return descriptor;
}

class Calculator {
  @logMethod
  add(a: number, b: number) {
    return a + b;
  }
}
```

`add` 메서드를 호출하면 콘솔에 다음과 같은 출력이 표시됩니다.

```
Method add called with arguments [1,2] and returned 3
```

#### 속성 데코레이터

마지막으로 속성 데코레이터의 예를 살펴보겠습니다. 클래스 `Person`이 있다고 가정합니다.

```typescript
class Person {
  @readonly
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

읽기 전용으로 만드는 데코레이터를 `name` 속성에 추가할 수 있습니다.

```typescript
function readonly(target: any, propertyName: string) {
  Object.defineProperty(target, propertyName, {
    writable: false
  });
}

class Person {
  @readonly
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

`name` 속성을 수정하려고 하면 런타임 오류가 발생합니다.

```typescript
const person = new Person('Alice');
person.name = 'Bob'; // runtime error: Cannot assign to read only property 'name' of object '#<Person>'
```

### 결론

데코레이터는 깔끔하고 모듈화된 방식으로 코드에 기능을 추가하는 데 도움이 되는 강력한 기능입니다. 이 게시물에서는 데코레이터가 무엇인지, 어떻게 사용하는지, 몇 가지 실용적인 예를 살펴보았습니다. 자세한 내용을 알아보려면 아래 외부 리소스를 확인하십시오.

### 외부 리소스

- [TypeScript 핸드북: 데코레이터](https://www.typescriptlang.org/docs/handbook/decorators.html)
- [ECMAScript 제안: 데코레이터](https://github.com/tc39/proposal-decorators)