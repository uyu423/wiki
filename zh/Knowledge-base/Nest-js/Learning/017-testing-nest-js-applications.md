---
title: 017：测试 Nest.js 应用程序
description: 
published: true
date: 2023-02-10T19:55:52.632Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:55:50.991Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [017: Testing Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/017-testing-nest-js-applications)
{.links-list}


## 介绍

在这篇文章中，我们将研究如何测试 Nest.js 应用程序。 Nest.js 是一个用于构建服务器端应用程序的 Node.js 框架。

Nest.js 应用程序易于测试，因为它们是使用模块化和可测试的组件构建的。在这篇文章中，我们将介绍一些测试 Nest.js 应用程序的不同方法。

## 单元测试

单元测试是一种测试单个代码单元的测试。在 Nest.js 中，代码单元通常是服务或控制器中的方法。

要对 Nest.js 应用程序进行单元测试，我们需要：

1.导入我们要测试的模块
2.创建我们要测试的类的实例
3.调用我们要测试的方法并断言返回预期的输出

让我们看一个例子。假设我们有一个简单的 Nest.js 服务，可以将两个数字相加。该服务的代码如下所示：

```javascript
export class CalculatorService {
  public add(a: number, b: number): number {
    return a + b;
  }
}
```

我们可以通过执行以下操作对该服务进行单元测试：

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

在上面的代码中，我们：

1.导入我们要测试的模块
2.创建了我们要测试的类的实例
3.调用了我们要测试的方法并断言返回了预期的输出

这是一个简单的示例，但它展示了我们如何对 Nest.js 应用程序进行单元测试。

## 集成测试

集成测试是一种测试，其中不同的代码单元被一起测试。在 Nest.js 中，代码单元通常是服务或控制器。

要集成测试 Nest.js 应用程序，我们需要：

1.导入我们要测试的模块
2.创建我们要测试的类的实例
3.调用我们要测试的方法并断言返回预期的输出

让我们看一个例子。假设我们有一个简单的 Nest.js 服务，可以将两个数字相加，还有一个调用该服务的控制器。这些代码如下所示：

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

我们可以通过执行以下操作来集成测试此控制器：

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

在上面的代码中，我们：

1.导入我们要测试的模块
2.创建了我们要测试的类的实例
3.调用我们要测试的方法并断言返回预期的输出

这是一个简单的示例，但它展示了我们如何集成测试 Nest.js 应用程序。

## 端到端测试

端到端测试是一种从头到尾测试整个应用程序的测试。在 Nest.js 中，这意味着从 http 请求到响应测试应用程序。

要端到端测试 Nest.js 应用程序，我们需要：

1.导入我们要测试的模块
2.创建我们要测试的类的实例
3.调用我们要测试的方法并断言返回预期的输出

让我们看一个例子。假设我们有一个简单的 Nest.js 应用程序，它有一个返回用户列表的控制器。该控制器的代码如下所示：

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

我们可以通过执行以下操作来端到端地测试这个控制器：

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

在上面的代码中，我们：

1.导入我们要测试的模块
2.创建了我们要测试的类的实例
3.调用我们要测试的方法并断言返回预期的输出

这是一个简单的示例，但它展示了我们如何端到端地测试 Nest.js 应用程序。

## 结论

在这篇文章中，我们研究了如何测试 Nest.js 应用程序。 Nest.js 应用程序易于测试，因为它们是使用模块化和可测试的组件构建的。

我们已经研究了三种不同类型的测试：单元测试、集成测试和端到端测试。每种类型的测试都有其自身的优点和缺点，因此根据您的需要选择正确的测试类型非常重要。

如果您刚刚开始测试，单元测试是一个很好的起点。一旦您熟悉了测试，就可以继续进行集成和端到端测试。