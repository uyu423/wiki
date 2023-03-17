---
title: 001: Nest.js 시작하기: 초보자를 위한 소개
description: 
published: true
date: 2023-03-17T19:24:00.355Z
tags: 
editor: markdown
dateCreated: 2023-03-17T19:24:00.355Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [001: Getting Started with Nest.js: An Introduction for Beginners***English** document is available*](/en/Knowledge-base/Nest-js/Learning/001-getting-started-with-nest-js-an-introduction-for-beginners)
{.links-list}

## Nest.js 소개

**Nest.js**는 JavaScript 또는 TypeScript를 사용하여 확장 가능하고 유지 관리 가능한 서버 측 애플리케이션을 구축하기 위한 강력하고 유연한 프레임워크입니다. 인기 있는 Node.js 플랫폼의 기능을 활용하고 이를 Angular에서 영감을 받은 모범 사례의 견고성과 결합합니다.

이 블로그 게시물에서는 Nest.js의 기본 사항을 탐색하고, 새 프로젝트를 설정하고, 핵심 개념을 이해하고, 간단한 RESTful API를 생성합니다.

### 왜 Nest.js인가?

다음은 Nest.js가 다른 서버 측 프레임워크 중에서 돋보이는 몇 가지 이유입니다.

1. **확장성**: Nest.js는 모듈식 아키텍처로 구축되어 애플리케이션 크기에 맞게 확장되는 방식으로 코드를 쉽게 구성하고 구조화할 수 있습니다.
2. **TypeScript 지원**: Nest.js는 TypeScript를 최고 수준으로 지원하므로 서버 측 코드에서 정적 타이핑 및 최신 언어 기능을 사용할 수 있습니다.
3. **종속성 주입**: Nest.js는 강력한 종속성 주입(DI) 시스템을 사용하여 종속성을 쉽게 관리하고 코드 재사용성을 촉진합니다.
4. **유연한**: Nest.js는 다양한 데이터베이스, ORM 및 타사 라이브러리와 함께 사용할 수 있으므로 프로젝트에 가장 적합한 도구를 자유롭게 선택할 수 있습니다.
5. **테스트 가능**: Nest.js는 테스트 기반 개발을 촉진하고 애플리케이션을 쉽게 테스트할 수 있는 유틸리티를 제공합니다.

이러한 이점을 염두에 두고 새로운 Nest.js 프로젝트를 설정하는 방법을 살펴보겠습니다.

## 새 Nest.js 프로젝트 설정

