---
title: 022: Nest.js에서 국제화 구현
description: 
published: true
date: 2023-02-15T03:32:43.672Z
tags: 
editor: markdown
dateCreated: 2023-02-15T03:32:36.011Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [022: Implementing internationalization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/022-implementing-internationalization-in-nest-js)
{.links-list}


# Nest.js에서 국제화 구현

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. JavaScript의 상위 집합인 TypeScript를 사용하고 객체 지향 프로그래밍, 기능적 프로그래밍 및 기능적 반응 프로그래밍의 요소를 결합합니다.

이 게시물에서는 Nest.js에서 국제화를 구현하는 방법을 살펴보겠습니다. 국제화는 여러 시장을 위한 제품, 응용 프로그램 또는 웹 사이트를 디자인하고 개발하는 과정입니다. Nest.js는 Nest.js 애플리케이션에 국제화를 쉽게 추가할 수 있는 i18n용 내장 모듈을 제공합니다.

## 시작하기

시작하기 전에 필요한 모든 것이 있는지 확인합시다. 먼저 @nestjs/i18n 모듈을 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install @nestjs/i18n
```

모듈이 설치되면 i18n에 대한 구성 파일을 만들어야 합니다. 이 파일을 i18n.options.ts라고 하고 Nest.js 프로젝트의 src 디렉토리로 이동합니다. 파일은 다음과 같아야 합니다.

```typescript
import {
  I18nModuleOptions,
  I18nCoreModule,
} from '@nestjs/i18n';

const i18nModuleOptions: I18nModuleOptions = {
  fallbacks: {
    'en-US': 'en',
  },
  defaultLocale: 'en',
  path: __dirname,
};

export { i18nModuleOptions };
```

이 파일에서는 영어를 기본 언어로 사용하도록 i18n 모듈을 구성하고 있습니다. 또한 src 디렉토리에서 언어 파일을 찾도록 모듈에 지시하고 있습니다.

## 언어 파일 생성

이제 i18n 구성 파일을 설정했으므로 언어 파일을 만들어야 합니다. 이 예에서는 두 개의 언어 파일을 생성합니다. 하나는 영어용이고 다른 하나는 스페인어용입니다. 이 파일을 각각 en.json 및 es.json이라고 합니다.

en.json 파일은 다음과 같아야 합니다.

```json
{
  "hello": "Hello, world!"
}
```

그리고 es.json 파일은 다음과 같아야 합니다.

```json
{
  "hello": "¡Hola, mundo!"
}
```

이 파일에는 "hello" 키에 대한 번역이 포함되어 있습니다. 파일 구조는 언어에 관계없이 동일합니다. 이는 i18n 모듈이 CommonJS 모듈 형식을 사용하기 때문입니다.

## Nest.js 애플리케이션에서 언어 파일 사용

이제 언어 파일이 설정되었으므로 Nest.js 애플리케이션에서 사용할 수 있습니다.

먼저 애플리케이션 모듈에서 I18nModule을 가져와야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```typescript
import { Module } from '@nestjs/common';
import { I18nModule } from '@nestjs/i18n';

@Module({
  imports: [
    I18nModule.forRoot(),
  ],
})
export class ApplicationModule {}
```

다음으로 번역 처리를 담당할 서비스를 만들어야 합니다. 이 서비스를 I18nService라고 합니다. 서비스는 다음과 같아야 합니다.

```typescript
import { Injectable } from '@nestjs/common';
import { I18nService as I18n } from '@nestjs/i18n';

@Injectable()
export class I18nService {
  constructor(private readonly i18n: I18n) {}

  translate(key: string, params?: any) {
    return this.i18n.translate(key, params);
  }
}
```

이 서비스에서는 @nestjs/i18n 모듈에서 I18nService를 주입합니다. 또한 번역 처리를 담당할 translate() 메서드도 만들고 있습니다.

이제 서비스가 설정되었으므로 컨트롤러에서 사용할 수 있습니다. 이 예에서는 사용자가 선호하는 언어로 인사말을 반환하는 간단한 컨트롤러를 만듭니다. 컨트롤러는 다음과 같아야 합니다.

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';
import { I18nService } from './i18n.service';

@Controller()
export class AppController {
  constructor(private readonly i18nService: I18nService) {}

  @Get()
  getHello(@Res() res: Response) {
    const message = this.i18nService.translate('hello');
    res.send(message);
  }
}
```

이 컨트롤러에서 우리는 I18nService를 주입하고 있습니다. 또한 사용자가 선호하는 언어로 인사말을 반환하는 getHello() 메서드를 만들고 있습니다.

## Nest.js 애플리케이션 테스트

이제 Nest.js 애플리케이션을 설정했으므로 모든 것이 예상대로 작동하는지 테스트해 보겠습니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm test
```

모든 것이 예상대로 작동하면 다음 출력이 표시됩니다.

```
> nestjs-i18n@0.0.1 test /Users/username/projects/nestjs-i18n
> jest

 PASS  src/app.controller.spec.ts
  AppController
    GET /
      ✓ should return "Hello, world!" (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.548s
Ran all test suites.
```

## 결론

이 게시물에서는 Nest.js에서 국제화를 구현하는 방법을 살펴보았습니다. 번역을 처리하기 위해 언어 파일과 서비스를 만들었습니다. 또한 사용자가 선호하는 언어로 인사말을 반환하는 컨트롤러도 만들었습니다.