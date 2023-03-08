---
title: 027: Nest.js로 마이크로서비스 구현
description: 
published: true
date: 2023-02-15T07:32:35.248Z
tags: 
editor: markdown
dateCreated: 2023-02-15T07:32:27.445Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [027: Implementing microservices with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/027-implementing-microservices-with-nest-js)
{.links-list}


# Nest.js로 마이크로서비스 구현

마이크로서비스는 확장 가능하고 탄력적인 클라우드 애플리케이션을 구축하기 위한 인기 있는 아키텍처 스타일입니다. Nest.js는 효율적이고 확장 가능한 엔터프라이즈급 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다.

이 게시물에서는 Nest.js로 마이크로서비스를 구현하는 방법을 알아봅니다. 먼저 마이크로서비스가 무엇이고 왜 유용한지 살펴보겠습니다. 그런 다음 Nest.js를 사용하여 간단한 마이크로서비스를 만드는 방법을 살펴보겠습니다. 마지막으로 마이크로서비스를 클라우드 플랫폼에 배포하는 방법을 배웁니다.

## 마이크로서비스란?

마이크로서비스는 애플리케이션이 작고 독립적인 서비스 집합으로 구축되는 소프트웨어 아키텍처 스타일입니다. 각 서비스에는 단일 책임이 있으며 독립적으로 배포하고 확장할 수 있습니다.

마이크로서비스는 기존의 모놀리식 아키텍처에 비해 많은 이점이 있습니다. 개발, 배포 및 확장이 더 쉽습니다. 또한 한 서비스의 장애가 다른 서비스에 영향을 미치지 않기 때문에 복원력이 더 뛰어납니다.

## Nest.js로 마이크로서비스 만들기

마이크로서비스가 무엇인지 알아보았으니 이제 Nest.js를 사용하여 간단한 마이크로서비스를 만드는 방법을 알아보겠습니다.

Nest.js는 효율적이고 확장 가능한 엔터프라이즈급 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 정적 유형 검사 및 기타 이점을 제공하는 JavaScript의 상위 집합인 TypeScript를 사용합니다.

Nest.js 마이크로서비스를 만들기 위해 Nest CLI를 사용합니다. Nest CLI는 Nest.js 애플리케이션을 쉽게 생성, 빌드 및 테스트할 수 있는 명령줄 인터페이스입니다.

먼저 마이크로 서비스를 위한 새 디렉터리를 만듭니다.

```
mkdir my-microservice
```

다음으로 디렉터리에서 새 Nest.js 프로젝트를 초기화합니다.

```
nest init
```

이렇게 하면 디렉토리에 `package.json`이라는 파일이 생성됩니다. 이 파일에는 설치해야 하는 종속성을 포함하여 프로젝트에 대한 정보가 들어 있습니다.

다음으로 프로젝트의 종속 항목을 설치합니다.

```
npm install
```

이제 프로젝트가 설정되었으므로 마이크로서비스 코딩을 시작할 수 있습니다. `src/app.controller.ts`라는 파일을 생성하여 시작하겠습니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
  @Get()
  root(): string {
    return 'Hello World!';
  }
}
```

이 파일에는 `AppController`라는 컨트롤러가 포함되어 있습니다. 이 컨트롤러에는 문자열 `'Hello World!'`를 반환하는 단일 메서드 `root()`가 포함되어 있습니다.

다음으로 `src/app.module.ts`라는 파일을 만듭니다.

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';

@Module({
  controllers: [AppController],
})
export class AppModule {}
```

이 파일에는 `AppModule`이라는 모듈이 포함되어 있습니다. 이 모듈에는 `AppController`가 포함되어 있습니다.

마지막으로 `src/main.ts`라는 파일을 만듭니다.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

이 파일에는 마이크로 서비스를 시작할 코드가 포함되어 있습니다. 먼저 Nest.js 애플리케이션을 만들기 위한 팩토리인 새로운 `NestFactory`를 만듭니다. 그런 다음 `AppModule`을 `NestFactory`에 전달합니다. 마지막으로 `listen()` 메서드를 호출하여 포트 `3000`에서 마이크로서비스를 시작합니다.

이제 마이크로 서비스가 완료되었으므로 다음 명령을 실행하여 시작할 수 있습니다.

```
npm start
```

그런 다음 http://localhost:3000에서 마이크로 서비스에 액세스할 수 있습니다.

## 마이크로서비스 배포

이제 Nest.js를 사용하여 마이크로서비스를 만드는 방법을 살펴보았으므로 이를 배포하는 방법을 알아보겠습니다.

마이크로서비스를 배포하는 방법에는 여러 가지가 있습니다. 이 게시물에서는 Docker를 사용하여 마이크로 서비스를 클라우드 플랫폼에 배포하는 방법을 배웁니다.

Docker는 컨테이너에서 애플리케이션을 쉽게 패키징, 배포 및 실행할 수 있게 해주는 도구입니다. 컨테이너는 코드, 런타임, 시스템 도구 및 라이브러리와 같이 애플리케이션을 실행하는 데 필요한 모든 것을 포함하는 독립형 환경입니다.

Docker를 사용하여 마이크로서비스를 클라우드 플랫폼에 배포하려면 먼저 `Dockerfile`을 생성해야 합니다.

```
FROM node:10.16.0-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

이 `Dockerfile`에는 Docker 이미지를 빌드하기 위한 지침이 포함되어 있습니다. 먼저 사용하려는 `노드` 이미지를 지정합니다. 다음으로 애플리케이션을 위한 작업 디렉토리를 생성합니다. 그런 다음 `package.json` 파일을 작업 디렉토리에 복사합니다. 이 파일을 사용하여 애플리케이션의 종속성을 설치합니다.

다음으로 나머지 애플리케이션 코드를 작업 디렉터리에 복사합니다. 마지막으로 포트 `3000`을 노출하고 컨테이너가 시작될 때 실행되어야 하는 명령을 지정합니다.

이제 `Dockerfile`이 있으므로 Docker 이미지를 빌드할 수 있습니다.

```
docker build -t my-microservice .
```

이 명령은 `my-microservice` 태그가 있는 Docker 이미지를 생성합니다. 그런 다음 Docker 이미지를 실행할 수 있습니다.

```
docker run -d -p 3000:3000 my-microservice
```

이 명령은 `my-microservice` 이미지에서 컨테이너를 시작합니다. `-d` 플래그는 컨테이너가 분리 모드에서 실행되어야 함을 지정합니다. 이는 컨테이너가 백그라운드에서 실행됨을 의미합니다. `-p` 플래그는 호스트의 포트 `3000`이 컨테이너의 포트 `3000`에 매핑되어야 함을 지정합니다.

그런 다음 http://localhost:3000에서 마이크로 서비스에 액세스할 수 있습니다.

## 결론

이 게시물에서는 Nest.js로 마이크로서비스를 구현하는 방법을 배웠습니다. 간단한 마이크로서비스를 만드는 방법과 Docker를 사용하여 이를 클라우드 플랫폼에 배포하는 방법을 살펴보았습니다.