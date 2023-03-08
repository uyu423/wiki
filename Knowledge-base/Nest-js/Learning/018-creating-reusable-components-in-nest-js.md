---
title: 018: Nest.js에서 재사용 가능한 구성 요소 만들기
description: 
published: true
date: 2023-02-07T21:17:22.330Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:17:16.590Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [018: Creating reusable components in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/018-creating-reusable-components-in-nest-js)
{.links-list}


# Nest.js에서 재사용 가능한 구성 요소 만들기

Nest.js는 Node.js 애플리케이션을 구축하기 위한 프레임워크입니다. TypeScript를 사용하며 Express.js 위에 구축됩니다.

Nest.js 사용의 이점 중 하나는 재사용 가능한 구성 요소를 쉽게 만들 수 있다는 것입니다. 이 게시물에서는 Nest.js에서 재사용 가능한 구성 요소를 만드는 방법을 살펴보겠습니다.

## 컴포넌트 정의

재사용 가능한 구성 요소를 만드는 첫 번째 단계는 구성 요소를 정의하는 것입니다. @Component 데코레이터를 사용하여 이를 수행할 수 있습니다.

예를 들어 사용자에 대한 정보를 기록하는 구성 요소를 만들고 싶다고 가정해 보겠습니다. 우리는 이것을 다음과 같이 정의할 것입니다:

```typescript
@Component()
export class UserLoggerComponent {
  // ...
}
```

## 컴포넌트 사용

구성 요소를 정의하면 이를 컨트롤러나 서비스에 주입하여 Nest.js 애플리케이션에서 사용할 수 있습니다.

예를 들어 사용자 생성 요청을 처리하는 컨트롤러가 있다고 가정해 보겠습니다. UserLoggerComponent를 이 컨트롤러에 주입하고 이를 사용하여 새 사용자에 대한 정보를 기록할 수 있습니다.

```typescript
@Controller('users')
export class UserController {
  constructor(private readonly userLogger: UserLoggerComponent) {}

  @Post()
  async createUser(@Body() userDto: UserDto) {
    // ...

    this.userLogger.log(userDto);

    // ...
  }
}
```

## 결론

이 게시물에서는 Nest.js에서 재사용 가능한 구성 요소를 만드는 방법을 살펴보았습니다. @Component 데코레이터를 사용하여 구성 요소를 정의하고 이를 사용하기 위해 컨트롤러에 주입했습니다.