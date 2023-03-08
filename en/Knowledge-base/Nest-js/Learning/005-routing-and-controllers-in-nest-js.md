---
title: 005: Routing and controllers in Nest.js
description: 
published: true
date: 2023-02-14T16:32:26.679Z
tags: 
editor: markdown
dateCreated: 2023-02-14T16:32:24.579Z
---

- [005: Enrutamiento y controladores en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/005-routing-and-controllers-in-nest-js)
{.links-list}
- [005: Nest.js 中的路由和控制器***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/005-routing-and-controllers-in-nest-js)
{.links-list}
- [005: Nest.js의 라우팅 및 컨트롤러***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/005-routing-and-controllers-in-nest-js)
{.links-list}


# Introduction

Nest.js is a Node.js framework for building server-side applications. It is based on Express.js and makes use of TypeScript, which is a superset of JavaScript that adds static typing to the language. 

Nest.js is a relatively new framework and as such, it does not have as much documentation or community support as Express.js. However, it is growing in popularity and is used by companies such as Microsoft, Google, and Amazon.

In this post, we will take a look at how to set up routing and controllers in Nest.js. We will also look at some of the benefits of using Nest.js over Express.js.

# Setting up routing and controllers in Nest.js

The first thing we need to do is install the Nest.js framework. We can do this using the Node.js package manager, npm.

```
npm install --save @nestjs/common
```

Once Nest.js is installed, we can create a new file in our project called `app.controller.ts`. This file will contain our controller logic.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/')
export class AppController {
  @Get()
  root() {
    return 'Hello, world!';
  }
}
```

In the code above, we have imported the `Controller` and `Get` decorators from `@nestjs/common`. We have then used the `@Controller` decorator to create a new controller at the `/` path. 

Finally, we have created a new `root` method and decorated it with the `@Get` decorator. This method will be called when a GET request is made to the `/` path.

We can now create a new file called `main.ts`. This file will be used to start our Nest.js application.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

In the code above, we have imported the `NestFactory` and `AppModule` from `@nestjs/core`. We have then used the `NestFactory` to create a new Nest.js application and passed in our `AppModule`. 

Finally, we have called the `listen` method to start the application on port 3000.

If we now run the application using `node main.ts`, we should see the following output:

```
$ node main.ts
[Nest] 7100   - 2020-03-22 10:54:54   [NestFactory] Starting Nest application...
[Nest] 7100   - 2020-03-22 10:54:54   [InstanceLoader] AppModule dependencies initialized +0ms
[Nest] 7100   - 2020-03-22 10:54:54   [RouterExplorer] Mapped {,GET} route +2ms
[Nest] 7100   - 2020-03-22 10:54:54   [NestApplication] Nest application successfully started +2ms
```

If we now open up our browser and navigate to `http://localhost:3000/`, we should see the following output:

```
Hello, world!
```

# Conclusion

In this post, we have seen how to set up routing and controllers in Nest.js. We have also looked at some of the benefits of using Nest.js over Express.js.

If you are looking for a Node.js framework that makes use of TypeScript, then Nest.js is definitely worth considering.