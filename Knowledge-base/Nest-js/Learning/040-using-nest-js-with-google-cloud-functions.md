---
title: 040: Google 클라우드 기능과 함께 Nest.js 사용
description: 
published: true
date: 2023-02-15T12:32:37.683Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:32:36.056Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [040: Using Nest.js with Google Cloud Functions***English** document is available*](/en/Knowledge-base/Nest-js/Learning/040-using-nest-js-with-google-cloud-functions)
{.links-list}


# Google Cloud 기능과 함께 Nest.js 사용

Google Cloud Functions는 서버를 프로비저닝하거나 관리할 필요 없이 코드를 실행할 수 있는 서버리스 플랫폼입니다. JavaScript, Python 및 Go를 비롯한 다양한 언어로 코드를 작성할 수 있습니다.

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(JavaScript에 정적 유형 검사를 제공)로 구축되었으며 객체 지향 및 기능 프로그래밍의 요소를 결합합니다.

이 게시물에서는 Google Cloud Functions와 함께 Nest.js를 사용하는 방법을 보여줍니다. MongoDB 데이터베이스에서 사용자 목록을 반환하는 간단한 함수를 만듭니다.

## 1. 새 프로젝트 만들기

먼저 새 프로젝트를 만들어야 합니다. Nest.js CLI를 사용하여 새 프로젝트를 생성합니다.

```
$ nest new project-name
```

## 2. 종속성 설치

다음으로 프로젝트에 대한 종속성을 설치해야 합니다. MongoDB Node.js 드라이버와 Nest.js MongoDB 패키지가 필요합니다.

```
$ npm install mongodb @nestjs/mongoose
```

## 3. Nest.js 모듈 생성

다음으로 Nest.js 모듈을 만들어야 합니다. 이것은 MongoDB와 상호 작용하기 위한 코드를 포함할 표준 JavaScript 모듈입니다.

```javascript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [
    MongooseModule.forFeature([
      { name: 'User', schema: UserSchema }
    ])
  ],
  providers: [UserService],
  exports: [UserService]
})
export class UserModule {}
```

## 4. Nest.js 서비스 만들기

다음으로 Nest.js 서비스를 만들어야 합니다. 이것은 MongoDB와 상호 작용하기 위한 코드를 포함할 표준 JavaScript 클래스입니다.

```javascript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class UserService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<User>
  ) {}

  async findAll(): Promise<User[]> {
    return await this.userModel.find().exec();
  }
}
```

## 5. Google 클라우드 기능 만들기

다음으로 Google Cloud Function을 만들어야 합니다. 이것은 누군가 API 끝점에 요청을 할 때 트리거되는 표준 JavaScript 기능입니다.

```javascript
import * as functions from 'firebase-functions';
import { NestFactory } from '@nestjs/core';
import { UserModule } from './user.module';

export const userApi = functions.https.onRequest(async (req, res) => {
  const app = await NestFactory.create(UserModule);
  await app.init();
  res.send(await app.get(UserService).findAll());
});
```

## 6. 함수 배포

마지막으로 함수를 배포해야 합니다. Firebase CLI를 사용하여 이 작업을 수행할 수 있습니다.

```
$ firebase deploy --only functions
```

## 7. API 엔드포인트 테스트

끝점 URL에 GET 요청을 만들어 API 끝점을 테스트할 수 있습니다. 사용자 목록과 함께 JSON 응답이 표시되어야 합니다.

```
$ curl https://us-central1-project-name.cloudfunctions.net/userApi
```

## 축하해요!

Google Cloud Functions를 사용하는 Nest.js API 끝점을 성공적으로 만들었습니다.