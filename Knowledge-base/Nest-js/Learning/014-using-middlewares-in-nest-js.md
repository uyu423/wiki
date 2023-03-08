---
title: 014: Nest.js에서 미들웨어 사용하기
description: 
published: true
date: 2023-02-15T00:32:32.946Z
tags: 
editor: markdown
dateCreated: 2023-02-15T00:32:25.391Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [014: Using middlewares in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/014-using-middlewares-in-nest-js)
{.links-list}


# Nest.js에서 미들웨어 사용

Nest.js는 확장 가능한 서버 측 애플리케이션을 만드는 데 도움이 되는 Node.js용 웹 프레임워크입니다. 이 게시물에서는 Nest.js에서 미들웨어를 사용하는 방법을 살펴보겠습니다.

미들웨어는 들어오는 요청이 수신될 때 Nest.js에 의해 호출되는 기능입니다. 로깅, 유효성 검사 및 인증과 같은 작업을 수행하는 데 사용할 수 있습니다.

Nest.js에는 자체 미들웨어를 쉽게 생성할 수 있는 내장형 미들웨어 팩토리가 함께 제공됩니다. 미들웨어를 생성하려면 `NestMiddleware` 인터페이스를 구현하는 클래스를 생성해야 합니다. 이 인터페이스는 `req` 및 `res` 객체를 매개변수로 사용하는 `use()` 메서드를 정의합니다.

다음은 들어오는 요청을 기록하는 미들웨어의 간단한 예입니다.

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: any, res: any, next: () => void) {
    console.log(`Incoming request at ${req.url}`);
    next();
  }
}
```

이 미들웨어를 사용하려면 Nest.js에 등록해야 합니다. 이는 `app.module.ts` 파일에서 수행할 수 있습니다.

```typescript
import { Module } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';

@Module({
  providers: [LoggerMiddleware],
})
export class AppModule {}
```

미들웨어가 등록되면 Nest.js는 들어오는 요청을 받을 때마다 미들웨어를 호출합니다.

미들웨어를 사용하여 유효성 검사 및 인증과 같은 작업을 수행할 수도 있습니다. 예를 들어 들어오는 요청이 인증되었는지 확인하는 미들웨어를 만들 수 있습니다.

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class AuthMiddleware implements NestMiddleware {
  use(req: any, res: any, next: () => void) {
    if (!req.isAuthenticated()) {
      res.status(401).send('You are not authenticated');
    } else {
      next();
    }
  }
}
```

이 미들웨어는 들어오는 요청이 인증되었는지 확인합니다. 그렇지 않은 경우 '401 Unauthorized' 상태 코드를 반환합니다. 그렇지 않으면 체인의 다음 미들웨어를 호출합니다.

미들웨어를 서로 연결하여 들어오는 각 요청에 대해 실행되는 일련의 작업을 생성할 수 있습니다. 예를 들어 요청을 기록하고 요청의 유효성을 검사한 다음 요청을 인증하는 체인을 만들 수 있습니다.

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';
import { AuthMiddleware } from './auth.middleware';

@Module({
  providers: [
    LoggerMiddleware,
    AuthMiddleware,
  ],
})
export class AppModule {}
```

이 예에서는 `LoggerMiddleware`가 먼저 호출된 다음 `AuthMiddleware`가 호출됩니다.

미들웨어를 사용하여 다양한 작업을 수행할 수 있습니다. Nest.js의 기능을 확장하는 데 사용할 수 있는 강력한 도구입니다.