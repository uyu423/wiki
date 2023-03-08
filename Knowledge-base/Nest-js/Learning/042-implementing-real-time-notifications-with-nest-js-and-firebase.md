---
title: 042: Nest.js 및 Firebase로 실시간 알림 구현
description: 
published: true
date: 2023-02-12T03:17:53.925Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:17:52.261Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [042: Implementing real-time notifications with Nest.js and Firebase***English** document is available*](/en/Knowledge-base/Nest-js/Learning/042-implementing-real-time-notifications-with-nest-js-and-firebase)
{.links-list}


# Nest.js 및 Firebase로 실시간 알림 구현

이 게시물에서는 FCM(Firebase Cloud Messaging) 서비스를 사용하여 Nest.js 애플리케이션에서 실시간 알림을 설정하는 방법을 살펴보겠습니다.

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(JavaScript로 컴파일됨)로 구축되었으며 객체 지향 프로그래밍, 기능적 프로그래밍 및 반응형 프로그래밍의 요소를 결합합니다.

Firebase는 Google에서 개발한 모바일 및 웹 애플리케이션 개발 플랫폼입니다. 여러 서비스를 제공하며 그 중 하나가 FCM입니다. FCM은 무료로 안정적으로 메시지를 전달할 수 있는 크로스 플랫폼 메시징 솔루션입니다.

## Nest.js 프로젝트 설정

새로운 Nest.js 프로젝트를 설정하는 것으로 시작하겠습니다. 이를 위해 Nest CLI를 사용할 것입니다. 설치되어 있지 않은 경우 다음 명령을 실행하여 설치할 수 있습니다.

```
$ npm install -g @nestjs/cli
```

Nest CLI가 설치되면 다음 명령을 실행하여 새 프로젝트를 만들 수 있습니다.

```
$ nest new project-name
```

이렇게 하면 프로젝트 파일이 있는 새 디렉터리가 생성됩니다.

## 종속성 설치

프로젝트에 다음 종속 항목을 설치해야 합니다.

- @nestjs/common
- @nestjs/platform-express
- firebase 관리자

다음 명령을 실행하여 이러한 종속성을 설치할 수 있습니다.

```
$ npm install --save @nestjs/common @nestjs/platform-express firebase-admin
```

## Firebase 구성

FCM을 사용하기 위해서는 새로운 Firebase 프로젝트를 생성해야 합니다. [Firebase 콘솔](https://console.firebase.google.com/)로 이동하여 '프로젝트 만들기' 버튼을 클릭하면 됩니다.

프로젝트 이름을 지정하고 "프로젝트 만들기" 버튼을 클릭합니다.

프로젝트가 생성되면 "웹 앱에 Firebase 추가" 버튼을 클릭합니다.

그러면 Firebase 구성이 포함된 팝업이 열립니다. 구성 개체를 복사하여 프로젝트의 `environment.ts` 파일에 추가해야 합니다. 파일은 다음과 같아야 합니다.

```javascript
export const environment = {
  production: false,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

또한 `environment.prod.ts` 파일에 다음 행을 추가해야 합니다.

```javascript
export const environment = {
  production: true,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

## FCM 서비스 생성

FCM 메시지 전송을 처리할 새 서비스를 만들어야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ nest generate service fcm
```

그러면 `src/fcm` 디렉토리에 새 서비스 파일이 생성됩니다. `firebase-admin` 모듈과 `environment` 파일을 가져와야 합니다. 또한 `admin.messaging.Messaging` 클래스의 새 인스턴스를 만들어야 합니다. 서비스는 다음과 같아야 합니다.

```javascript
import { Injectable } from '@nestjs/common';
import * as admin from 'firebase-admin';
import { environment } from '../../environments/environment';

@Injectable()
export class FcmService {
  private readonly messaging = admin.messaging();

  constructor() {
    admin.initializeApp({
      credential: admin.credential.applicationDefault(),
      databaseURL: environment.firebase.databaseURL,
      projectId: environment.firebase.projectId
    });
  }

  // ...
}
```

## FCM 메시지 보내기

FCM 메시지를 보낼 'FcmService'에 새 메서드를 추가해야 합니다. 이 메서드는 메시지 수신자를 지정하는 `to` 매개변수와 보낼 데이터가 포함된 `data` 매개변수를 취해야 합니다.

이 메서드는 메시지가 전송된 시점을 확인하는 'Promise'를 반환해야 합니다.

```javascript
  async send(to: string, data: any): Promise<void> {
    const message = {
      to,
      data
    };

    await this.messaging.send(message);
  }
```

## 컨트롤러 만들기

`FcmService`의 `send` 메서드를 호출할 새 컨트롤러를 만들어야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
$ nest generate controller fcm
```

이렇게 하면 `src/fcm` 디렉토리에 새 컨트롤러 파일이 생성됩니다. `FcmService` 및 `@nestjs/common` 모듈을 가져와야 합니다. 또한 `FcmService`를 컨트롤러에 주입해야 합니다. 컨트롤러는 다음과 같아야 합니다.

```javascript
import { Controller, Post, Body } from '@nestjs/common';
import { FcmService } from './fcm.service';

@Controller('fcm')
export class FcmController {
  constructor(private readonly fcmService: FcmService) {}

  @Post()
  async send(@Body('to') to: string, @Body('data') data: any): Promise<void> {
    await this.fcmService.send(to, data);
  }
}
```

## 컨트롤러 테스트

`to` 및 `data` 매개변수를 사용하여 `/fcm` 끝점에 POST 요청을 전송하여 컨트롤러를 테스트할 수 있습니다. [Postman](https://www.getpostman.com/) 도구를 사용하면 됩니다.

메시지가 성공적으로 전송된 경우 Postman 콘솔에 성공 메시지가 표시되어야 합니다.

## 결론

이 게시물에서는 FCM(Firebase Cloud Messaging) 서비스를 사용하여 Nest.js 애플리케이션에서 실시간 알림을 설정하는 방법을 살펴보았습니다.