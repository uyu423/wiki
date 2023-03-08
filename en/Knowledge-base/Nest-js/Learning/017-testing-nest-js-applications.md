---
title: 017: Testing Nest.js applications
description: 
published: true
date: 2023-02-10T19:55:57.660Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:55:51.000Z
---

- [017: Prueba de aplicaciones Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/017-testing-nest-js-applications)
{.links-list}
- [017：测试 Nest.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/017-testing-nest-js-applications)
{.links-list}
- [017: Nest.js 애플리케이션 테스트***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/017-testing-nest-js-applications)
{.links-list}


## Introduction 

In this post, we'll be looking at how to test Nest.js applications. Nest.js is a Node.js framework for building server-side applications. 

Nest.js applications are easy to test, as they are built using modular and testable components. In this post, we'll go over some of the different ways to test Nest.js applications.

## Unit Testing 

Unit testing is a type of testing where individual units of code are tested. In Nest.js, units of code are typically methods in services or controllers.

To unit test a Nest.js application, we need to:

1. Import the module we want to test
2. Create an instance of the class we want to test
3. Call the method we want to test and assert that the expected output is returned

Let's look at an example. Suppose we have a simple Nest.js service that adds two numbers together. The code for this service would look like this:

```javascript
export class CalculatorService {
  public add(a: number, b: number): number {
    return a + b;
  }
}
```

We can unit test this service by doing the following:

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

In the code above, we:

1. Imported the module we want to test
2. Created an instance of the class we want to test
3. Called the method we want to test and asserted that the expected output is returned

This is a simple example, but it shows how we can unit test a Nest.js application.

## Integration Testing 

Integration testing is a type of testing where different units of code are tested together. In Nest.js, units of code are typically services or controllers.

To integration test a Nest.js application, we need to:

1. Import the module we want to test
2. Create an instance of the class we want to test
3. Call the methods we want to test and assert that the expected output is returned

Let's look at an example. Suppose we have a simple Nest.js service that adds two numbers together and a controller that calls this service. The code for these would look like this:

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

We can integration test this controller by doing the following:

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

In the code above, we:

1. Imported the module we want to test
2. Created an instance of the class we want to test
3. Called the methods we want to test and asserted that the expected output is returned

This is a simple example, but it shows how we can integration test a Nest.js application.

## End-to-End Testing 

End-to-end testing is a type of testing where the entire application is tested from start to finish. In Nest.js, this means testing the application from the http request to the response.

To end-to-end test a Nest.js application, we need to:

1. Import the module we want to test
2. Create an instance of the class we want to test
3. Call the methods we want to test and assert that the expected output is returned

Let's look at an example. Suppose we have a simple Nest.js application that has a controller that returns a list of users. The code for this controller would look like this:

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

We can end-to-end test this controller by doing the following:

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

In the code above, we:

1. Imported the module we want to test
2. Created an instance of the class we want to test
3. Called the methods we want to test and asserted that the expected output is returned

This is a simple example, but it shows how we can end-to-end test a Nest.js application.

## Conclusion 

In this post, we've looked at how to test Nest.js applications. Nest.js applications are easy to test, as they are built using modular and testable components.

We've looked at three different types of testing: unit testing, integration testing, and end-to-end testing. Each type of testing has its own benefits and drawbacks, so it's important to choose the right type of testing for your needs.

If you're just starting out with testing, unit testing is a good place to start. Once you're more comfortable with testing, you can move on to integration and end-to-end testing.