---
title: 062：在Nest.js中实现文件上传下载
description: 
published: true
date: 2023-02-04T00:18:00.714Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:17:59.001Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [062: Implementing file uploads and downloads in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/062-implementing-file-uploads-and-downloads-in-nest-js)
{.links-list}


# 062: 在 Nest.js 中实现文件上传和下载

## 介绍

在许多网络应用程序中，需要允许用户上传和下载文件。例如，用户可能想要上传一张图片用作他们的个人资料图片，或者下载应用程序生成的 PDF 文档。

在这篇文章中，我们将看看如何在 Nest.js 应用程序中实现文件上传和下载。我们将从了解如何上传文件开始，然后我们将了解如何下载文件。

## 上传文件

在 Nest.js 中上传文件主要有两种方式：使用 `multer` 模块或 `Nest.js uploadFile` 方法。

### 使用 `multer` 模块

`multer` 模块是在 Node.js 应用程序中处理文件上传的一个流行选项。它易于使用并且具有广泛的功能。

要使用 `multer`，您首先需要从 npm 安装它：

```
npm install multer
```

安装 `multer` 后，您可以像这样在 Nest.js 应用程序中使用它：

```javascript
// src/app.controller.ts

import { Controller, Post, UseInterceptors, UploadedFile } from '@nestjs/common';
import { FileInterceptor } from '@nestjs/platform-express';

@Controller()
export class AppController {

  @Post('/upload')
  @UseInterceptors(FileInterceptor('file'))
  uploadFile(@UploadedFile() file) {
    console.log(file);
  }
}
```

在上面的代码中，我们定义了一个带有 `/upload` 端点的控制器来接受文件上传。我们还添加了 `@UseInterceptors` 装饰器以使用 `FileInterceptor` Nest.js 拦截器，用于处理文件上传。

`FileInterceptor` 拦截器接受一个 `name` 参数，这是包含文件的表单字段的名称。在我们的示例中，表单字段的名称是 `file`。

最后，我们将 @UploadedFile 装饰器添加到 uploadFile 方法的 file 参数中。此装饰器用于获取有关上传文件的信息。

如果我们运行应用程序并上传文件，我们应该看到以下输出：

```
{ fieldname: 'file',
  originalname: 'test.txt',
  encoding: '7bit',
  mimetype: 'text/plain',
  buffer: <Buffer 74 65 73 74 0d 0a>,
  size: 9 }
```

如您所见，@UploadedFile 装饰器为我们提供了有关上传文件的信息，例如原始名称和 mimetype。

### 使用 `Nest.js uploadFile` 方法

在 Nest.js 中上传文件的另一种选择是使用 `Nest.js uploadFile` 方法。此方法是 @nestjs/common 包的一部分，这意味着您不需要安装任何额外的依赖项。

要使用 `Nest.js uploadFile` 方法，您首先需要在控制器中创建一个 `uploadFile` 方法：

```javascript
// src/app.controller.ts

import { Controller, Post, Body, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  @Post('/upload')
  @HttpCode(HttpStatus.OK)
  uploadFile(@Body() body) {
    console.log(body);
  }
}
```

在上面的代码中，我们定义了一个带有 `/upload` 端点的控制器来接受文件上传。我们还添加了“@HttpCode”装饰器以将 HTTP 状态代码设置为“200”，以及“@Body”装饰器以获取请求正文。

接下来，我们需要在我们的服务中创建一个 `uploadFile` 方法：

```javascript
// src/app.service.ts

import { Injectable } from '@nestjs/common';
import { HttpService, HttpStatus, } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AppService {
  constructor(
    private readonly httpService: HttpService,
    private readonly configService: ConfigService,
  ) {}

  async uploadFile(file: any) {
    const formData = new FormData();
    formData.append('file', file);

    try {
      const response = await this.httpService.post(
        `${this.configService.get('API_URL')}/upload`,
        formData,
      ).toPromise();

      return response.data;
    } catch (error) {
      throw new HttpException('Internal server error', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
}
```

在上面的代码中，我们将 `HttpService` 和 `ConfigService` 注入到我们的 `AppService` 中。我们还创建了一个接受 file 参数的 uploadFile 方法。

此方法创建一个 `FormData` 对象，用于将文件提交到 `/upload` 端点。我们还添加了一个 try/catch 块来捕获发生的任何错误。

最后，我们需要从控制器调用 uploadFile 方法：

```javascript
// src/app.controller.ts

import { Controller, Post, Body, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  constructor(private readonly appService: AppService) {}

  @Post('/upload')
  @HttpCode(HttpStatus.OK)
  uploadFile(@Body() body) {
    this.appService.uploadFile(body);
  }
}
```

在上面的代码中，我们将 `AppService` 注入了我们的控制器。我们还创建了一个 uploadFile 方法，它从我们的服务中调用 uploadFile 方法。

如果我们运行应用程序并上传文件，我们应该看到以下输出：

```
{ file:
   { fieldname: 'file',
     originalname: 'test.txt',
     encoding: '7bit',
     mimetype: 'text/plain',
     buffer: <Buffer 74 65 73 74 0d 0a>,
     size: 9 } }
```

如您所见，`Nest.js uploadFile` 方法为我们提供了有关上传文件的信息，例如原始名称和 mimetype。

## 下载文件

