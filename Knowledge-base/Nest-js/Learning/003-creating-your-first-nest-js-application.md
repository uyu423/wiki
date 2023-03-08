---
title: 003: 첫 번째 Nest.js 애플리케이션 만들기
description: 
published: true
date: 2023-02-14T15:34:15.028Z
tags: 
editor: markdown
dateCreated: 2023-02-14T15:34:13.183Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [003: Creating your first Nest.js application***English** document is available*](/en/Knowledge-base/Nest-js/Learning/003-creating-your-first-nest-js-application)
{.links-list}


# 첫 번째 Nest.js 애플리케이션 만들기

이 가이드는 첫 번째 Nest.js 애플리케이션을 만드는 단계를 안내합니다. Nest.js는 Node.js 애플리케이션을 구축하기 위한 프레임워크입니다. Express.js를 기반으로 하며 JavaScript의 상위 집합인 TypeScript를 사용합니다.

## 전제 조건

시작하기 전에 컴퓨터에 다음을 설치해야 합니다.

- Node.js
- npm
- 타입스크립트

## 시작하기

먼저 프로젝트의 새 디렉토리를 만듭니다. 그런 다음 다음 명령을 실행하여 프로젝트를 초기화합니다.

```
npm init
```

이렇게 하면 프로젝트 디렉토리에 `package.json` 파일이 생성됩니다. 다음으로 Nest.js 프레임워크를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install --save @nestjs/core
```

## 안녕하세요 세상

이제 Nest.js가 설치되었으므로 첫 번째 Nest.js 애플리케이션을 만들 수 있습니다. 프로젝트 디렉터리에 `app.ts`라는 새 파일을 만들고 다음 코드를 추가합니다.

```typescript
import { NestFactory } from '@nestjs/core';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

이 코드는 `@nestjs/core` 패키지에서 `NestFactory` 클래스를 가져오고 이를 사용하여 `AppModule` 클래스의 인스턴스를 만듭니다. `AppModule` 클래스는 Nest.js 모듈입니다. Nest.js 모듈은 코드를 구성하는 데 사용됩니다.

다음으로 코드는 `app` 개체에서 `listen()` 메서드를 호출합니다. 이렇게 하면 Nest.js 애플리케이션이 포트 3000에서 들어오는 HTTP 요청을 수신하기 시작합니다.

## 결론

이 가이드에서는 첫 번째 Nest.js 애플리케이션을 만들었습니다. 모듈 및 NestFactory 클래스와 같은 Nest.js의 일부 핵심 개념에 대해서도 배웠습니다.