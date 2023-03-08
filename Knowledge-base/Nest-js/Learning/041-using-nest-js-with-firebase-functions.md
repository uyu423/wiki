---
title: 041: Firebase 기능과 함께 Nest.js 사용
description: 
published: true
date: 2023-02-15T13:33:20.754Z
tags: 
editor: markdown
dateCreated: 2023-02-15T13:33:19.105Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [041: Using Nest.js with Firebase Functions***English** document is available*](/en/Knowledge-base/Nest-js/Learning/041-using-nest-js-with-firebase-functions)
{.links-list}


# Firebase 기능과 함께 Nest.js 사용

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(유형화된 JavaScript 제공)로 구축되었으며 객체 지향 프로그래밍, 기능적 프로그래밍 및 기능적 반응 프로그래밍의 요소를 결합합니다.

Firebase Functions는 서버를 프로비저닝하거나 관리할 필요 없이 클라우드에서 JavaScript 코드를 실행할 수 있는 서버리스 플랫폼입니다. 기능은 Firebase 실시간 데이터베이스의 데이터 변경, Firebase 인증을 통한 신규 사용자 가입 또는 Firebase 클라우드 메시징을 통한 수신 메시지와 같은 Firebase 제품의 이벤트에 의해 트리거될 수 있습니다.

이 게시물에서는 Firebase Functions와 함께 Nest.js를 사용하는 방법을 알아봅니다. Firebase Functions에서 실행되고 HTTP 요청에 응답하는 간단한 Nest.js 서버리스 애플리케이션을 빌드합니다.

## 프로젝트 설정

먼저 새로운 Nest.js 프로젝트를 생성해 보겠습니다. Nest CLI를 사용하여 새 프로젝트를 생성합니다. 다음 명령을 실행하여 새 프로젝트를 생성합니다.

```
$ nest new nest-firebase-functions
```

그러면 ```nest-firebase-functions```라는 폴더에 새 Nest.js 프로젝트가 생성됩니다.

다음으로 Node.js용 Firebase Functions SDK를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ npm install firebase-functions@latest firebase-admin@latest --save
```

이렇게 하면 최신 버전의 Firebase Functions SDK 및 Firebase Admin SDK가 설치됩니다.

## 코드 작성

이제 Nest.js 프로젝트와 Firebase SDK가 설치되었으므로 몇 가지 코드를 작성할 수 있습니다.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

import * as functions from 'firebase-functions';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(() => console.log('Nest.js is listening'));
}

export const api = functions.https.onRequest(bootstrap);
```타입스크립트
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

import * as functions from 'firebase-functions';

비동기 함수 부트스트랩() {
  const app = await NestFactory.create(AppModule);
  await app.listen(() => console.log('Nest.js가 듣고 있습니다'));
}

export const api = functions.https.onRequest(bootstrap);
```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```@nestjs/core```에서 ```NestFactory``` 및 ```AppModule```을 가져옵니다.

다음으로 전체 ```firebase-functions``` 네임스페이스를 가져옵니다. 이렇게 하면 HTTP 기능을 구성하는 데 사용할 ```functions``` 객체에 액세스할 수 있습니다.

그런 다음 ```bootstrap```이라는 ```async``` 함수를 정의합니다. 이 함수는 HTTP 함수가 호출될 때 호출됩니다. ```await``` 키워드는 비동기 작업이 완료될 때까지 기다리는 데 사용됩니다.

```typescript
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```bootstrap``` 함수를 호출하는 ```functions.https.onRequest``` 함수를 내보냅니다. 이렇게 하면 ```/api``` 끝점에 대한 HTTP 요청이 있을 때 Nest.js 애플리케이션이 호출됩니다.

이제 코드가 있으므로 ```app.module.ts``` 파일을 살펴보겠습니다. 이것은 Nest.js 모듈을 정의하는 파일입니다.

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```타입스크립트
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@기준 치수({
  수입: [],
  컨트롤러: [AppController],
  공급자: [AppService],
})
내보내기 클래스 AppModule {}
```
$ firebase init
```AppModule```을 정의합니다.

우리 모듈은 ```@nestjs/common```에서 ```Module``` 데코레이터를 가져옵니다. 이 데코레이터는 Nest.js 모듈을 정의하는 데 사용됩니다.