在 Nest.js 中下载文件主要有两种方式：使用`Nest.js downloadFile` 方法或`Nest.js sendFile` 方法。

### 使用 `Nest.js downloadFile` 方法

`Nest.js downloadFile` 方法是 `@nestjs/common` 包的一部分，这意味着您不需要安装任何额外的依赖项。

要使用 `Nest.js downloadFile` 方法，您首先需要在控制器中创建一个 `downloadFile` 方法：

```javascript
// src/app.controller.ts

import { Controller, Get, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile() {
    const file = `${__dirname}/../../test.txt`;
    return this.appService.downloadFile(file);
  }
}
```

在上面的代码中，我们定义了一个带有“/download”端点的控制器，该端点返回一个文件。我们还添加了“@HttpCode”装饰器以将 HTTP 状态代码设置为“200”。

接下来，我们需要在我们的服务中创建一个 `downloadFile` 方法：

```javascript
// src/app.service.ts

import { Injectable } from '@nestjs/common';
import { HttpService, HttpStatus, } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AppService {
  constructor(
    private readonly httpService: HttpService,
    private readonly configService: ConfigService,
  ) {}

  async downloadFile(file: string) {
    try {
      const response = await this.httpService.get(
        `${this.configService.get('API_URL')}/download?file=${file}`,
        {
          responseType: 'arraybuffer',
          headers: {
            'Content-Type': 'application/octet-stream',
            'Content-Disposition': `attachment; filename=${file}`,
          },
        },
      ).toPromise();

      return response.data;
    } catch (error) {
      throw new HttpException('Internal server error', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
}
```

在上面的代码中，我们将 `HttpService` 和 `ConfigService` 注入到我们的 `AppService` 中。我们还创建了一个接受 file 参数的 downloadFile 方法。

此方法使用 `file` 查询参数向 `/download` 端点发出 GET 请求。我们还添加了一个 try/catch 块来捕获发生的任何错误。

最后，我们需要从我们的控制器中调用 `downloadFile` 方法：

```javascript
// src/app.controller.ts

import { Controller, Get, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  constructor(private readonly appService: AppService) {}

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile() {
    const file = `${__dirname}/../../test.txt`;
    return this.appService.downloadFile(file);
  }
}
```

在上面的代码中，我们将 `AppService` 注入了我们的控制器。我们还创建了一个 downloadFile 方法，它从我们的服务中调用 downloadFile 方法。

如果我们运行应用程序并访问 `/download` 端点，我们应该看到 `test.txt` 文件的内容。

### 使用 `Nest.js sendFile` 方法

在 Nest.js 中下载文件的另一种选择是使用 `Nest.js sendFile` 方法。此方法是 @nestjs/common 包的一部分，这意味着您不需要安装任何额外的依赖项。

要使用 `Nest.js sendFile` 方法，您首先需要在控制器中创建一个 `sendFile` 方法：

```javascript
// src/app.controller.ts

import { Controller, Get, Res, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile(@Res() res) {
    const file = `${__dirname}/../../test.txt`;
    return res.sendFile(file);
  }
}
```

在上面的代码中，我们定义了一个带有“/download”端点的控制器，该端点返回一个文件。我们还添加了“@HttpCode”装饰器以将 HTTP 状态代码设置为“200”，以及“@Res”装饰器以获取响应对象。

接下来，我们需要在我们的服务中创建一个 sendFile 方法：

```javascript
// src/app.service.ts

import { Injectable } from '@nestjs/common';
import { HttpService, HttpStatus, } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AppService {
  constructor(
    private readonly httpService: HttpService,
    private readonly configService: ConfigService,
  ) {}

  async sendFile(file: string) {
    try {
      const response = await this.httpService.get(
        `${this.configService.get('API_URL')}/download?file=${file}`,
        {
          responseType: 'arraybuffer',
          headers: {
            'Content-Type': 'application/octet-stream',
            'Content-Disposition': `attachment; filename=${file}`,
          },
        },
      ).toPromise();

      return response.data;
    } catch (error) {
      throw new HttpException('Internal server error', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
}
```

在上面的代码中，我们将 `HttpService` 和 `ConfigService` 注入到我们的 `AppService` 中。我们还创建了一个接受 file 参数的 sendFile 方法。

此方法使用 `file` 查询参数向 `/download` 端点发出 GET 请求。我们还添加了一个 try/catch 块来捕获发生的任何错误。

最后，我们需要从控制器调用 sendFile 方法：

```javascript
// src/app.controller.ts

import { Controller, Get, Res, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  constructor(private readonly appService: AppService) {}

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile(@Res() res) {
    const file = `${__dirname}/../../test.txt`;
    return this.appService.sendFile(file);
  }
}
```

在上面的代码中，我们将 `AppService` 注入了我们的控制器。我们还创建了一个 downloadFile 方法，它从我们的服务中调用 sendFile 方法。

如果我们运行应用程序并访问 `/download` 端点，我们应该看到 `test.txt` 文件的内容。

## 结论

在本文中，我们了解了如何在 Nest.js 应用程序中实现文件上传和下载。

我们研究了两种不同的文件上传方式：使用 `multer` 模块或 `Nest.js uploadFile` 方法。我们还研究了两种不同的文件下载方式：使用 `Nest.js downloadFile` 方法或 `Nest.js sendFile` 方法。

您选择哪种方法取决于您的具体需求。