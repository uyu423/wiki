---
title: 027: TypeScript의 네임스페이스 별칭: 별칭을 사용하여 네임스페이스를 참조하는 방법
description: 
published: true
date: 2023-03-05T02:32:25.463Z
tags: 
editor: markdown
dateCreated: 2023-03-05T02:32:24.102Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [027: Namespace Aliases in TypeScript: How to Use Aliases to Refer to Namespaces***English** document is available*](/en/Knowledge-base/TypeScript/Learning/027-namespace-aliases-in-typescript-how-to-use-aliases-to-refer-to-namespaces)
{.links-list}


TypeScript의 네임스페이스 별칭: 별칭을 사용하여 네임스페이스를 참조하는 방법

TypeScript는 개발자가 깨끗하고 유지 관리 가능한 코드를 작성하는 데 도움이 되는 많은 기능을 제공하는 언어입니다. 이러한 기능 중 하나는 개발자가 더 짧은 이름을 사용하여 네임스페이스를 참조할 수 있도록 하는 네임스페이스 별칭입니다. 이 게시물에서는 TypeScript에서 네임스페이스 별칭을 사용하는 방법을 살펴보겠습니다.

## TypeScript에서 네임스페이스란 무엇입니까?

네임스페이스 별칭에 대해 알아보기 전에 먼저 TypeScript에 어떤 네임스페이스가 있는지 이해해 봅시다. 네임스페이스는 코드를 논리적 그룹으로 구성하는 방법입니다. 모듈과 비슷하지만 계층 구조가 추가되었습니다. 네임스페이스는 중첩될 수 있으며 클래스, 인터페이스, 함수 및 기타 네임스페이스를 포함할 수 있습니다.

다음은 TypeScript에서 네임스페이스의 예입니다.

```typescript
namespace MyNamespace {
  export interface MyInterface {
    // interface definition
  }

  export class MyClass {
    // class definition
  }

  export function myFunction() {
    // function definition
  }
}
```

이 예제에서는 인터페이스, 클래스 및 함수를 포함하는 `MyNamespace`라는 네임스페이스를 정의합니다. 또한 `export` 키워드를 사용하여 네임스페이스 외부에서 이러한 멤버에 액세스할 수 있도록 합니다.

## 네임스페이스 별칭이란 무엇입니까?

네임스페이스 별칭을 사용하면 개발자가 더 짧은 이름을 사용하여 네임스페이스를 참조할 수 있습니다. 이는 네임스페이스 이름이 길거나 이름 충돌을 피하려는 경우에 유용할 수 있습니다.

다음은 네임스페이스 별칭을 사용하는 방법의 예입니다.

```typescript
namespace MyNamespace {
  export class MyClass {
    // class definition
  }
}

// Define a namespace alias
import MyAlias = MyNamespace;

// Use the namespace alias to refer to the namespace
const myObj = new MyAlias.MyClass();
```

이 예에서는 `MyClass`라는 클래스로 `MyNamespace`라는 네임스페이스를 정의합니다. 그런 다음 `MyNamespace`를 참조하는 `MyAlias`라는 네임스페이스 별칭을 정의합니다. 마지막으로 별칭을 사용하여 `MyClass` 인스턴스를 만듭니다.

## 네임스페이스 별칭 사용 방법

네임스페이스 별칭을 사용하는 것은 간단합니다. 따라야 할 단계는 다음과 같습니다.

1. 별칭을 지정할 네임스페이스를 정의합니다.
2. `import` 키워드와 `=` 연산자를 사용하여 네임스페이스 별칭을 정의합니다.
3. 별명을 사용하여 네임스페이스를 참조하십시오.

다음은 이러한 단계를 보여주는 예입니다.

```typescript
namespace MyNamespace {
  export class MyClass {
    // class definition
  }
}

// Define a namespace alias
import MyAlias = MyNamespace;

// Use the namespace alias to refer to the namespace
const myObj = new MyAlias.MyClass();
```

이 예에서는 `MyClass`라는 클래스로 `MyNamespace`라는 네임스페이스를 정의합니다. 그런 다음 `MyNamespace`를 참조하는 `MyAlias`라는 네임스페이스 별칭을 정의합니다. 마지막으로 별칭을 사용하여 `MyClass` 인스턴스를 만듭니다.

## 추가 정보

- 동일한 네임스페이스에 대해 여러 네임스페이스 별칭을 정의할 수 있습니다.
- 네임스페이스 별칭을 사용하여 중첩된 네임스페이스를 참조할 수 있습니다.
- 네임스페이스 별칭을 사용하여 일반적으로 사용되는 네임스페이스에 대해 더 짧은 이름을 만들 수 있습니다.

## 경고

- 네임스페이스 별칭을 사용할 때 이름 충돌이 발생하지 않도록 주의하십시오.
- 이름이 짧은 네임스페이스에 대해 네임스페이스 별칭을 생성하지 마십시오.

## 결론

네임스페이스 별칭은 개발자가 더 짧은 이름을 사용하여 네임스페이스를 참조할 수 있도록 하는 TypeScript의 유용한 기능입니다. 이렇게 하면 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만들 수 있습니다. 이 게시물에 설명된 단계를 따르면 오늘 TypeScript 프로젝트에서 네임스페이스 별칭을 사용할 수 있습니다.

## 더 읽을 거리

- [TypeScript 핸드북: 네임스페이스](https://www.typescriptlang.org/docs/handbook/namespaces.html)
- [TypeScript 핸드북: 모듈](https://www.typescriptlang.org/docs/handbook/modules.html)