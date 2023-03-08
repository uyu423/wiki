---
title: 049: Common pitfalls to avoid when using Nest.js
description: 
published: true
date: 2023-02-02T04:17:41.867Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:17:37.613Z
---

- [049: Errores comunes que se deben evitar al usar Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/049-common-pitfalls-to-avoid-when-using-nest-js)
{.links-list}
- [049：使用 Nest.js 时要避免的常见陷阱***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/049-common-pitfalls-to-avoid-when-using-nest-js)
{.links-list}
- [049: Nest.js를 사용할 때 피해야 할 일반적인 함정***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/049-common-pitfalls-to-avoid-when-using-nest-js)
{.links-list}


# 049: Common pitfalls to avoid when using Nest.js

Nest.js is a powerful framework for building Node.js applications. However, as with any framework, there are certain common pitfalls that can trip up developers who are new to Nest. In this post, we'll take a look at some of the most common mistakes made when using Nest.js, and how to avoid them.

## 1. Not initializing Nest.js properly

One of the most common mistakes made when using Nest.js is failing to initialize the framework properly. Nest.js must be initialized with the `--init` flag when creating a new project:

```
nest new my-project --init
```

If you forget to include the `--init` flag, your project will not be set up properly and you will run into errors.

## 2. Not using the @Module decorator

Another mistake that is often made is forgetting to use the `@Module` decorator when creating modules. The `@Module` decorator is required for all Nest.js modules:

```javascript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

If you forget to use the `@Module` decorator, Nest.js will not be able to properly identify your module and you will run into errors.

## 3. Not using the @Controller decorator

Similarly, the `@Controller` decorator is required for all Nest.js controllers:

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

If you forget to use the `@Controller` decorator, Nest.js will not be able to properly identify your controller and you will run into errors.

## 4. Not using the @Injectable decorator

Another decorator that is often forgotten is the `@Injectable` decorator. The `@Injectable` decorator is required for all Nest.js services:

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

If you forget to use the `@Injectable` decorator, Nest.js will not be able to properly identify your service and you will run into errors.

## 5. Not using the @NestModule decorator

Another mistake that is often made is forgetting to use the `@NestModule` decorator when creating modules. The `@NestModule` decorator is required for all Nest.js modules:

```javascript
import { NestModule } from '@nestjs/common';

@NestModule({})
export class MyModule {}
```

If you forget to use the `@NestModule` decorator, Nest.js will not be able to properly identify your module and you will run into errors.

## 6. Not using the @NestController decorator

Similarly, the `@NestController` decorator is required for all Nest.js controllers:

```javascript
import { NestController } from '@nestjs/common';

@NestController('/my-controller')
export class MyController {}
```

If you forget to use the `@NestController` decorator, Nest.js will not be able to properly identify your controller and you will run into errors.

## 7. Not using the @NestInjectable decorator

Another decorator that is often forgotten is the `@NestInjectable` decorator. The `@NestInjectable` decorator is required for all Nest.js services:

```javascript
import { NestInjectable } from '@nestjs/common';

@NestInjectable()
export class MyService {}
```

If you forget to use the `@NestInjectable` decorator, Nest.js will not be able to properly identify your service and you will run into errors.

## 8. Not using the @Component decorator

Another mistake that is often made is forgetting to use the `@Component` decorator when creating modules. The `@Component` decorator is required for all Nest.js modules:

```javascript
import { Component } from '@nestjs/common';

@Component({})
export class MyModule {}
```

If you forget to use the `@Component` decorator, Nest.js will not be able to properly identify your module and you will run into errors.

## 9. Not using the @Controller decorator

Similarly, the `@Controller` decorator is required for all Nest.js controllers:

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

If you forget to use the `@Controller` decorator, Nest.js will not be able to properly identify your controller and you will run into errors.

## 10. Not using the @Injectable decorator

Another decorator that is often forgotten is the `@Injectable` decorator. The `@Injectable` decorator is required for all Nest.js services:

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

If you forget to use the `@Injectable` decorator, Nest.js will not be able to properly identify your service and you will run into errors.