우리 모듈은 또한 ```./app``` 폴더에서 ```AppController``` 및 ```AppService```를 가져옵니다. 잠시 후에 이 파일들을 살펴보겠습니다.

```
$ firebase deploy
```app.module.ts``` 파일을 보았으니 이제 ```app.controller.ts``` 파일을 살펴보겠습니다. 이 파일은 ```AppController```를 정의합니다.

```
$ curl https://{your-firebase-project-id}.firebaseio.com/api
```타입스크립트
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@제어 장치()
내보내기 클래스 AppController {
  생성자(비공개 읽기 전용 appService: AppService) {}

  @얻다()
  getHello(): 문자열 {
    this.appService.getHello()를 반환합니다.
  }
}
```

컨트롤러는 ```@nestjs/common```에서 ```Controller``` 및 ```Get``` 데코레이터를 가져옵니다. 이러한 데코레이터는 각각 컨트롤러와 컨트롤러 작업을 정의하는 데 사용됩니다.

컨트롤러는 ```./app``` 폴더에서 ```AppService```도 가져옵니다. 잠시 후 이 파일을 살펴보겠습니다.

```@Controller``` 데코레이터는 컨트롤러를 정의하는 데 사용됩니다. ```@Controller('/')``` 구문은 컨트롤러 작업에 액세스할 수 있는 경로를 지정합니다. 이 경우 컨트롤러 작업은 루트 경로(```/```)에서 액세스할 수 있습니다.

```@Get()``` 데코레이터는 컨트롤러 작업을 정의하는 데 사용됩니다. ```@Get('/')``` 구문은 컨트롤러 작업에 액세스할 수 있는 경로를 지정합니다. 이 경우 컨트롤러 작업은 루트 경로(```/```)에서 액세스할 수 있습니다.

```getHello``` 메소드는 컨트롤러 액션입니다. 이 메소드는 HTTP GET 요청이 ```/``` 엔드포인트에 대해 작성될 때 호출됩니다. ```getHello``` 메소드는 HTTP 응답에서 클라이언트로 다시 전송될 문자열을 반환합니다.

이제 ```app.controller.ts``` 파일을 보았으니 ```app.service.ts``` 파일을 살펴보겠습니다. 이 파일은 ```AppService```를 정의합니다.

```app.service.ts``` 파일을 열고 내용을 다음으로 바꿉니다.

```타입스크립트
'@nestjs/common'에서 { 주입 가능 } 가져오기;

@주사용()
내보내기 클래스 AppService {
  getHello(): 문자열 {
    'Hello World!'를 반환합니다.
  }
}
```

우리 서비스는 ```@nestjs/common```에서 ```Injectable``` 데코레이터를 가져옵니다. 이 데코레이터는 서비스를 정의하는 데 사용됩니다.

```@Injectable()``` 데코레이터는 서비스를 구성하는 데 사용됩니다.

```getHello``` 메소드는 문자열을 반환하는 간단한 메소드입니다. 이 메서드는 컨트롤러 작업에 의해 호출됩니다.

## 코드 배포

이제 코드를 작성했으므로 Firebase에 배포해야 합니다.

먼저 Firebase 프로젝트를 생성해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ 파이어베이스 초기화
```

이렇게 하면 현재 디렉터리에 새 Firebase 프로젝트가 생성됩니다.

다음으로 코드를 Firebase에 배포해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ Firebase 배포
```

이렇게 하면 코드가 Firebase에 배포됩니다.

## 코드 테스트

이제 코드가 배포되었으므로 테스트해 보겠습니다.

```/api``` 끝점에 대한 HTTP 요청을 만들어 코드를 테스트할 수 있습니다. ```curl``` 명령을 사용하여 이 작업을 수행할 수 있습니다. 다음 명령을 실행하여 HTTP 요청을 만듭니다.

```
$ curl https://{your-firebase-project-id}.firebaseio.com/api
```

그러면 ```/api``` 엔드포인트에 대한 HTTP 요청이 생성되고 응답이 콘솔에 출력됩니다.

## 결론

이번 포스트에서는 Firebase Functions와 함께 Nest.js를 사용하는 방법에 대해 알아보았습니다. Firebase Functions에서 실행되고 HTTP 요청에 응답하는 간단한 Nest.js 서버리스 애플리케이션을 구축했습니다.