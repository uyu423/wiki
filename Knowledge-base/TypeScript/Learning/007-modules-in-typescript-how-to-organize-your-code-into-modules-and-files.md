---
title: 007: TypeScript의 모듈: 코드를 모듈과 파일로 구성하는 방법
description: 
published: true
date: 2023-03-05T05:32:27.982Z
tags: 
editor: markdown
dateCreated: 2023-03-05T05:32:27.982Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [007: Modules in TypeScript: How to Organize Your Code into Modules and Files***English** document is available*](/en/Knowledge-base/TypeScript/Learning/007-modules-in-typescript-how-to-organize-your-code-into-modules-and-files)
{.links-list}


TypeScript의 모듈: 코드를 모듈과 파일로 구성하는 방법

모든 코드를 단일 파일에 저장하는 데 지치셨습니까? 더 작고 관리하기 쉬운 조각으로 정리하고 싶습니까? TypeScript의 모듈만 보세요! 이 게시물에서는 모듈이 무엇인지, 모듈을 사용하는 방법 및 코드를 파일로 구성하는 방법을 살펴보겠습니다.

## 모듈이란 무엇입니까?

모듈은 코드를 재사용 가능한 별도의 구성 요소로 구성하는 방법입니다. 이를 통해 코드를 더 작은 조각으로 나눌 수 있으므로 관리 및 유지 관리가 더 쉬워집니다. TypeScript에서 모듈은 `export` 키워드를 사용하여 정의됩니다.

### 모듈 내보내기

모듈을 내보내려면 모듈 앞에 `export` 키워드를 붙이기만 하면 됩니다. 예를 들어, 두 개의 숫자를 더하는 함수를 포함하는 `math.ts`라는 모듈이 있다고 가정해 보겠습니다.

```typescript
export function add(a: number, b: number): number {
  return a + b;
}
```

그런 다음 `import` 키워드를 사용하여 이 모듈을 다른 파일로 가져올 수 있습니다.

```typescript
import { add } from './math';
```

### 기본 내보내기

명명된 내보내기 외에도 TypeScript는 기본 내보내기도 지원합니다. 기본 내보내기는 모듈의 "기본" 내보내기인 단일 내보내기입니다. 예를 들어 기본 함수를 내보내는 `foo.ts`라는 모듈이 있다고 가정해 보겠습니다.

```typescript
export default function() {
  console.log('Hello, world!');
}
```

그런 다음 이름을 지정할 필요 없이 `import` 키워드를 사용하여 이 모듈을 다른 파일로 가져올 수 있습니다.

```typescript
import foo from './foo';
```

### 모듈 다시 내보내기

때로는 다른 모듈에서 모듈을 다시 내보낼 수 있습니다. 이는 모듈에 대한 "공용 API"를 만드는 데 유용할 수 있습니다. 모듈을 다시 내보내려면 `*` 기호와 함께 `export` 키워드를 사용할 수 있습니다.

```typescript
export * from './math';
```

이것은 `math` 모듈에서 명명된 모든 내보내기를 내보냅니다.

## 코드를 파일로 정리하기

이제 모듈을 내보내는 방법을 알았으니 코드를 파일로 구성하는 방법에 대해 이야기해 보겠습니다. 일반적으로 기능에 따라 코드를 파일로 구성하는 것을 목표로 해야 합니다. 예를 들어 사용자 인증을 처리하는 모듈이 있는 경우 이를 `auth.ts`라는 파일에 넣을 수 있습니다.

### 파일 명명 규칙

코드를 파일로 구성할 때 코드를 쉽게 찾고 관리할 수 있도록 몇 가지 명명 규칙을 따르는 것이 중요합니다. 다음은 몇 가지 일반적인 명명 규칙입니다.

- 소문자 파일 이름을 사용하십시오.
- 하이픈을 사용하여 파일 이름에서 단어를 구분합니다(예: `user-authentication.ts`).
- 모듈의 목적을 반영하는 설명이 포함된 이름을 사용하십시오.

### 폴더 구조

명명 규칙 외에도 코드의 폴더 구조도 고려해야 합니다. 다음은 코드를 폴더로 구성하기 위한 몇 가지 팁입니다.

- 응용 프로그램의 각 주요 기능 또는 구성 요소에 대해 별도의 폴더를 사용하십시오.
- 하위 폴더를 사용하여 관련 모듈을 구성합니다.
- 폴더를 너무 깊게 중첩하지 마십시오.

다음은 간단한 웹 애플리케이션의 폴더 구조 예입니다.

```
src/
  index.ts
  app/
    app.ts
    routes.ts
    components/
      header.ts
      footer.ts
    auth/
      auth.ts
      login.ts
      register.ts
  utils/
    math.ts
```

## 결론

모듈은 코드를 재사용 가능한 구성 요소로 구성하는 강력한 도구입니다. 모듈을 사용하면 코드를 더 작고 관리하기 쉬운 조각으로 나눌 수 있으므로 유지 관리 및 확장이 더 쉬워집니다. 이름 지정 규칙을 따르고 코드를 파일로 구성할 때 폴더 구조를 고려해야 합니다.

### 추가 정보

- 모듈에 대한 TypeScript 문서: https://www.typescriptlang.org/docs/handbook/modules.html

### 외부 리소스

- Tyler McGinnis의 "모듈로 React 코드베이스 구성": https://ui.dev/organizing-your-react-codebase-with-es6-modules/
- Jonathan Saring의 "모듈형 JavaScript: 모듈 초보자 가이드": https://www.sitepoint.com/javascript-modules-beginners-guide/