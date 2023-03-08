---
title: 050: 고급 Nest.js 기능 및 기술
description: 
published: true
date: 2023-02-15T18:33:03.091Z
tags: 
editor: markdown
dateCreated: 2023-02-15T18:33:00.848Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [050: Advanced Nest.js features and techniques***English** document is available*](/en/Knowledge-base/Nest-js/Learning/050-advanced-nest-js-features-and-techniques)
{.links-list}


050: 고급 Nest.js 기능 및 기술

Nest.js는 Node.js를 위한 강력한 웹 프레임워크입니다. Express.js 위에 구축되었으며 TypeScript를 사용하므로 엔터프라이즈급 애플리케이션을 쉽게 개발하고 배포할 수 있습니다.

이 게시물에서는 Nest.js가 제공하는 몇 가지 고급 기능과 기술을 살펴보겠습니다.

다음 주제를 다룰 것입니다.

- 라우팅
- 인증 및 승인
- 데이터베이스 액세스
- 테스트

## 라우팅

Nest.js에서 경로는 @Controller() 데코레이터를 사용하여 정의됩니다. 예를 들어:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

보시다시피 @Controller() 데코레이터는 컨트롤러 내에서 정의된 모든 경로의 기본 경로를 정의합니다. @Get(), @Post(), @Put() 및 @Delete() 데코레이터는 각 경로에 대한 HTTP 메서드를 정의하는 데 사용됩니다.

## 인증 및 승인

Nest.js는 인증 및 권한 부여에 대한 기본 지원을 제공합니다.

사용자를 인증하기 위해 Nest.js는 @Authenticate() 데코레이터를 제공합니다. 이 데코레이터는 컨트롤러 또는 메서드 수준에서 사용할 수 있습니다.

예를 들어 UserController에 정의된 모든 경로를 인증하려면 컨트롤러에서 @Authenticate() 데코레이터를 사용할 수 있습니다.

```typescript
@Controller('/users')
@Authenticate()
export class UserController {
  // ...
}
```

특정 경로만 인증하려면 메소드에 @Authenticate() 데코레이터를 사용할 수 있습니다.

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authenticate()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Nest.js는 승인을 위해 @Authorize() 데코레이터도 제공합니다. 이 데코레이터는 컨트롤러 또는 메서드 수준에서 사용할 수 있습니다.

예를 들어 UserController에 정의된 모든 경로에 권한을 부여하려면 컨트롤러에서 @Authorize() 데코레이터를 사용할 수 있습니다.

```typescript
@Controller('/users')
@Authorize()
export class UserController {
  // ...
}
```

특정 경로만 승인하려면 메소드에 @Authorize() 데코레이터를 사용할 수 있습니다.

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authorize()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

## 데이터베이스 액세스

Nest.js는 데이터베이스에 액세스하는 여러 가지 방법을 제공합니다.

가장 일반적인 방법은 @Inject() 데코레이터를 사용하여 데이터베이스 클라이언트를 컨트롤러 또는 서비스에 주입하는 것입니다.

예를 들어 MongoDB 클라이언트를 컨트롤러에 주입하려면 다음 코드를 사용할 수 있습니다.

```typescript
@Controller('/users')
export class UserController {

  constructor(
    @Inject('MONGODB_CLIENT') private mongodb: MongoClient,
  ) {}

  // ...

}
```

데이터베이스에 액세스하는 또 다른 방법은 @UseDatabases() 데코레이터를 사용하는 것입니다. 이 데코레이터는 컨트롤러 또는 서비스 수준에서 사용할 수 있습니다.

예를 들어 컨트롤러에서 MongoDB 및 PostgreSQL을 사용하려면 다음 코드를 사용할 수 있습니다.

```typescript
@Controller('/users')
@UseDatabases(['MONGODB', 'POSTGRESQL'])
export class UserController {

  // ...

}
```

## 테스트

Nest.js는 애플리케이션을 테스트하는 여러 가지 방법을 제공합니다.

가장 일반적인 방법은 @Test() 데코레이터를 사용하는 것입니다. 이 데코레이터는 컨트롤러 또는 서비스 수준에서 사용할 수 있습니다.

예를 들어 UserController를 테스트하려면 다음 코드를 사용할 수 있습니다.

```typescript
@Test()
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

애플리케이션을 테스트하는 또 다른 방법은 @TestModule() 데코레이터를 사용하는 것입니다. 이 데코레이터는 모듈 수준에서 사용할 수 있습니다.

예를 들어 UserModule을 테스트하려면 다음 코드를 사용할 수 있습니다.

```typescript
@TestModule()
export class UserModule {}
```

## 결론

이 게시물에서는 Nest.js가 제공하는 몇 가지 고급 기능과 기술을 다루었습니다.

경로를 정의하는 방법, 사용자를 인증 및 권한 부여하는 방법, 데이터베이스에 액세스하는 방법 및 Nest.js 애플리케이션을 테스트하는 방법을 살펴보았습니다.

Nest.js에 대해 자세히 알아보려면 공식 문서를 확인하는 것이 좋습니다.