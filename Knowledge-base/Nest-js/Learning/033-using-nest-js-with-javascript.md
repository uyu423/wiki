---
title: 033: 자바스크립트로 Nest.js 사용하기
description: 
published: true
date: 2023-02-15T11:32:41.761Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:32:40.163Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [033: Using Nest.js with JavaScript***English** document is available*](/en/Knowledge-base/Nest-js/Learning/033-using-nest-js-with-javascript)
{.links-list}


# 자바스크립트로 Nest.js 사용하기

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(선택 사항)로 구축되며 객체 지향 프로그래밍, 기능 프로그래밍 및 반응 프로그래밍의 요소를 결합합니다.

Nest.js는 JavaScript 배경을 가진 개발자를 위한 훌륭한 프레임워크입니다. 사용하기 쉽고 친숙한 구문이 있습니다. 이 게시물에서는 JavaScript로 Nest.js를 사용하는 방법을 살펴보겠습니다.

## 설치

Nest.js를 설치하려면 머신에 Node.js와 npm이 설치되어 있어야 합니다. 그런 다음 다음 명령을 사용하여 Nest.js를 설치할 수 있습니다.

```
npm install -g @nestjs/cli
```

## Nest.js 프로젝트 생성

Nest.js가 설치되면 Nest.js CLI를 사용하여 새 프로젝트를 만들 수 있습니다. 이렇게 하려면 다음 명령을 실행합니다.

```
nest new project-name
```

그러면 지정한 이름으로 새 Nest.js 프로젝트가 생성됩니다.

## 프로젝트 이름/src/app.controller.js

우리가 살펴볼 첫 번째 파일은 app.controller.js 파일입니다. 컨트롤러를 정의할 파일입니다. 컨트롤러는 하나 이상의 메서드를 포함하는 클래스입니다. 각 메서드는 요청 처리를 담당합니다.

간단한 컨트롤러를 살펴보겠습니다.

```javascript
import { Controller, Get, Post, Body } from '@nestjs/common';

@Controller('/api/v1/todos')
export class TodosController {
  @Get()
  findAll() {
    return [];
  }

  @Post()
  create(@Body() createTodoDto) {
    return [];
  }
}
```

위의 코드에서 우리는 findAll과 create라는 두 가지 메서드로 컨트롤러를 정의했습니다. findAll 메소드는 GET 요청 처리를 담당합니다. create 메소드는 POST 요청 처리를 담당합니다.

## 프로젝트 이름/src/app.service.js

다음으로 살펴볼 파일은 app.service.js 파일입니다. 이것은 서비스를 정의할 파일입니다. 서비스는 비즈니스 로직을 포함하는 클래스입니다.

간단한 서비스를 살펴보겠습니다.

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class TodosService {
  getAll() {
    return [];
  }

  create(createTodoDto) {
    return [];
  }
}
```

위의 코드에서 getAll 및 create라는 두 가지 메서드로 서비스를 정의했습니다. getAll 메소드는 모든 todos를 반환합니다. create 메소드는 새로운 todo를 생성합니다.

## 프로젝트 이름/src/app.module.js

다음으로 살펴볼 파일은 app.module.js 파일입니다. 모듈을 정의할 파일입니다. 모듈은 컨트롤러와 서비스를 포함하는 클래스입니다.

간단한 모듈을 살펴보겠습니다.

```javascript
import { Module } from '@nestjs/common';
import { TodosController } from './app.controller';
import { TodosService } from './app.service';

@Module({
  controllers: [TodosController],
  providers: [TodosService],
})
export class TodosModule {}
```

위의 코드에서 우리는 컨트롤러와 서비스로 모듈을 정의했습니다. 컨트롤러는 요청 처리를 담당합니다. 서비스는 비즈니스 로직을 담당합니다.

## 프로젝트 이름/src/main.js

다음으로 살펴볼 파일은 main.js 파일입니다. 이것은 Nest.js 애플리케이션을 시작할 파일입니다.

코드를 살펴보겠습니다.

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

위의 코드에서 NestFactory와 AppModule을 가져왔습니다. 그런 다음 새 Nest.js 애플리케이션을 만들고 포트 3000에서 시작했습니다.

## 결론

이 게시물에서는 JavaScript로 Nest.js를 사용하는 방법을 살펴보았습니다. Nest.js를 설치하고 새 프로젝트를 만드는 방법을 살펴보았습니다. 또한 컨트롤러, 서비스 및 모듈을 정의하는 방법도 살펴보았습니다.