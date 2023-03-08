---
title: 전체 스택 개발을 위해 Nest.js, Express.js 및 Next.js 결합
description: 
published: true
date: 2023-02-01T07:57:38.993Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:57:37.470Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Combining Nest.js, Express.js, and Next.js for Full-Stack Development***English** version of this document is available*](/en/Knowledge-base/TypeScript/combining-nest-js-express-js-and-next-js-for-full-stack-development)
{.links-list}


  ChatGPT는 개발자가 자연어 처리를 사용하여 챗봇을 만들 수 있는 플랫폼입니다.


# 전체 스택 개발을 위해 Nest.js, Express.js 및 Next.js 결합

Node.js의 등장으로 풀스택 JavaScript 개발이 등장했습니다. 이를 통해 단일 언어를 사용하여 응용 프로그램을 개발할 수 있어 개발 프로세스가 보다 효율적으로 이루어졌습니다. 이 기사에서는 Nest.js, Express.js 및 Next.js를 결합하여 전체 스택 JavaScript 애플리케이션을 만드는 방법을 살펴보겠습니다.

## Nest.js가 무엇인가요?

Nest.js는 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. Node.js 및 Express.js 위에 구축되었으며 TypeScript를 사용합니다. Nest.js는 서버 측 애플리케이션 구축에 탁월한 선택입니다. 사용하기 쉽고 많은 기능이 있습니다.

## Express.js가 무엇인가요?

Express.js는 Node.js용 웹 애플리케이션 프레임워크입니다. 가장 인기 있는 Node.js 프레임워크이며 Uber, Airbnb 및 Twitter와 같은 많은 회사에서 사용합니다. Express.js는 웹 애플리케이션 구축에 탁월한 선택입니다. 사용하기 쉽고 많은 기능이 있습니다.

## Next.js가 무엇인가요?

Next.js는 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. React 위에 구축되었으며 TypeScript를 사용합니다. Next.js는 서버 측 애플리케이션을 구축하기 위한 훌륭한 선택입니다. 사용하기 쉽고 많은 기능이 있습니다.

## Nest.js, Express.js 및 Next.js를 결합하는 방법은 무엇입니까?

Nest.js, Express.js 및 Next.js를 결합하는 두 가지 방법이 있습니다. 첫 번째 방법은 Nest.js 프레임워크를 사용하여 서버 측 애플리케이션을 빌드하는 것이고 두 번째 방법은 Next.js 프레임워크를 사용하여 서버 측 애플리케이션을 빌드하는 것입니다.

### Nest.js를 사용하여 서버 측 애플리케이션 구축

Nest.js를 사용하여 서버 측 애플리케이션을 빌드하려면 다음 종속 항목을 설치해야 합니다.

```
npm install --save @nestjs/core @nestjs/common express
```

그런 다음 `src` 디렉토리에 `main.ts`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```typescript
import { NestFactory } from '@nestjs/core';
import { ApplicationModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(ApplicationModule);
  await app.listen(3000);
}
bootstrap();
```

다음으로 `src` 디렉토리에 `app.module.ts`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class ApplicationModule {}
```

그런 다음 `src` 디렉토리에 `app.controller.ts`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
  @Get()
  root() {
    return 'Hello World!';
  }
}
```

마지막으로 `src` 디렉토리에 `app.service.ts`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

이제 다음 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

```
npm start
```

http://localhost:3000에서 애플리케이션에 액세스할 수 있습니다.

### Next.js를 사용하여 서버 측 애플리케이션 구축

Next.js를 사용하여 서버 측 애플리케이션을 빌드하려면 다음 종속 항목을 설치해야 합니다.

```
npm install --save next react react-dom
```

그런 다음 루트 디렉터리에 `next.config.js`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```javascript
module.exports = {
  target: 'serverless',
};
```

다음으로 `src` 디렉토리에 `pages/index.js`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```javascript
export default () => 'Hello World!';
```

이제 다음 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

```
npm run dev
```

http://localhost:3000에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 Nest.js, Express.js 및 Next.js를 결합하여 전체 스택 JavaScript 애플리케이션을 만드는 방법을 살펴보았습니다. 또한 Nest.js 및 Next.js를 사용하여 서버 측 애플리케이션을 빌드하는 방법도 살펴보았습니다.