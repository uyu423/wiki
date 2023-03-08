---
title: 007: Nest.js에서 서비스 만들기
description: 
published: true
date: 2023-02-14T18:32:19.744Z
tags: 
editor: markdown
dateCreated: 2023-02-14T18:32:18.066Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [007: Creating services in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/007-creating-services-in-nest-js)
{.links-list}


# 소개

이 게시물에서는 Nest.js에서 서비스를 만드는 방법을 살펴보겠습니다. 서비스는 애플리케이션에서 복잡한 논리를 추상화하는 좋은 방법이며 Nest.js는 이를 생성하는 매우 간단한 방법을 제공합니다.

다음 주제를 다룰 것입니다.

- 서비스란?
- 서비스를 이용하면 어떤 혜택이 있나요?
- Nest.js에서 서비스를 만드는 방법은 무엇입니까?
- Nest.js 구성 요소에 서비스를 주입하는 방법은 무엇입니까?
- Nest.js 구성 요소에서 서비스를 사용하는 방법은 무엇입니까?

# 서비스란?

소프트웨어 엔지니어링에서 서비스는 응용 프로그램의 다른 구성 요소에서 액세스할 수 있는 독립적인 기능 단위입니다. 서비스는 일반적으로 비즈니스 로직을 캡슐화하는 데 사용되며 애플리케이션의 여러 부분에서 재사용할 수 있습니다.

# 서비스를 이용하면 어떤 혜택이 있나요?

다음을 포함하여 애플리케이션에서 서비스를 사용하면 많은 이점이 있습니다.

- 서비스는 코드를 건조하게 유지하는 데 도움이 될 수 있습니다(Don't Repeat Yourself).
- 서비스는 코드를 보다 모듈화하고 유지 관리하기 쉽게 만들 수 있습니다.
- 서비스는 코드의 테스트 가능성을 향상시킬 수 있습니다.
- 서비스는 코드의 확장성을 높일 수 있습니다.

# Nest.js에서 서비스를 생성하는 방법은 무엇입니까?

Nest.js에서 서비스를 생성하는 것은 매우 간단합니다. 먼저 `src/` 디렉토리에 새 파일을 만들고 이름을 `my-service.service.ts`로 지정합니다. 그런 다음 파일에 다음 코드를 추가합니다.

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {
  doSomething(): string {
    return 'Hello, world!';
  }
}
```

보시다시피 `@Injectable()` 데코레이터를 제공하는 `@nestjs/common` 모듈을 가져왔습니다. 그런 다음 이 데코레이터를 사용하여 `MyService` 클래스를 주입 가능한 것으로 표시했습니다.

# Nest.js 구성 요소에 서비스를 주입하는 방법은 무엇입니까?

Nest.js 구성 요소에서 서비스를 사용하려면 구성 요소에 서비스를 주입해야 합니다. 구성 요소에 서비스를 주입하는 것은 매우 간단합니다. 먼저 `@nestjs/common` 모듈에서 `@Inject()` 데코레이터를 가져와야 합니다. 그런 다음 이 데코레이터를 사용하여 서비스를 구성 요소에 주입할 수 있습니다.

```typescript
import { Injectable, Inject } from '@nestjs/common';
import { MyService } from './my-service.service';

@Injectable()
export class MyComponent {
  constructor(
    @Inject(MyService)
    private readonly myService: MyService,
  ) {}
}
```

# Nest.js 구성 요소에서 서비스를 사용하는 방법은 무엇입니까?

서비스가 구성 요소에 삽입되면 다른 서비스처럼 사용할 수 있습니다. 다음 예에서는 `MyService` 서비스의 `doSomething()` 메서드를 사용합니다.

```typescript
import { Injectable, Inject } from '@nestjs/common';
import { MyService } from './my-service.service';

@Injectable()
export class MyComponent {
  constructor(
    @Inject(MyService)
    private readonly myService: MyService,
  ) {}

  doSomething(): string {
    return this.myService.doSomething();
  }
}
```

# 결론

이 게시물에서는 Nest.js에서 서비스를 만드는 방법을 살펴보았습니다. 서비스는 애플리케이션에서 복잡한 논리를 추상화하는 좋은 방법이며 Nest.js는 이를 생성하는 매우 간단한 방법을 제공합니다.

또한 Nest.js 구성 요소에 서비스를 주입하는 방법과 Nest.js 구성 요소에서 서비스를 사용하는 방법도 살펴보았습니다.

Nest.js의 서비스에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- [Nest.js 문서 - 서비스](https://docs.nestjs.com/fundamentals/services)
- [Nest.js 튜토리얼 - 서비스](https://nestjs.com/tutorials/services)
- [Nest.js 샘플 - 서비스](https://github.com/nestjs/nest/tree/master/sample/10-services)