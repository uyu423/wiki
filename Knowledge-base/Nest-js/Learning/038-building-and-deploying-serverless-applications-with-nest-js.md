---
title: 038: Nest.js로 서버리스 애플리케이션 구축 및 배포
description: 
published: true
date: 2023-02-12T14:18:02.637Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:17:55.772Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [038: Building and deploying serverless applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/038-building-and-deploying-serverless-applications-with-nest-js)
{.links-list}


# 038: Nest.js로 서버리스 애플리케이션 구축 및 배포

이 게시물에서는 Nest.js를 사용하여 서버리스 애플리케이션을 구축하고 배포하는 방법을 알아봅니다.

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(강력한 타이핑 제공)로 구축되었으며 객체 지향 프로그래밍, 함수형 프로그래밍 및 반응형 프로그래밍의 요소를 결합합니다.

Nest.js는 서버리스 애플리케이션 구축에 탁월한 선택입니다. 가볍고 빠르며 TypeScript 지원, 사용하기 쉬운 종속성 주입 시스템 및 강력한 모듈 시스템과 같은 다양한 기능을 제공합니다.

Nest.js로 서버리스 애플리케이션을 빠르고 쉽게 구축할 수 있습니다. 이 게시물에서는 간단한 서버리스 Nest.js 애플리케이션을 생성하고 이를 AWS Lambda에 배포하는 단계를 안내합니다.

## Nest.js 애플리케이션 만들기

먼저 새로운 Nest.js 애플리케이션을 생성해야 합니다. Nest CLI를 사용하여 새 프로젝트를 생성할 수 있습니다.

```
nest new serverless-app
```

이렇게 하면 Nest.js 애플리케이션에 필요한 기본 파일과 폴더가 있는 `serverless-app`이라는 새 폴더가 생성됩니다.

다음으로 `@nestjs/serverless` 패키지를 설치해야 합니다. 이 패키지는 서버리스 Nest.js 애플리케이션을 구축하는 데 필요한 모듈과 종속성을 제공합니다.

```
npm install --save @nestjs/serverless
```

이제 `@nestjs/serverless` 패키지가 설치되었으므로 새로운 서버리스 Nest.js 애플리케이션을 만들 수 있습니다.

먼저 `src` 폴더에 `main.ts`라는 새 파일을 생성합니다. 이 파일은 서버리스 Nest.js 애플리케이션의 진입점이 됩니다.

`main.ts`에서 `@nestjs/core` 패키지의 `NestFactory` 클래스를 가져와야 합니다. 이 클래스는 새로운 Nest.js 애플리케이션을 만드는 데 사용됩니다.

```typescript
import { NestFactory } from '@nestjs/core';
```

다음으로 `@nestjs/serverless` 패키지에서 `ServerlessApplicationModule`을 가져와야 합니다. 이 모듈은 Nest.js 애플리케이션을 부트스트랩하는 데 사용됩니다.

```typescript
import { ServerlessApplicationModule } from '@nestjs/serverless';
```

이제 `NestFactory` 및 `ServerlessApplicationModule` 클래스를 가져왔으므로 이를 사용하여 새 Nest.js 애플리케이션을 만들 수 있습니다.

```typescript
async function bootstrap() {
  const app = await NestFactory.create(ServerlessApplicationModule);
  await app.listen(3000);
}
bootstrap();
```

위의 코드에서 우리는 `NestFactory` 클래스를 사용하여 새로운 Nest.js 애플리케이션을 만듭니다. 애플리케이션을 부트스트랩하기 위해 `ServerlessApplicationModule`을 `create` 메서드에 전달하고 있습니다.

마지막으로 `listen` 메서드를 사용하여 포트 3000에서 애플리케이션을 시작합니다.

## 컨트롤러 만들기

이제 Nest.js 애플리케이션이 생성되었으므로 컨트롤러를 생성해 보겠습니다. 컨트롤러는 들어오는 HTTP 요청을 처리하고 응답을 반환하는 역할을 합니다.

