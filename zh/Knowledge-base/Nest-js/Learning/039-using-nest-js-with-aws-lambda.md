---
title: 039：将 Nest.js 与 AWS Lambda 结合使用
description: 
published: true
date: 2023-02-09T03:17:45.298Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:17:43.707Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [039: Using Nest.js with AWS Lambda***English** document is available*](/en/Knowledge-base/Nest-js/Learning/039-using-nest-js-with-aws-lambda)
{.links-list}


# 039：将 Nest.js 与 AWS Lambda 结合使用

AWS Lambda 是一个无服务器计算平台，让您无需预置或管理服务器即可运行代码。 Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。

在本文中，我们将向您展示如何将 Nest.js 与 AWS Lambda 结合使用。我们将创建一个简单的 Nest.js 应用程序并将其部署到 AWS Lambda。

## 创建 Nest.js 应用程序

首先，我们需要创建一个 Nest.js 应用程序。我们可以使用 Nest.js CLI 生成一个新项目。

```
$ nest new nest-lambda
```

这将在名为“nest-lambda”的文件夹中创建一个新的 Nest.js 项目。

接下来，我们需要安装“@nestjs/aws-lambda”包。该软件包为 AWS Lambda 提供了一个 Nest.js 适配器。

```
$ cd nest-lambda
$ npm install --save @nestjs/aws-lambda
```

现在我们已经安装了“@nestjs/aws-lambda”包，我们可以在“src”文件夹中创建一个名为“main.ts”的新文件。该文件将包含我们的 Nest.js 应用程序。

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

在这个文件中，我们从 Nest.js 导入了 `NestFactory` 和 `AppModule`。然后我们使用 `NestFactory` 来创建一个新的 Nest.js 应用程序。我们将我们的 AppModule 传递给了 NestFactory。最后，我们调用 `listen` 方法在端口 3000 上启动 Nest.js 应用程序。

## 部署到 AWS Lambda

现在我们有了一个 Nest.js 应用程序，我们可以将它部署到 AWS Lambda。首先，我们需要创建一个 AWS 账户。拥有帐户后，您可以创建新的 AWS Lambda 函数。

在 Lambda 控制台中，单击“创建函数”按钮。

![创建函数](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-create-function.png)

在“创建函数”页面上，选择“从头开始创作”选项。

![author-from-scratch](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-author-from-scratch.png)

在“配置函数”页面上，输入函数名称并选择“Node.js 12.x”运行时。然后，向下滚动并单击“创建函数”按钮。

![配置函数](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-function.png)

创建函数后，您应该会看到“函数代码”编辑器。在这个编辑器中，我们将添加我们的 Nest.js 应用程序代码。

首先，我们需要安装“@nestjs/aws-lambda”包。我们可以使用 `npm` 命令来做到这一点。

```
$ npm install --save @nestjs/aws-lambda
```

接下来，我们将把我们的 `main.ts` 文件添加到“函数代码”编辑器中。

![函数代码](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-function-code.png)

添加代码后，我们需要为函数选择“处理程序”。处理程序是我们的 Lambda 函数的入口点。在我们的例子中，处理程序是 `main.handler`。

![处理程序](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-handler.png)

现在我们已经配置了我们的功能，我们可以向下滚动并单击“保存”按钮。

![保存](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-save.png)

保存函数后，我们可以通过单击“测试”按钮对其进行测试。

![测试](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test.png)

在“配置测试事件”页面上，我们可以创建一个新的测试事件。在这种情况下，我们将把 `httpMethod` 设置为 `GET` 并将 `path` 设置为 `/`。然后，我们将单击“创建”按钮。

![配置测试事件](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-test-event.png)

创建测试事件后，我们可以单击“测试”按钮来运行我们的函数。

![test-2](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test-2.png)

如果一切顺利，您应该会看到带有“200”状态代码的“执行结果”部分。

![执行结果](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-execution-result.png)

## 结论

在本文中，我们向您展示了如何将 Nest.js 与 AWS Lambda 结合使用。我们创建了一个简单的 Nest.js 应用程序并将其部署到 AWS Lambda。