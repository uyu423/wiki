---
title: 024: Nest.js에서 REST API 생성 및 사용
description: 
published: true
date: 2023-02-09T06:55:56.618Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:55:54.955Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [024: Creating and consuming REST APIs in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/024-creating-and-consuming-rest-apis-in-nest-js)
{.links-list}


# 소개

Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. Express.js를 기반으로 하며 TypeScript를 사용합니다.

프레임워크는 REST API를 생성하고 사용하기 위한 도구 및 라이브러리 세트를 제공합니다.

이 게시물에서는 Nest.js에서 REST API를 만들고 사용하는 방법을 배웁니다.

# Nest.js에서 REST API 생성

Nest.js는 REST API를 생성하기 위한 일련의 주석 및 데코레이터를 제공합니다.

## 주석 기반 API

Nest.js 주석은 reflect-metadata 라이브러리의 데코레이터를 기반으로 합니다.

주석을 사용하려면 다음과 같이 reflect-metadata 라이브러리를 설치해야 합니다.

```
npm install reflect-metadata --save
```

그런 다음 @Controller 및 @Get 주석을 사용하여 간단한 REST API를 만들 수 있습니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/api')
export class MyController {
  @Get('/hello')
  public hello(): string {
    return 'Hello World!';
  }
}
```

@Controller 주석은 컨트롤러의 경로를 정의합니다. @Get 주석은 컨트롤러의 메서드와 경로를 정의합니다.

위의 예에서 컨트롤러는 ```/api/hello```에서 액세스할 수 있습니다.

@Post, @Put, @Delete 및 @Patch 주석을 사용하여 리소스를 생성, 업데이트 및 삭제하기 위한 REST API를 생성할 수도 있습니다.

## 데코레이터 기반 API

Nest.js는 REST API를 생성하기 위한 데코레이터 세트도 제공합니다.

데코레이터를 사용하려면 @nestjs/common 라이브러리를 설치해야 합니다.

```
npm install @nestjs/common --save
```

그런 다음 @Controller 및 @Get 데코레이터를 사용하여 간단한 REST API를 만들 수 있습니다.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/api')
export class MyController {
  @Get('/hello')
  public hello(): string {
    return 'Hello World!';
  }
}
```

@Controller 데코레이터는 컨트롤러의 경로를 정의합니다. @Get 데코레이터는 컨트롤러의 메서드와 경로를 정의합니다.

위의 예에서 컨트롤러는 ```/api/hello```에서 액세스할 수 있습니다.

@Post, @Put, @Delete 및 @Patch 데코레이터를 사용하여 리소스를 생성, 업데이트 및 삭제하기 위한 REST API를 생성할 수도 있습니다.

# Nest.js에서 REST API 사용

Nest.js는 REST API를 사용하기 위한 라이브러리 세트를 제공합니다.

## HTTP 클라이언트

Nest.js에는 XMLHttpRequest API를 기반으로 하는 내장 HTTP 클라이언트가 포함되어 있습니다.

HTTP 클라이언트를 사용하려면 @nestjs/common 라이브러리를 설치해야 합니다.

```
npm install @nestjs/common --save
```

그런 다음 HTTP 클라이언트를 컨트롤러에 주입하고 이를 사용하여 HTTP 요청을 할 수 있습니다.

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import { HttpClient } from '@nestjs/common';

@Controller('/api')
export class MyController {
  constructor(private readonly httpClient: HttpClient) {}

  @Get('/hello')
  public async hello(): Promise<string> {
    const response = await this.httpClient.get('https://example.com/api/hello');
    return response.data;
  }
}
```

위의 예에서 HTTP 클라이언트를 컨트롤러에 주입하고 이를 사용하여 https://example.com/api/hello에 대한 GET 요청을 했습니다.

HTTP 클라이언트를 사용하여 POST, PUT, PATCH 및 DELETE 요청을 할 수도 있습니다.

## 악시오스

Nest.js는 Axios HTTP 클라이언트도 지원합니다.

Axios를 사용하려면 axios 및 @nestjs/common 라이브러리를 설치해야 합니다.

```
npm install axios @nestjs/common --save
```

그런 다음 Axios HTTP 클라이언트를 컨트롤러에 주입하고 이를 사용하여 HTTP 요청을 할 수 있습니다.

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import axios from 'axios';

@Controller('/api')
export class MyController {
  constructor(@Inject('AxiosInstance') private readonly axiosInstance: typeof axios) {}

  @Get('/hello')
  public async hello(): Promise<string> {
    const response = await this.axiosInstance.get('https://example.com/api/hello');
    return response.data;
  }
}
```

위의 예에서 Axios HTTP 클라이언트를 컨트롤러에 삽입하고 이를 사용하여 https://example.com/api/hello에 대한 GET 요청을 수행했습니다.

Axios HTTP 클라이언트를 사용하여 POST, PUT, PATCH 및 DELETE 요청을 할 수도 있습니다.

# 결론

이 게시물에서는 Nest.js에서 REST API를 만들고 사용하는 방법을 배웠습니다.