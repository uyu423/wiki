---
title: 005: Nest.js의 라우팅 및 컨트롤러
description: 
published: true
date: 2023-02-14T16:32:32.708Z
tags: 
editor: markdown
dateCreated: 2023-02-14T16:32:24.568Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [005: Routing and controllers in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/005-routing-and-controllers-in-nest-js)
{.links-list}


# 소개

Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. Express.js를 기반으로 하며 언어에 정적 타이핑을 추가하는 JavaScript의 상위 집합인 TypeScript를 사용합니다.

Nest.js는 비교적 새로운 프레임워크이므로 Express.js만큼 많은 문서나 커뮤니티 지원이 없습니다. 그러나 인기가 높아지고 있으며 Microsoft, Google 및 Amazon과 같은 회사에서 사용하고 있습니다.

이 게시물에서는 Nest.js에서 라우팅 및 컨트롤러를 설정하는 방법을 살펴보겠습니다. 또한 Express.js보다 Nest.js를 사용할 때의 몇 가지 이점에 대해서도 살펴보겠습니다.

# Nest.js에서 라우팅 및 컨트롤러 설정

가장 먼저 해야 할 일은 Nest.js 프레임워크를 설치하는 것입니다. Node.js 패키지 관리자인 npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install --save @nestjs/common
```

Nest.js가 설치되면 프로젝트에 `app.controller.ts`라는 새 파일을 만들 수 있습니다. 이 파일에는 컨트롤러 로직이 포함됩니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/')
export class AppController {
  @Get()
  root() {
    return 'Hello, world!';
  }
}
```

위의 코드에서 `@nestjs/common`에서 `Controller` 및 `Get` 데코레이터를 가져왔습니다. 그런 다음 `/` 경로에 새 컨트롤러를 생성하기 위해 `@Controller` 데코레이터를 사용했습니다.

마지막으로 새로운 `root` 메서드를 만들고 `@Get` 데코레이터로 장식했습니다. 이 메서드는 `/` 경로에 대한 GET 요청이 있을 때 호출됩니다.

이제 `main.ts`라는 새 파일을 만들 수 있습니다. 이 파일은 Nest.js 애플리케이션을 시작하는 데 사용됩니다.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

위의 코드에서는 `@nestjs/core`에서 `NestFactory` 및 `AppModule`을 가져왔습니다. 그런 다음 `NestFactory`를 사용하여 새로운 Nest.js 애플리케이션을 만들고 `AppModule`을 전달했습니다.

마지막으로 `listen` 메서드를 호출하여 포트 3000에서 애플리케이션을 시작했습니다.

이제 `node main.ts`를 사용하여 애플리케이션을 실행하면 다음 출력이 표시됩니다.

```
$ node main.ts
[Nest] 7100   - 2020-03-22 10:54:54   [NestFactory] Starting Nest application...
[Nest] 7100   - 2020-03-22 10:54:54   [InstanceLoader] AppModule dependencies initialized +0ms
[Nest] 7100   - 2020-03-22 10:54:54   [RouterExplorer] Mapped {,GET} route +2ms
[Nest] 7100   - 2020-03-22 10:54:54   [NestApplication] Nest application successfully started +2ms
```

이제 브라우저를 열고 `http://localhost:3000/`으로 이동하면 다음과 같은 결과가 표시됩니다.

```
Hello, world!
```

# 결론

이 게시물에서는 Nest.js에서 라우팅 및 컨트롤러를 설정하는 방법을 살펴보았습니다. 또한 Express.js보다 Nest.js를 사용할 때의 몇 가지 이점에 대해서도 살펴보았습니다.

TypeScript를 사용하는 Node.js 프레임워크를 찾고 있다면 Nest.js를 고려해 볼 가치가 있습니다.