Nest.js에서 컨트롤러는 클래스로 생성됩니다. `src/controllers` 폴더에 `hello.controller.ts`라는 새 파일을 만들어 봅시다.

`hello.controller.ts`에서 `@nestjs/common` 패키지의 `Controller` 데코레이터를 가져와야 합니다. 이 데코레이터는 클래스를 컨트롤러로 표시하는 데 사용됩니다.

```typescript
import { Controller } from '@nestjs/common';
```

다음으로 `@nestjs/common` 패키지에서 `Get` 데코레이터를 가져와야 합니다. 이 데코레이터는 컨트롤러 메서드를 HTTP `GET` 요청에 대한 핸들러로 표시하는 데 사용됩니다.

```typescript
import { Get } from '@nestjs/common';
```

이제 `Controller` 및 `Get` 데코레이터를 가져왔으므로 이를 사용하여 컨트롤러를 만들 수 있습니다.

```typescript
@Controller('hello')
export class HelloController {
  @Get()
  hello() {
    return 'Hello, world!';
  }
}
```

위의 코드에서 `HelloController`라는 컨트롤러를 만들었습니다. 이 컨트롤러에는 문자열 `Hello, world!`를 반환하는 `hello`라는 메서드가 하나 있습니다.

또한 `Controller` 데코레이터를 사용하여 이 컨트롤러의 경로를 지정했습니다. 이 경우 경로를 `hello`로 지정했습니다. 이는 `/hello` 경로에 `GET` 요청이 있을 때 `hello` 메서드가 호출됨을 의미합니다.

## 컨트롤러 등록

이제 컨트롤러가 생성되었으므로 Nest.js 애플리케이션에 등록해야 합니다.

`main.ts`에서 컨트롤러를 가져와서 `NestFactory.create` 메서드에 전달하면 됩니다.

```typescript
import { HelloController } from './controllers/hello.controller';

async function bootstrap() {
  const app = await NestFactory.create(
    ServerlessApplicationModule,
    {
      controllers: [HelloController],
    },
  );
  await app.listen(3000);
}
bootstrap();
```

위의 코드에서는 `hello.controller.ts`에서 `HelloController`를 가져왔습니다. 그런 다음 `NestFactory.create` 메서드의 `controllers` 배열에 전달했습니다.

그러면 Nest.js 애플리케이션에 `HelloController`가 등록됩니다.

## 애플리케이션 배포

이제 Nest.js 애플리케이션을 만들고 컨트롤러를 등록했으므로 애플리케이션을 배포할 준비가 되었습니다.

애플리케이션을 AWS Lambda에 배포할 것입니다. Lambda는 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 서버리스 플랫폼입니다.

애플리케이션을 Lambda에 배포하기 위해 `nest deploy` 명령을 사용합니다. 이 명령은 애플리케이션을 패키징하고 Lambda에 배포합니다.

```
nest deploy
```

이 명령은 새로운 Lambda 함수를 생성하고 여기에 Nest.js 애플리케이션을 배포합니다.

배포가 완료되면 `/hello` 경로에 `GET` 요청을 만들어 애플리케이션을 테스트할 수 있습니다. 반환된 `Hello, world!` 문자열을 볼 수 있습니다.

## 결론

이 게시물에서는 Nest.js를 사용하여 서버리스 애플리케이션을 구축하고 배포하는 방법을 배웠습니다.

Nest.js는 서버리스 애플리케이션 구축에 탁월한 선택입니다. 가볍고 빠르며 TypeScript 지원, 사용하기 쉬운 종속성 주입 시스템 및 강력한 모듈 시스템과 같은 다양한 기능을 제공합니다.

Nest.js로 서버리스 애플리케이션을 빠르고 쉽게 구축할 수 있습니다. 이 게시물에서는 간단한 서버리스 Nest.js 애플리케이션을 생성하고 이를 AWS Lambda에 배포하는 단계를 살펴보았습니다.