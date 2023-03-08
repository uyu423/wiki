---
title: 017: Nest.js 애플리케이션 테스트
description: 
published: true
date: 2023-02-10T19:55:52.679Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:55:50.990Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [017: Testing Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/017-testing-nest-js-applications)
{.links-list}


## 소개

이 게시물에서는 Nest.js 애플리케이션을 테스트하는 방법을 살펴보겠습니다. Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다.

Nest.js 애플리케이션은 모듈식 및 테스트 가능한 구성 요소를 사용하여 빌드되므로 테스트하기 쉽습니다. 이 게시물에서는 Nest.js 애플리케이션을 테스트하는 다양한 방법 중 일부를 살펴보겠습니다.

## 단위 테스트

단위 테스트는 개별 코드 단위를 테스트하는 테스트 유형입니다. Nest.js에서 코드 단위는 일반적으로 서비스 또는 컨트롤러의 메서드입니다.

Nest.js 애플리케이션을 단위 테스트하려면 다음이 필요합니다.

1. 테스트하려는 모듈을 가져옵니다.
2. 테스트하려는 클래스의 인스턴스를 만듭니다.
3. 테스트하려는 메서드를 호출하고 예상 출력이 반환되는지 확인합니다.

예를 들어 보겠습니다. 두 개의 숫자를 더하는 간단한 Nest.js 서비스가 있다고 가정합니다. 이 서비스의 코드는 다음과 같습니다.

```javascript
export class CalculatorService {
  public add(a: number, b: number): number {
    return a + b;
  }
}
```

다음을 수행하여 이 서비스를 단위 테스트할 수 있습니다.

```javascript
import { Test, TestingModule } from '@nestjs/testing';
import { CalculatorService } from './calculator.service';

describe('CalculatorService', () => {
  let service: CalculatorService;
  
  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [CalculatorService],
    }).compile();
    
    service = module.get<CalculatorService>(CalculatorService);
  });
  
  it('should add two numbers together', () => {
    const result = service.add(1, 2);
    
    expect(result).toEqual(3);
  });
});
```

위의 코드에서 우리는:

1. 테스트하려는 모듈을 가져왔습니다.
2. 테스트하려는 클래스의 인스턴스를 생성했습니다.
3. 테스트하려는 메서드를 호출하고 예상 출력이 반환된다고 어설션

이것은 간단한 예이지만 Nest.js 애플리케이션을 단위 테스트하는 방법을 보여줍니다.

## 통합 테스팅

통합 테스트는 서로 다른 코드 단위를 함께 테스트하는 테스트 유형입니다. Nest.js에서 코드 단위는 일반적으로 서비스 또는 컨트롤러입니다.

Nest.js 애플리케이션을 통합 테스트하려면 다음이 필요합니다.

1. 테스트하려는 모듈을 가져옵니다.
2. 테스트하려는 클래스의 인스턴스를 만듭니다.
3. 테스트하려는 메서드를 호출하고 예상 출력이 반환되는지 확인합니다.

예를 들어 보겠습니다. 두 개의 숫자를 함께 추가하는 간단한 Nest.js 서비스와 이 서비스를 호출하는 컨트롤러가 있다고 가정합니다. 이에 대한 코드는 다음과 같습니다.

```javascript
// calculator.service.ts
export class CalculatorService {
  public add(a: number, b: number): number {
    return a + b;
  }
}
```

```javascript
// calculator.controller.ts
import { Controller, Get, Query } from '@nestjs/common';
import { CalculatorService } from './calculator.service';

@Controller('calculator')
export class CalculatorController {
  constructor(private readonly calculatorService: CalculatorService) {}
  
  @Get()
  public add(@Query('a') a: number, @Query('b') b: number): number {
    return this.calculatorService.add(a, b);
  }
}
```

다음을 수행하여 이 컨트롤러를 통합 테스트할 수 있습니다.

```javascript
import { Test, TestingModule } from '@nestjs/testing';
import { CalculatorController } from './calculator.controller';
import { CalculatorService } from './calculator.service';

describe('CalculatorController', () => {
  let controller: CalculatorController;
  
  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [CalculatorController],
      providers: [CalculatorService],
    }).compile();
    
    controller = module.get<CalculatorController>(CalculatorController);
  });
  
  it('should add two numbers together', () => {
    const result = controller.add(1, 2);
    
    expect(result).toEqual(3);
  });
});
```

위의 코드에서 우리는:

1. 테스트하려는 모듈을 가져왔습니다.
2. 테스트하려는 클래스의 인스턴스를 생성했습니다.
3. 테스트하려는 메서드를 호출하고 예상 출력이 반환된다고 어설션

이것은 간단한 예이지만 Nest.js 애플리케이션을 통합 테스트하는 방법을 보여줍니다.

## 종단 간 테스트

종단 간 테스트는 전체 응용 프로그램을 처음부터 끝까지 테스트하는 테스트 유형입니다. Nest.js에서 이는 http 요청에서 응답까지 애플리케이션을 테스트하는 것을 의미합니다.

Nest.js 애플리케이션을 종단 간 테스트하려면 다음이 필요합니다.

1. 테스트하려는 모듈을 가져옵니다.
2. 테스트하려는 클래스의 인스턴스를 만듭니다.
3. 테스트하려는 메서드를 호출하고 예상 출력이 반환되는지 확인합니다.

예를 들어 보겠습니다. 사용자 목록을 반환하는 컨트롤러가 있는 간단한 Nest.js 애플리케이션이 있다고 가정합니다. 이 컨트롤러의 코드는 다음과 같습니다.

```javascript
import { Controller, Get } from '@nestjs/common';
import { User } from './user.entity';
import { UserService } from './user.service';

@Controller('users')
export class UserController {
  constructor(private readonly userService: UserService) {}
  
  @Get()
  public findAll(): User[] {
    return this.userService.findAll();
  }
}
```

다음을 수행하여 이 컨트롤러를 종단 간 테스트할 수 있습니다.

```javascript
import { Test, TestingModule } from '@nestjs/testing';
import { UserController } from './user.controller';
import { UserService } from './user.service';

describe('UserController', () => {
  let controller: UserController;
  
  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [UserController],
      providers: [UserService],
    }).compile();
    
    controller = module.get<UserController>(UserController);
  });
  
  it('should return a list of users', () => {
    const result = controller.findAll();
    
    expect(result).toEqual([{ id: 1, name: 'John Doe' }, { id: 2, name: 'Jane Doe' }]);
  });
});
```

위의 코드에서 우리는:

1. 테스트하려는 모듈을 가져왔습니다.
2. 테스트하려는 클래스의 인스턴스를 생성했습니다.
3. 테스트하려는 메서드를 호출하고 예상 출력이 반환된다고 어설션

이것은 간단한 예이지만 Nest.js 애플리케이션을 종단 간 테스트하는 방법을 보여줍니다.

## 결론

이 게시물에서는 Nest.js 애플리케이션을 테스트하는 방법을 살펴보았습니다. Nest.js 애플리케이션은 모듈식 및 테스트 가능한 구성 요소를 사용하여 빌드되므로 테스트하기 쉽습니다.

단위 테스트, 통합 테스트 및 종단 간 테스트의 세 가지 유형의 테스트를 살펴보았습니다. 각 유형의 테스트에는 고유한 장점과 단점이 있으므로 필요에 맞는 올바른 유형의 테스트를 선택하는 것이 중요합니다.

테스트를 이제 막 시작했다면 단위 테스트를 시작하는 것이 좋습니다. 테스트에 익숙해지면 통합 및 종단 간 테스트로 이동할 수 있습니다.