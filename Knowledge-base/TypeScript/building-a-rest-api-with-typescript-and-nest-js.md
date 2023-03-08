---
title: TypeScript 및 Nest.js로 REST API 빌드
description: 
published: true
date: 2023-02-17T18:12:50.757Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:44:00.602Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Building a REST API with TypeScript and Nest.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-a-rest-api-with-typescript-and-nest-js)
{.links-list}


# TypeScript와 Nest.js로 REST API 구축

Nest.js는 TypeScript 및 JavaScript(ES6, 7, 8) 위에 효율적이고 확장 가능한 엔터프라이즈급 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다.

## 왜 Nest.js를 사용하나요?

REST API를 구축하기 위해 Nest.js를 사용하려는 이유는 많습니다.

Nest.js는 TypeScript를 기반으로 하므로 정적 유형 검사를 포함하여 TypeScript의 모든 이점을 활용할 수 있습니다. 이는 동적으로 유형이 지정되는 JavaScript와 대조됩니다.

또한 Nest.js는 JavaScript Express 프레임워크를 활용합니다. Express는 Node.js를 위한 빠르고 독선적이지 않은 미니멀리스트 웹 프레임워크입니다. Express를 사용함으로써 Nest.js는 사용 가능한 수많은 Express 플러그인 및 미들웨어를 활용할 수 있습니다.

Nest.js는 또한 매우 모듈식입니다. Nest.js 아키텍처는 CRNA(Common Root Name Architecture)를 기반으로 합니다. 이 아키텍처를 사용하면 Nest.js의 각 모듈을 서로 독립적으로 사용할 수 있습니다.

## TypeScript 사용의 이점

Nest.js는 TypeScript를 기반으로 하므로 TypeScript의 모든 기능을 활용할 수 있습니다. TypeScript는 선택적 정적 유형을 코드에 추가하는 JavaScript의 상위 집합입니다.

JavaScript보다 TypeScript를 사용하면 다음과 같은 이점이 있습니다.

- TypeScript는 JavaScript의 상위 집합입니다. 즉, 유효한 모든 JavaScript 코드는 유효한 TypeScript 코드이기도 합니다. 이를 통해 JavaScript 개발자는 TypeScript를 쉽게 시작할 수 있습니다.

- TypeScript 코드는 JavaScript로 컴파일되므로 모든 JavaScript 환경에서 실행됩니다. 이를 통해 서버나 웹 브라우저에 TypeScript 코드를 쉽게 배포할 수 있습니다.

- TypeScript는 정적으로 입력됩니다. 이것은 TypeScript 컴파일러가 실행되기 전에 코드의 오류를 확인할 수 있음을 의미합니다. 이것은 오류가 코드에 도입되는 것을 방지하는 데 도움이 될 수 있습니다.

- TypeScript 컴파일러는 이전 버전의 JavaScript와 호환되는 JavaScript 코드를 생성할 수 있습니다. 이를 특정 JavaScript 버전을 "타겟팅"하는 것으로 알려져 있습니다. 이는 이전 브라우저나 서버를 지원해야 할 때 유용할 수 있습니다.

- TypeScript는 자체 유형 정의 파일과 함께 제공됩니다. 이 파일을 사용하여 코드에서 예상되는 값 유형에 대한 TypeScript 정보를 제공할 수 있습니다. 이는 JavaScript로 작성된 타사 라이브러리를 사용할 때 특히 유용합니다.

## TypeScript 및 Nest.js 설치

TypeScript와 Nest.js를 사용하려면 설치가 필요합니다. TypeScript 컴파일러는 npm 패키지 관리자를 사용하여 설치할 수 있습니다.

```
npm install -g typescript
```

Nest.js 프레임워크는 npm 패키지 관리자를 사용하여 설치할 수 있습니다.

```
npm install -g @nestjs/cli
```

## Nest.js와 함께 TypeScript 사용

Nest.js는 TypeScript를 프로그래밍 언어로 사용합니다. 즉, Nest.js 애플리케이션을 개발할 때 TypeScript를 사용해야 합니다.

TypeScript는 JavaScript의 상위 집합입니다. 즉, 모든 유효한 JavaScript 코드는 유효한 TypeScript 코드이기도 합니다. TypeScript는 선택적 정적 유형을 코드에 추가합니다.

JavaScript보다 TypeScript를 사용하면 다음과 같은 이점이 있습니다.

- TypeScript는 정적으로 입력됩니다. 이것은 TypeScript 컴파일러가 실행되기 전에 코드의 오류를 확인할 수 있음을 의미합니다. 이것은 오류가 코드에 도입되는 것을 방지하는 데 도움이 될 수 있습니다.

