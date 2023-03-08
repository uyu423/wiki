---
title: 032: TypeScript와 함께 Nest.js 사용하기
description: 
published: true
date: 2023-02-12T09:55:33.781Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:55:32.030Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [032: Using Nest.js with TypeScript***English** document is available*](/en/Knowledge-base/Nest-js/Learning/032-using-nest-js-with-typescript)
{.links-list}


# TypeScript와 함께 Nest.js 사용

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합인 TypeScript를 사용합니다.

이 게시물에서는 TypeScript와 함께 Nest.js를 사용하는 방법을 보여줍니다. Nest.js 프로젝트 설정, TypeScript 구성 및 간단한 컨트롤러 작성 단계를 살펴보겠습니다.

## Nest.js 프로젝트 설정

먼저 새로운 Nest.js 프로젝트를 생성해 보겠습니다. Nest CLI를 사용하여 프로젝트 스켈레톤을 생성합니다.

```
$ nest new project-name
```

그러면 다음 구조로 `project-name`이라는 새 디렉토리가 생성됩니다.

```
project-name
├── README.md
├── node_modules
├── package-lock.json
├── package.json
├── tsconfig.json
└── tslint.json
```

다음으로 프로젝트의 종속 항목을 설치해 보겠습니다.

```
$ cd project-name
$ npm install
```

## TypeScript 구성

Nest.js는 기본적으로 TypeScript를 사용하므로 별도로 설치할 필요가 없습니다. 그러나 구성해야 합니다.

`tsconfig.json`을 열고 다음 옵션을 추가합니다.

```js
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "strict": true
  }
}
```

이 옵션은 TypeScript 코드를 ES6로 컴파일하고 CommonJS 모듈 형식을 사용합니다. `outDir` 옵션은 컴파일된 JavaScript 파일의 출력 디렉토리를 지정합니다. 그리고 `strict` 옵션은 엄격한 유형 검사를 가능하게 합니다.

## 컨트롤러 작성

이제 프로젝트가 설정되었으므로 컨트롤러를 작성할 수 있습니다. 컨트롤러는 HTTP 요청 처리 및 응답 반환을 담당합니다.

`src/controllers/hello.controller.ts`라는 파일을 만들어 봅시다:

```ts
import { Controller, Get } from '@nestjs/common';

@Controller('hello')
export class HelloController {
  @Get()
  public async index(): Promise<string> {
    return 'Hello, world!';
  }
}
```

이 컨트롤러에는 문자열 `'Hello, world!'`를 반환하는 단일 `@Get` 경로가 있습니다.

이 컨트롤러를 Nest.js에 등록하려면 모듈을 만들어야 합니다. `src/modules/hello.module.ts`라는 파일을 만들어 봅시다:

```ts
import { Module } from '@nestjs/common';
import { HelloController } from '../controllers/hello.controller';

@Module({
  controllers: [HelloController]
})
export class HelloModule {}
```

이 모듈은 `HelloController`를 가져와 Nest.js에 등록합니다.

마지막으로 Nest.js에게 이 모듈을 사용하도록 지시해야 합니다. 이것을 `app.module.ts` 파일에 추가하면 됩니다:

```ts
import { Module } from '@nestjs/common';
import { HelloModule } from './modules/hello.module';

@Module({
  imports: [HelloModule]
})
export class AppModule {}
```

이제 컨트롤러가 등록되었으므로 Nest.js 서버를 시작할 수 있습니다.

```
$ npm start
```

그리고 브라우저에서 http://localhost:3000/hello를 엽니다. `'Hello, world!'`라는 문자열이 표시되어야 합니다.

## 결론

이 게시물에서는 TypeScript와 함께 Nest.js를 사용하는 방법을 보여주었습니다. Nest.js 프로젝트를 설정하고 TypeScript를 구성하고 간단한 컨트롤러를 작성했습니다.