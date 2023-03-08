---
title: 002: Nest.js용 개발 환경 설정
description: 
published: true
date: 2023-02-14T14:32:30.540Z
tags: 
editor: markdown
dateCreated: 2023-02-14T14:32:28.915Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [002: Setting up a development environment for Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/002-setting-up-a-development-environment-for-nest-js)
{.links-list}


# Nest.js 개발 환경 설정

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(https://www.typescriptlang.org/)로 구축되었으며 객체 지향 프로그래밍, 함수형 프로그래밍 및 반응형 프로그래밍의 요소를 결합합니다.

## 전제 조건

시작하기 전에 개발 시스템에 다음이 설치되어 있는지 확인하십시오.

* Node.js (https://nodejs.org/en/)
* 타입스크립트(https://www.typescriptlang.org/)
* Visual Studio Code와 같은 코드 편집기(https://code.visualstudio.com/)

## 새로운 Nest.js 프로젝트 생성

터미널을 열고 다음 명령을 실행하여 새 Nest.js 프로젝트를 만듭니다.

```
nest new <project name>
```

이렇게 하면 프로젝트 이름으로 새 디렉터리가 생성되고 기본 Nest.js 구조로 프로젝트가 초기화됩니다.

## Nest.js 서버 시작

새로 생성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 Nest.js 서버를 시작합니다.

```
npm run start
```

그러면 기본적으로 http://localhost:3000에서 Nest.js 서버가 시작됩니다. 'PORT' 환경 변수를 설정하여 포트 번호를 변경할 수 있습니다.

## 새 Nest.js 컨트롤러 만들기

이제 Nest.js 서버가 실행 중이므로 새 컨트롤러를 만들어 보겠습니다. 프로젝트 루트 디렉터리에서 `controllers`라는 새 디렉터리와 그 안에 `<controller name>.controller.ts`라는 새 파일을 만듭니다.

컨트롤러 파일은 다음과 같아야 합니다.

```typescript
import { Controller } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {}
```

`<컨트롤러 경로>`를 컨트롤러에 액세스할 수 있는 경로로 바꾸고 `<컨트롤러 이름>`을 컨트롤러 이름으로 바꿉니다.

## 새 Nest.js 경로 만들기

컨트롤러 파일 내에서 다음을 추가하여 새 경로를 만듭니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {

  @Get()
  getHello(): string {
    return 'Hello World!';
  }

}
```

`@Get()` 데코레이터는 `getHello()` 메서드를 GET 경로로 정의합니다. 각각 `@Post()`, `@Put()` 및 `@Delete()` 데코레이터를 사용하여 POST, PUT 및 DELETE 경로를 정의할 수도 있습니다.

## Nest.js 경로 테스트

웹 브라우저에서 http://localhost:3000/<controller path>를 열면 `Hello World!` 메시지가 표시됩니다.

## 결론

이 자습서에서는 Nest.js용 개발 환경을 설정하고 경로가 있는 새 Nest.js 컨트롤러를 만드는 방법을 배웠습니다.