- TypeScript 컴파일러는 이전 버전의 JavaScript와 호환되는 JavaScript 코드를 생성할 수 있습니다. 이를 특정 JavaScript 버전을 "타겟팅"하는 것으로 알려져 있습니다. 이는 이전 브라우저나 서버를 지원해야 할 때 유용할 수 있습니다.

- TypeScript는 자체 유형 정의 파일과 함께 제공됩니다. 이 파일을 사용하여 코드에서 예상되는 값 유형에 대한 TypeScript 정보를 제공할 수 있습니다. 이는 JavaScript로 작성된 타사 라이브러리를 사용할 때 특히 유용합니다.

Nest.js는 코드베이스 전체에서 TypeScript 언어를 사용합니다. 즉, Nest.js를 효과적으로 사용하려면 TypeScript에 익숙해져야 합니다.

TypeScript에 익숙하지 않은 경우 TypeScript 웹 사이트에서 TypeScript 자습서를 확인할 수 있습니다.

## Nest.js 애플리케이션 만들기

TypeScript와 Nest.js가 설치되었으므로 이제 Nest.js 애플리케이션을 만들 수 있습니다.

Nest.js CLI를 사용하여 새 Nest.js 애플리케이션을 만들 수 있습니다.

```
nest new my-api
```

이렇게 하면 "my-api"라는 디렉터리에 새 Nest.js 애플리케이션이 생성됩니다.

## 경로 정의

경로는 Nest.js 라우터에서 정의됩니다. 라우터는 애플리케이션의 경로를 정의하는 데 사용되는 모듈입니다.

경로는 경로와 핸들러 함수로 정의됩니다. 경로는 들어오는 요청의 URL을 일치시키는 데 사용되는 문자열입니다. 핸들러 기능은 들어오는 요청을 처리하고 응답을 생성하는 데 사용됩니다.

Nest.js에서 경로는 ```app.routing.ts```. 

```타입스크립트
import { ModuleWithProviders, RouterModule, Routes } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

const 경로: 경로 = [
  { 경로: '/', 컨트롤러: AppController, 방법: 'get' },
];

내보내기 const AppRoutingModule: ModuleWithProviders = RouterModule.forRoot(라우트);
```

In the code above, a route is defined for the path ```/```. This route will match the URL ```/``` and will use the ```AppController``` to handle the request. 

The ```AppController``` is a Nest.js controller. Controllers are responsible for handling requests and generating responses. 

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

In the code above, the ```AppController``` is annotated with the ```@Controller``` decorator. This decorator tells Nest.js that this class is a controller. 

The ```AppController``` has a single route handler. This handler is annotated with the ```@Get``` decorator. This decorator tells Nest.js that this handler will process GET requests. 

The ```getHello()``` handler is a simple handler that returns the string "Hello World!". 

## Defining Services

Services are used to encapsulate business logic in Nest.js applications. Services are injected into controllers and are used to process requests and generate responses. 

Services are defined in the file ```app.service.ts```. 

```타입스크립트
'@nestjs/common'에서 { 주입 가능 } 가져오기;

@주사용()
내보내기 클래스 AppService {
  getHello(): 문자열 {
    'Hello World!'를 반환합니다.
  }
}
```

In the code above, the ```AppService``` is annotated with the ```@Injectable``` decorator. This decorator tells Nest.js that this class is a service. 

The ```AppService``` has a single method, ```getHello()```. This method returns the string "Hello World!". 

## Injecting Services

Services are injected into controllers using the ```@Inject()``` decorator. 

```타입스크립트
import { Controller, Get, Inject } from '@nestjs/common';
import { AppService } from './app.service';

@제어 장치()
내보내기 클래스 AppController {
  건설자(
    @Inject('앱_서비스')
    개인 읽기 전용 appService: AppService,
  ) {}

  @얻다()
  getHello(): 문자열 {
    this.appService.getHello()를 반환합니다.
  }
}
```

In the code above, the ```AppService``` is injected into the ```AppController``` using the ```@Inject()``` decorator. The ```@Inject()``` decorator takes a service token as a parameter. The service token is used to identify the service that is being injected. 

The ```@Inject()``` decorator can be used to inject services into controller methods as well as controller constructor methods. 

## Running the Application

The Nest.js CLI can be used to run the application. 

```
둥지 시작
```

이렇게 하면 포트 3000에서 Nest.js 애플리케이션이 시작됩니다.