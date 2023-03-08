---
title: Nest.js 및 TypeScript로 RESTful API 구축
description: 
published: true
date: 2023-02-15T14:55:40.805Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:55:39.208Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building RESTful APIs with Nest.js and TypeScript***English** document is available*](/en/Knowledge-base/TypeScript/building-restful-apis-with-nest-js-and-typescript)
{.links-list}


# Nest.js 및 TypeScript로 RESTful API 구축

Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 정적 유형 검사 및 기타 기능을 추가하고 RESTful API 구축을 위한 좋은 플랫폼을 제공하는 JavaScript의 상위 집합인 TypeScript를 사용합니다.

이 기사에서는 Nest.js 및 TypeScript를 사용하여 RESTful API를 빌드하는 방법을 살펴보겠습니다. 프로젝트 구조를 살펴보는 것으로 시작한 다음 API 엔드포인트 생성으로 이동합니다. 또한 Nest.js에서 TypeScript를 사용하는 방법도 살펴보겠습니다.

## 프로젝트 구조

Nest.js 프로젝트의 프로젝트 구조는 Node.js 프로젝트의 구조와 유사합니다. 소스 코드용 src 디렉토리와 테스트용 테스트 디렉토리가 있습니다. src 디렉토리에는 애플리케이션의 진입점인 main.ts 파일이 포함되어 있습니다. 테스트 디렉토리에는 테스트의 진입점인 main.spec.ts 파일이 포함되어 있습니다.

이 프로젝트에는 TypeScript 컴파일러를 구성하는 데 사용되는 tsconfig.json 파일도 있습니다. 이 파일에는 대상 JavaScript 버전 및 모듈 유형과 같은 컴파일러 옵션이 포함되어 있습니다.

프로젝트에는 종속성 및 스크립트와 같은 프로젝트의 메타데이터가 포함된 package.json 파일도 있습니다.

## API 끝점 만들기

가장 먼저 해야 할 일은 API 끝점을 만드는 것입니다. src/main.ts 파일에서 이 작업을 수행합니다.

익스프레스 모듈을 가져오고 익스프레스 애플리케이션을 만드는 것으로 시작하겠습니다. 또한 body-parser 모듈과 cors 모듈을 가져올 것입니다.

```javascript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as cors from 'cors';

const app = express();
```

다음으로 Express 애플리케이션을 구성합니다. 포트를 3000으로 설정하고 본문 파서와 cors 미들웨어를 활성화합니다.

```javascript
app.set('port', 3000);
app.use(bodyParser.json());
app.use(cors());
```

이제 API 엔드포인트를 생성합니다. 사용자 목록을 검색하기 위한 GET 엔드포인트부터 시작하겠습니다.

```javascript
app.get('/users', (req, res) => {
  // ...
});
```

다음으로 새 사용자를 만들기 위한 POST 끝점을 만듭니다.

```javascript
app.post('/users', (req, res) => {
  // ...
});
```

마지막으로 기존 사용자를 업데이트하기 위한 PUT 엔드포인트를 생성합니다.

```javascript
app.put('/users/:id', (req, res) => {
  // ...
});
```

## Nest.js와 함께 TypeScript 사용

Nest.js와 TypeScript는 함께 잘 작동합니다. Nest.js는 Nest.js와 함께 TypeScript를 쉽게 사용할 수 있는 데코레이터를 제공합니다.

예를 들어 @Controller 데코레이터를 사용하여 컨트롤러를 만들 수 있습니다. @Get 데코레이터를 사용하여 GET 끝점을 만들 수 있습니다. @Post 데코레이터를 사용하여 POST 끝점을 만들 수 있습니다.

```typescript
import { Controller, Get, Post, Put } from '@nestjs/common';

@Controller('/users')
export class UserController {

  @Get()
  getUsers() {
    // ...
  }

  @Post()
  createUser() {
    // ...
  }

  @Put(':id')
  updateUser() {
    // ...
  }

}
```