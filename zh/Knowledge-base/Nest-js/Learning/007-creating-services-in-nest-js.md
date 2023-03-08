---
title: 007：在 Nest.js 中创建服务
description: 
published: true
date: 2023-02-14T18:32:19.763Z
tags: 
editor: markdown
dateCreated: 2023-02-14T18:32:18.074Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [007: Creating services in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/007-creating-services-in-nest-js)
{.links-list}


# 介绍

在这篇文章中，我们将研究如何在 Nest.js 中创建服务。服务是在应用程序中抽象出复杂逻辑的好方法，而 Nest.js 提供了一种非常简单的方法来创建它们。

我们将涵盖以下主题：

- 什么是服务？
- 使用服务有什么好处？
- 如何在 Nest.js 中创建服务？
- 如何将服务注入 Nest.js 组件？
- 如何在 Nest.js 组件中使用服务？

# 什么是服务？

在软件工程中，服务是一个独立的功能单元，可以被应用程序中的其他组件访问。服务通常用于封装业务逻辑，并且可以跨应用程序的不同部分重复使用。

# 使用服务有什么好处？

在您的应用程序中使用服务有很多好处，包括：

- 服务可以帮助您保持代码干燥（不要重复自己）。
- 服务可以让你的代码更加模块化，更容易维护。
- 服务可以提高代码的可测试性。
- 服务可以使您的代码更具可扩展性。

# 如何在 Nest.js 中创建服务？

在 Nest.js 中创建服务非常简单。首先，在 `src/` 目录中创建一个新文件并将其命名为 `my-service.service.ts`。然后，将以下代码添加到文件中：

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {
  doSomething(): string {
    return 'Hello, world!';
  }
}
```

如您所见，我们已经导入了“@nestjs/common”模块，它提供了“@Injectable()”装饰器。然后我们使用这个装饰器将我们的 MyService 类标记为可注入的。

# 如何将服务注入 Nest.js 组件？

为了在 Nest.js 组件中使用服务，我们需要将其注入到组件中。将服务注入组件非常简单。首先，我们需要从 @nestjs/common 模块导入 @Inject() 装饰器。然后，我们可以使用这个装饰器将服务注入到组件中：

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

# 如何在 Nest.js 组件中使用服务？

一旦将服务注入到组件中，就可以像使用任何其他服务一样使用它。在下面的示例中，我们将使用 `MyService` 服务中的 `doSomething()` 方法：

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

# 结论

在这篇文章中，我们研究了如何在 Nest.js 中创建服务。服务是在应用程序中抽象出复杂逻辑的好方法，而 Nest.js 提供了一种非常简单的方法来创建它们。

我们还研究了如何将服务注入 Nest.js 组件以及如何在 Nest.js 组件中使用服务。

如果您想了解有关 Nest.js 中服务的更多信息，我建议您查看以下资源：

- [Nest.js 文档 - 服务](https://docs.nestjs.com/fundamentals/services)
- [Nest.js 教程 - 服务](https://nestjs.com/tutorials/services)
- [Nest.js 示例 - 服务](https://github.com/nestjs/nest/tree/master/sample/10-services)