---
title: 035: TypeScript의 네임스페이스 대 모듈: 차이점 이해 및 사용 시기
description: 
published: true
date: 2023-03-05T09:32:38.737Z
tags: 
editor: markdown
dateCreated: 2023-03-05T09:32:38.737Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [035: Namespaces vs. Modules in TypeScript: Understanding the Differences and When to Use Each***English** document is available*](/en/Knowledge-base/TypeScript/Learning/035-namespaces-vs-modules-in-typescript-understanding-the-differences-and-when-to-use-each)
{.links-list}



소개

TypeScript는 JavaScript로 컴파일하는 기능으로 잘 알려진 널리 사용되는 프로그래밍 언어입니다. 대규모 응용 프로그램을 구축하는 데 탁월한 선택이 되는 많은 기능이 있습니다. 이러한 기능 중 하나는 네임스페이스와 모듈을 사용하는 기능입니다. 이 게시물에서는 TypeScript에서 네임스페이스와 모듈의 차이점과 각각을 사용하는 경우를 살펴봅니다.

TypeScript의 네임스페이스

TypeScript의 네임스페이스는 관련 코드를 함께 그룹화하는 데 사용됩니다. 모듈과 유사하지만 같은 것은 아닙니다. 네임스페이스는 `namespace` 키워드를 사용하여 선언됩니다.

### 네임스페이스 선언

TypeScript에서 네임스페이스를 선언하려면 `namespace` 키워드 뒤에 네임스페이스 이름을 사용합니다. 다음은 예입니다.

```typescript
namespace MyNamespace {
  export function myFunction() {
    console.log("Hello from MyNamespace");
  }
}
```

이 예제에서는 `myFunction`이라는 함수를 포함하는 `MyNamespace`라는 네임스페이스를 선언했습니다. `export` 키워드는 네임스페이스 외부에서 함수를 사용할 수 있도록 하는 데 사용됩니다.

### 네임스페이스 사용

네임스페이스를 사용하려면 이름으로 참조하기만 하면 됩니다. 다음은 예입니다.

```typescript
MyNamespace.myFunction();
```

이 예에서는 `MyNamespace` 네임스페이스에 정의된 `myFunction` 함수를 호출합니다.

### 네임스페이스의 장점

네임스페이스는 코드를 논리 그룹으로 구성하는 데 유용할 수 있습니다. 또한 응용 프로그램의 서로 다른 부분 간의 이름 충돌을 방지하는 데 도움이 될 수 있습니다.

TypeScript의 모듈

TypeScript의 모듈은 코드를 캡슐화하고 이름 충돌을 방지하는 데 사용됩니다. 네임스페이스와 유사하지만 외부 코드와 함께 작동하도록 설계되었습니다. 모듈은 `module` 키워드를 사용하여 선언됩니다.

### 모듈 선언

TypeScript에서 모듈을 선언하려면 `module` 키워드 뒤에 모듈 이름을 사용합니다. 다음은 예입니다.

```typescript
module MyModule {
  export function myFunction() {
    console.log("Hello from MyModule");
  }
}
```

이 예제에서는 `myFunction`이라는 함수를 포함하는 `MyModule`이라는 모듈을 선언했습니다. `export` 키워드는 모듈 외부에서 함수를 사용할 수 있도록 하는 데 사용됩니다.

### 모듈 사용

모듈을 사용하려면 모듈을 코드로 가져와야 합니다. 다음은 예입니다.

```typescript
import { MyModule } from "./my-module";

MyModule.myFunction();
```

이 예에서는 `my-module.ts`라는 파일에서 `MyModule` 모듈을 가져옵니다. 그런 다음 `MyModule` 모듈에 정의된 `myFunction` 함수를 호출할 수 있습니다.

### 모듈의 장점

모듈은 코드를 캡슐화하고 명명 충돌을 방지하는 데 유용할 수 있습니다. 또한 대규모 응용 프로그램을 더 작고 관리하기 쉬운 조각으로 나누는 데 사용할 수 있습니다.

### 네임스페이스와 모듈의 차이점

네임스페이스와 모듈의 주요 차이점은 네임스페이스는 내부 코드와 함께 작동하도록 설계된 반면 모듈은 외부 코드와 함께 작동하도록 설계되었다는 것입니다. 네임스페이스는 코드를 논리 그룹으로 구성하고 애플리케이션 내에서 이름 충돌을 방지하는 데 유용합니다. 모듈은 코드를 캡슐화하고 응용 프로그램의 다른 부분 간의 이름 충돌을 방지하는 데 유용합니다.

### 네임스페이스를 사용하는 경우

네임스페이스는 코드를 논리적 그룹으로 구성하고 애플리케이션 내에서 이름 충돌을 방지해야 할 때 유용합니다. 외부 애플리케이션에서 사용하지 않을 내부 코드로 작업해야 할 때도 유용합니다.

### 모듈을 사용하는 경우

모듈은 코드를 캡슐화하고 응용 프로그램의 다른 부분 간의 이름 충돌을 방지해야 할 때 유용합니다. 다른 응용 프로그램에서 사용할 외부 코드로 작업해야 할 때도 유용합니다.

### 추가 정보

TypeScript에서 네임스페이스와 모듈을 사용할 때 작업에 적합한 도구를 선택하는 것이 중요합니다. 내부 코드로 작업해야 하는 경우 네임스페이스를 선택하는 것이 좋습니다. 외부 코드로 작업해야 하는 경우 모듈이 더 나은 선택입니다.

### 경고

네임스페이스나 모듈을 너무 많이 사용하면 코드를 관리하기 어려울 수 있습니다. 필요한 경우에만 아껴서 사용하는 것이 중요합니다.

### 위험

네임스페이스 또는 모듈을 잘못 사용하면 이름 충돌 및 기타 문제가 발생할 수 있습니다. 코드에서 사용하기 전에 작동 방식을 이해하는 것이 중요합니다.

결론

이 게시물에서는 TypeScript에서 네임스페이스와 모듈의 차이점과 각각을 사용하는 경우를 살펴보았습니다. 네임스페이스는 코드를 논리적 그룹으로 구성하고 응용 프로그램 내에서 이름 충돌을 방지하는 데 유용하고 모듈은 코드를 캡슐화하고 응용 프로그램의 다른 부분 간의 이름 충돌을 방지하는 데 유용합니다. 작업에 적합한 도구를 선택하면 관리하기 쉬운 깨끗하고 유지 관리 가능한 코드를 작성할 수 있습니다.

외부 자원

- [TypeScript 문서: 네임스페이스](https://www.typescriptlang.org/docs/handbook/namespaces.html)
- [TypeScript 문서: 모듈](https://www.typescriptlang.org/docs/handbook/modules.html)