Nest.js를 시작하려면 컴퓨터에 Node.js를 설치해야 합니다. Node.js가 설치되어 있지 않은 경우 [공식 웹 사이트](https://nodejs.org/en/download/)에서 다운로드할 수 있습니다.

Node.js가 설치되면 다음 단계에 따라 새 Nest.js 프로젝트를 만들 수 있습니다.

### 1. Nest CLI 설치

Nest CLI는 Nest.js 프로젝트를 생성, 관리 및 빌드하는 데 도움이 되는 명령줄 도구입니다. Nest CLI를 설치하려면 터미널을 열고 다음 명령을 실행합니다.

```bash
npm install -g @nestjs/cli
```

이 명령은 컴퓨터에 Nest CLI를 전역으로 설치하여 모든 디렉터리에서 사용할 수 있도록 합니다.

### 2. 새 프로젝트 만들기

Nest CLI를 설치한 후 다음 명령을 실행하여 새 Nest.js 프로젝트를 만들 수 있습니다.

```bash
nest new my-nest-project
```

`my-nest-project`를 원하는 프로젝트 이름으로 바꿉니다. Nest CLI는 패키지 관리자(npm 또는 yarn)를 선택한 다음 프로젝트에 필요한 파일과 폴더를 생성하라는 메시지를 표시합니다.

### 3. 프로젝트 디렉토리로 이동

프로젝트가 생성되면 다음을 실행하여 프로젝트 디렉토리로 이동합니다.

```bash
cd my-nest-project
```

### 4. 애플리케이션 실행

Nest.js 애플리케이션을 시작하려면 프로젝트 디렉토리 내에서 다음 명령을 실행하십시오.

```bash
npm run start
```

이 명령은 개발 모드에서 응용 프로그램을 시작합니다. 즉, 코드를 변경하면 자동으로 다시 로드됩니다. 다음 출력이 표시되어야 합니다.

```bash
[Nest] 12345   - 12/34/56   Starting compilation...
[Nest] 12345   - 12/34/56   Compilation complete. Starting Nest application...
[Nest] 12345   - 12/34/56   Nest application successfully started
```

기본적으로 Nest.js 애플리케이션은 [http://localhost:3000](http://localhost:3000)에서 실행됩니다. 브라우저에서 이 URL을 방문하거나 [Postman](https://www.postman.com/)과 같은 도구를 사용하여 HTTP 요청을 만들어 애플리케이션을 테스트할 수 있습니다.

## Nest.js 핵심 개념 이해

이제 Nest.js 프로젝트가 설정되었으므로 애플리케이션을 빌드할 때 작업하게 될 몇 가지 핵심 개념을 살펴보겠습니다.

### 모듈

Nest.js에서 **모듈**은 `@Module()` 데코레이터로 장식된 클래스입니다. 모듈은 애플리케이션을 더 작고 재사용 가능한 조각으로 구성하는 데 사용됩니다. 모듈은 다른 모듈을 가져오고, 구성 요소를 선언하고, 다른 모듈에 제공할 수 있습니다.

다음은 간단한 모듈의 예입니다.

```typescript
import { Module } from '@nestjs/common';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';

@Module({
  imports: [],
  controllers: [CatsController],
  providers: [CatsService],
})
export class CatsModule {}
```

이 예에서 `CatsModule`은 `CatsController` 및 `CatsService` 구성 요소를 가져와 필요할 수 있는 다른 모듈에 제공합니다.

### 컨트롤러

**컨트롤러**는 `@Controller()` 데코레이터로 장식된 클래스입니다. 컨트롤러는 들어오는 HTTP 요청을 처리하고 응답을 반환하는 역할을 합니다. 경로 및 관련 요청 처리 논리를 정의합니다.

다음은 간단한 컨트롤러의 예입니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('cats')
export class CatsController {
  @Get()
  findAll(): string {
    return 'This action returns all cats';
  }
}
```

이 예에서 `CatsController`는 단일 경로인 `/cats`를 정의하며 "이 작업은 모든 고양이를 반환합니다"라는 텍스트로 HTTP GET 요청에 응답합니다.

### 공급자

**공급자**는 애플리케이션에서 종속성을 만들고 관리하는 데 사용할 수 있는 클래스 또는 팩터리 함수입니다. 공급자는 `@Injectable()` 데코레이터로 데코레이트되며 Nest.js의 종속성 주입 시스템을 사용하여 다른 구성 요소에 주입할 수 있습니다.

다음은 간단한 공급자의 예입니다.

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class CatsService {
  private readonly cats: string[] = [];

  create(cat: string) {
    this.cats.push(cat);
  }

  findAll(): string[] {
    return this.cats;
  }
}
```

이 예에서 'CatsService'는 고양이 목록을 관리하는 공급자입니다. 새 고양이를 추가하고 모든 고양이를 검색하는 방법을 제공합니다.

## 간단한 RESTful API 만들기

이러한 핵심 개념을 사용하는 방법을 보여주기 위해 고양이 관리를 위한 간단한 RESTful API를 만들어 보겠습니다. `Cat` 인터페이스와 함께 작동하도록 `CatsService`를 업데이트하는 것으로 시작하겠습니다.

```typescript
import { Injectable } from '@nestjs/common';
import { Cat } from './interfaces/cat.interface';

@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  create(cat: Cat) {
    this.cats.push(cat);
  }

  findAll(): Cat[] {
    return this.cats;
  }
}
```

다음으로 `src/cats/interfaces` 폴더에 `cat.interface.ts`라는 새 파일을 만들고 `Cat` 인터페이스를 정의합니다.

```typescript
export interface Cat {
  id: number;
  name: string;
  age: number;
  breed: string;
}
```

이제 요청을 처리하기 위해 `CatsService`를 사용하도록 `CatsController`를 업데이트하겠습니다.

```typescript
import { Controller, Get, Post, Body } from '@nestjs/common';
import { CatsService } from './cats.service';
import { Cat } from './interfaces/cat.interface';

@Controller('cats')
export class CatsController {
  constructor(private readonly catsService: CatsService) {}

  @Post()
  create(@Body() cat: Cat): void {
    this.catsService.create(cat);
  }

  @Get()
  findAll(): Cat[] {
    return this.catsService.findAll();
  }
}
```

이 업데이트된 `CatsController` 버전에서는 HTTP POST 요청을 사용하여 고양이를 생성하기 위한 새로운 경로를 추가했습니다. 문자열 대신 `Cat` 개체의 배열을 반환하도록 `findAll()` 메서드도 업데이트했습니다.

이러한 변경으로 간단한 RESTful API가 완성되었습니다. Postman과 같은 도구를 사용하거나 API를 사용하는 간단한 프런트 엔드 애플리케이션을 만들어 API를 테스트할 수 있습니다.

## 결론

이 블로그 게시물에서는 새 프로젝트 설정, 핵심 개념 이해, 간단한 RESTful API 생성을 포함하여 Nest.js의 기본 사항을 다뤘습니다. Nest.js는 JavaScript 또는 TypeScript를 사용하여 확장 가능하고 유지 관리 가능한 서버 측 애플리케이션을 구축하는 데 도움이 되는 강력하고 유연한 프레임워크입니다.

Nest.js 및 해당 기능에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

- [Nest.js 공식 문서](https://docs.nestjs.com/)
- [Nest.js GitHub 저장소](https://github.com/nestjs/nest)
- [Udemy의 Nest.js 과정](https://www.udemy.com/course/nestjs-zero-to-hero/)

즐거운 코딩하세요!