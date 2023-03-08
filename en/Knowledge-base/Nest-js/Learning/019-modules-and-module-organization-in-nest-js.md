---
title: 019: Modules and module organization in Nest.js
description: 
published: true
date: 2023-02-06T01:17:49.360Z
tags: 
editor: markdown
dateCreated: 2023-02-06T01:17:47.640Z
---

- [019: Módulos y organización de módulos en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/019-modules-and-module-organization-in-nest-js)
{.links-list}
- [019: Nest.js 中的模块和模块组织***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/019-modules-and-module-organization-in-nest-js)
{.links-list}
- [019: Nest.js의 모듈 및 모듈 구성***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/019-modules-and-module-organization-in-nest-js)
{.links-list}


# Modules and module organization in Nest.js

Nest.js is a Node.js framework for building scalable server-side applications. It uses modern JavaScript, is built with TypeScript (optional) and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

Nest.js is heavily inspired by Angular. In fact, the author of Nest.js is the same person who created Angular. Nest.js shares many of the same concepts and ideas as Angular, so if you're familiar with Angular, Nest.js will feel very familiar to you.

One of the key concepts in Nest.js is modules. Modules are used to organize your code and structure your application. Nest.js comes with a built-in module system, which is based on the CommonJS module system.

Modules are like libraries. They are a way of packaging up code so that it can be reused in other parts of your application. Nest.js modules are very similar to Angular modules.

Each Nest.js module is a collection of related components, directives, pipes, and services. Modules can import other modules, which gives you a way to share code between modules.

Modules can also export components, directives, pipes, and services so that they can be used in other modules.

Nest.js modules are different from Node.js modules. Node.js modules are used to build applications that run on Node.js. Nest.js modules are used to build applications that run on Node.js and use Nest.js.

Node.js modules are typically packaged up as libraries and published to npm. Nest.js modules are typically packaged up as libraries and published to npm as well.

## Creating a module

Creating a Nest.js module is simple. All you need is a directory with a file called `module.ts`. The `module.ts` file is the entry point for the module.

```typescript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

The `@Module` decorator is used to define a Nest.js module. The `@Module` decorator takes an object with a few properties. The most important property is the `imports` property.

The `imports` property is an array of other modules that this module depends on. This is how you share code between modules.

```typescript
import { Module } from '@nestjs/common';

@Module({
  imports: [OtherModule],
})
export class MyModule {}
```

The `imports` property is not required. If you don't need to share code between modules, you don't need to use the `imports` property.

## Module organization

Nest.js applications are typically organized into a set of modules. The main module is the root module and the other modules are child modules.

The root module is the module that is bootstrapped when the application is started. The other modules are loaded by the root module.

Child modules can be loaded by other child modules. This allows you to create a nested structure of modules.

The recommended way to organize modules is to have a feature module for each feature in your application. A feature module is a module that encapsulates a feature of your application.

For example, if you have a blog feature, you would have a blog feature module. The blog feature module would contain all the code for the blog feature.

Feature modules are typically organized into a directory structure. For example, the blog feature module might be organized into the following directory structure.

```
- blog
  - blog.module.ts
  - blog.service.ts
  - blog.controller.ts
  - blog.component.ts
  - blog.pipe.ts
  - blog.directive.ts
```

The `blog.module.ts` file is the module file for the blog feature module. The other files in the directory are the components of the module.

The recommended way to structure your application is to have a root module and a set of feature modules. This gives you a clean separation of concerns and a clear structure for your application.

## Summary

Modules are a key concept in Nest.js. Modules are used to organize your code and structure your application. Nest.js comes with a built-in module system, which is based on the CommonJS module system.

Each Nest.js module is a collection of related components, directives, pipes, and services. Modules can import other modules, which gives you a way to share code between modules.

Modules can also export components, directives, pipes, and services so that they can be used in other modules.

Nest.js modules are different from Node.js modules. Node.js modules are used to build applications that run on Node.js. Nest.js modules are used to build applications that run on Node.js and use Nest.js.

Node.js modules are typically packaged up as libraries and published to npm. Nest.js modules are typically packaged up as libraries and published to npm as well.

Creating a Nest.js module is simple. All you need is a directory with a file called `module.ts`. The `module.ts` file is the entry point for the module.

The `@Module` decorator is used to define a Nest.js module. The `@Module` decorator takes an object with a few properties. The most important property is the `imports` property.

The `imports` property is an array of other modules that this module depends on. This is how you share code between modules.

Nest.js applications are typically organized into a set of modules. The main module is the root module and the other modules are child modules.

Child modules can be loaded by other child modules. This allows you to create a nested structure of modules.

The recommended way to organize modules is to have a feature module for each feature in your application. A feature module is a module that encapsulates a feature of your application.

For example, if you have a blog feature, you would have a blog feature module. The blog feature module would contain all the code for the blog feature.