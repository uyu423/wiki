---
title: 023: JavaScript와 TypeScript 혼합: TypeScript를 기존 JavaScript 코드와 함께 사용하는 방법
description: 
published: true
date: 2023-03-07T18:32:38.390Z
tags: 
editor: markdown
dateCreated: 2023-03-07T18:32:38.390Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [023: Mixing JavaScript and TypeScript: How to Use TypeScript with Existing JavaScript Code***English** document is available*](/en/Knowledge-base/TypeScript/Learning/023-mixing-javascript-and-typescript-how-to-use-typescript-with-existing-javascript-code)
{.links-list}



JavaScript와 TypeScript 혼합: TypeScript를 기존 JavaScript 코드와 함께 사용하는 방법

TypeScript는 정적 타이핑, 클래스, 인터페이스 및 기타 기능을 JavaScript에 추가하는 JavaScript의 상위 집합입니다. 더 나은 코드 유지 관리 및 확장성을 제공하므로 대규모 응용 프로그램 개발에 널리 사용됩니다. 그러나 많은 기존 JavaScript 프로젝트는 TypeScript를 염두에 두고 개발되지 않았을 수 있습니다. 이 게시물에서는 기존 JavaScript 코드와 함께 TypeScript를 사용하는 방법을 살펴보겠습니다.

## 기존 JavaScript 코드와 함께 TypeScript를 사용하는 이유는 무엇입니까?

기존 JavaScript 코드와 함께 TypeScript를 사용하려는 몇 가지 이유가 있습니다.

- **유형 안전성**: TypeScript는 런타임이 아닌 컴파일 시간에 오류를 포착하는 데 도움이 되는 정적 유형 지정을 제공합니다. 이렇게 하면 코드 품질이 향상되고 버그 가능성이 줄어듭니다.

- **개선된 코드 유지 관리**: TypeScript는 코드를 구성하고 구성하기 위한 도구를 제공하여 이해하고 유지 관리하기가 더 쉽습니다.

- **확장성**: TypeScript는 객체 지향 프로그래밍 원칙을 지원하여 대규모 애플리케이션을 보다 쉽게 구축할 수 있습니다.

## TypeScript 프로젝트 설정

기존 JavaScript 코드로 TypeScript를 사용하려면 먼저 TypeScript 프로젝트를 설정해야 합니다. 다음 단계를 사용하여 이를 수행할 수 있습니다.

1. npm을 사용하여 TypeScript를 설치합니다.

```npm install -g typescript```

2. Create a new folder for our project:

```mkdir my-project```

3. 프로젝트 폴더로 이동합니다.

```cd my-project```

4. Initialize a new TypeScript project:

```tsc --초기화```

이렇게 하면 TypeScript 프로젝트를 구성하는 데 사용할 수 있는 프로젝트 폴더에 `tsconfig.json` 파일이 생성됩니다.

## 기존 JavaScript 코드와 함께 TypeScript 사용

TypeScript 프로젝트를 설정하면 기존 JavaScript 코드와 함께 TypeScript를 사용할 수 있습니다. 이를 수행하는 방법에는 여러 가지가 있습니다.

### 1. `.js` 파일 이름을 `.ts`로 변경

기존 JavaScript 코드와 함께 TypeScript를 사용하는 한 가지 방법은 단순히 `.js` 파일의 이름을 `.ts` 파일로 바꾸는 것입니다. 이를 통해 기존 코드에서 정적 타이핑과 같은 TypeScript 기능을 사용할 수 있습니다.

그러나 이 방법에는 몇 가지 제한 사항이 있습니다. 예를 들어 TypeScript는 우리가 사용 중인 외부 종속성에 대한 유형을 유추할 수 없으므로 이러한 종속성에 대한 유형 정의를 수동으로 추가해야 합니다.

### 2. 유형 선언 사용

기존 JavaScript 코드와 함께 TypeScript를 사용하는 또 다른 방법은 유형 선언을 사용하는 것입니다. 유형 선언은 외부 JavaScript 라이브러리 및 API의 유형을 설명하는 파일입니다.

npm을 사용하여 유형 선언을 설치할 수 있습니다.

```npm install @types/library-name```

For example, if we want to use type declarations for the jQuery library, we can install them using:

```npm install @types/jquery```

유형 선언을 설치하고 나면 외부 라이브러리와 함께 TypeScript를 사용할 수 있습니다.

### 3. JSDoc 주석 사용

JSDoc 주석은 JavaScript 코드에 유형 정보를 추가하는 방법입니다. JSDoc 주석을 사용하여 기존 JavaScript 코드에 유형 정보를 추가하여 TypeScript 기능을 사용할 수 있습니다.

예를 들어 다음 함수에 JSDoc 주석을 추가하여 매개변수 유형과 반환 값을 지정할 수 있습니다.

```javascript
/**
 * Adds two numbers together.
 * @param {number} x - The first number.
 * @param {number} y - The second number.
 * @returns {number} The sum of x and y.
 */
function add(x, y) {
  return x + y;
}
```

코드에 JSDoc 주석을 추가하면 정적 타이핑과 같은 TypeScript 기능을 사용할 수 있습니다.

## 결론

기존 JavaScript 코드와 함께 TypeScript를 사용하면 코드 품질, 유지 관리성 및 확장성을 개선하는 데 도움이 될 수 있습니다. `.js` 파일의 이름을 `.ts`로 바꾸거나 유형 선언을 사용하거나 JSDoc 주석을 추가하여 기존 JavaScript 코드와 함께 TypeScript를 사용할 수 있습니다. 다음 단계를 따르면 기존 JavaScript 프로젝트에서 TypeScript 기능을 활용할 수 있습니다.

## 추가 정보

- TypeScript 핸드북: https://www.typescriptlang.org/docs/handbook/intro.html

## 경고

- JavaScript 코드가 TypeScript에서 지원하지 않는 기능을 사용하는 경우 `.js` 파일의 이름을 `.ts` 파일로 변경하면 일부 오류가 발생할 수 있습니다.

## 위험

- 유형 선언이 항상 최신이거나 정확하지 않을 수 있으므로 코드에 오류가 발생할 수 있습니다. 프로젝트에서 유형 선언을 사용하기 전에 유형 선언의 품질을 확인하는 것이 중요합니다.

## 더 읽을거리

- "JavaScript에서 TypeScript로 변환 가이드": https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html
- "TypeScript 대 JavaScript: 프로젝트를 마이그레이션해야 합니까?": https://www.altar.io/blog/typescript-vs-javascript-should-you-migrate-your-project