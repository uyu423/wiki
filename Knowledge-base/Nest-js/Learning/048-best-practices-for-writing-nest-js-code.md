---
title: 048: Nest.js 코드 작성 모범 사례
description: 
published: true
date: 2023-02-03T07:23:45.132Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:23:43.456Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [048: Best practices for writing Nest.js code***English** document is available*](/en/Knowledge-base/Nest-js/Learning/048-best-practices-for-writing-nest-js-code)
{.links-list}


# 048: Nest.js 코드 작성 모범 사례

Nest.js는 Node.js 애플리케이션을 구축하기 위한 강력한 프레임워크입니다. Express.js 위에 구축되었으며 TypeScript를 사용하므로 체계적이고 유지 관리가 쉬운 코드를 쉽게 작성할 수 있습니다.

이 게시물에서는 Nest.js 코드 작성에 대한 몇 가지 모범 사례를 살펴보겠습니다.

## 올바른 코딩 스타일 사용

코드를 작성할 때 올바른 코딩 스타일을 사용하는 것이 중요합니다. 이렇게 하면 읽고 유지 관리하기 쉬운 코드를 작성하는 데 도움이 됩니다.

Nest.js 코드에 사용할 수 있는 몇 가지 다른 코딩 스타일이 있습니다. 가장 인기 있는 것은 에어비앤비 스타일 가이드입니다. 이 스타일 가이드는 Node.js 커뮤니티에서 널리 사용되며 많은 회사에서 채택되었습니다.

또 다른 인기 있는 스타일 가이드는 StandardJS 스타일 가이드입니다. 이 스타일 가이드는 에어비앤비 스타일 가이드보다 덜 독단적이며 어떤 스타일을 사용해야 할지 잘 모르겠다면 좋은 선택입니다.

## 타입스크립트 사용

Nest.js는 TypeScript로 작성되었으며 Nest.js 코드를 작성할 때 TypeScript를 사용하는 것이 좋습니다. TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다.

TypeScript는 읽고 유지 관리하기 쉬운 코드를 작성하는 좋은 방법입니다. 또한 코드의 오류를 방지하는 데 도움이 됩니다.

## 올바른 종속성 사용

Nest.js 코드를 작성할 때 올바른 종속성을 사용하는 것이 중요합니다. 사용할 수 있는 몇 가지 다른 유형의 종속성이 있습니다.

첫 번째 유형의 종속성은 Node.js 모듈입니다. 이들은 npm에 게시되고 npm install 명령을 사용하여 설치할 수 있는 모듈입니다.

두 번째 유형의 종속성은 TypeScript 정의 파일입니다. 이러한 파일은 TypeScript에 대한 유형 정보를 제공합니다. npm에 게시되지 않으며 수동으로 설치해야 합니다.

세 번째 유형의 종속성은 JavaScript 파일입니다. 이러한 파일은 npm에 게시되지 않으며 수동으로 설치해야 합니다.

## 올바른 프로젝트 구조 사용

Nest.js 코드를 작성할 때 올바른 프로젝트 구조를 사용하는 것이 중요합니다. Nest.js에 권장되는 프로젝트 구조는 다음과 같습니다.

```
- src
  - controllers
  - services
  - pipes
  - filters
  - interceptors
  - modules
  - middlewares
  - entities
  - dtos
  - providers
  - guards
  - exceptions
  - interceptors
  - main.ts
  - app.module.ts
```

## 올바른 이름 지정 규칙 사용

Nest.js 코드를 작성할 때 올바른 명명 규칙을 사용하는 것이 중요합니다. Nest.js에 권장되는 명명 규칙은 다음과 같습니다.

- 컨트롤러 이름은 *Controller.ts여야 합니다.
- 서비스 이름은 *Service.ts여야 합니다.
- 파이프 이름은 *Pipe.ts여야 합니다.
- 필터 이름은 *Filter.ts여야 합니다.
- 인터셉터의 이름은 *Interceptor.ts여야 합니다.
- 모듈 이름은 *Module.ts여야 합니다.
- 미들웨어의 이름은 *Middleware.ts여야 합니다.
- 엔터티의 이름은 *Entity.ts여야 합니다.
- Dtos의 이름은 *Dto.ts여야 합니다.
- 제공자의 이름은 *Provider.ts여야 합니다.
- 경비원의 이름은 *Guard.ts여야 합니다.
- 예외는 *Exception.ts로 이름을 지정해야 합니다.

## 올바른 코딩 패턴 사용

Nest.js 코드를 작성할 때 올바른 코딩 패턴을 사용하는 것이 중요합니다. Nest.js에 권장되는 코딩 패턴은 다음과 같습니다.

- 컨트롤러는 얇아야 합니다.
- 서비스가 두꺼워야 함
- 데이터 변환에는 파이프를 사용해야 합니다.
- 데이터 검증을 위해 필터를 사용해야 합니다.
- 로깅에는 인터셉터를 사용해야 합니다.
- 조직화를 위해 모듈을 사용해야 함
- 미들웨어는 인증에 사용되어야 합니다.
- 엔터티는 데이터 모델링에 사용되어야 합니다.
- 데이터 전송은 Dtos를 사용해야 합니다.
- 공급자는 종속성 주입에 사용되어야 합니다.
- Guards는 권한 부여에 사용되어야 합니다.
- 오류 처리를 위해 예외를 사용해야 합니다.

## 올바른 테스트 접근 방식 사용

Nest.js 코드를 작성할 때 올바른 테스트 접근 방식을 사용하는 것이 중요합니다. Nest.js에 권장되는 테스트 접근 방식은 다음과 같습니다.

- 작은 기능에 단위 테스트 사용
- 더 큰 기능에 대한 통합 테스트 사용
- 전체 애플리케이션에 종단 간 테스트 사용

## 올바른 도구 사용

Nest.js 코드를 작성할 때 올바른 도구를 사용하는 것이 중요합니다. Nest.js에 권장되는 도구는 다음과 같습니다.

- Visual Studio Code와 같은 코드 편집기 사용
- Gulp와 같은 빌드 도구 사용
- Jest와 같은 테스트 프레임워크 사용
- TSLint와 같은 린터 사용

## 올바른 문서 사용

Nest.js 코드를 작성할 때 올바른 문서를 사용하는 것이 중요합니다. Nest.js에 대한 권장 문서는 다음과 같습니다.

- JavaScript 문서에 JSDoc 사용
- TypeScript 문서에 TypeDoc 사용

## 결론

이 게시물에서는 Nest.js 코드 작성에 대한 몇 가지 모범 사례를 살펴보았습니다. 우리는 올바른 코딩 스타일을 사용하고, TypeScript를 사용하고, 올바른 종속성을 사용하고, 올바른 프로젝트 구조를 사용하고, 올바른 명명 규칙을 사용하고, 올바른 코딩 패턴을 사용하고, 올바른 테스트 접근 방식을 사용하고, 올바른 도구를 사용하는 것이 중요하다는 것을 확인했습니다. , 올바른 설명서를 사용하십시오.