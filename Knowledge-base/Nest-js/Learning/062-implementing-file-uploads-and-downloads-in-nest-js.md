---
title: 062: Nest.js에서 파일 업로드 및 다운로드 구현
description: 
published: true
date: 2023-02-04T00:18:00.854Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:17:59.001Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [062: Implementing file uploads and downloads in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/062-implementing-file-uploads-and-downloads-in-nest-js)
{.links-list}


# 062: Nest.js에서 파일 업로드 및 다운로드 구현

## 소개

많은 웹 애플리케이션에서 사용자가 파일을 업로드하고 다운로드할 수 있도록 허용해야 합니다. 예를 들어 사용자는 프로필 사진으로 사용할 이미지를 업로드하거나 애플리케이션에서 생성한 PDF 문서를 다운로드할 수 있습니다.

이 게시물에서는 Nest.js 애플리케이션에서 파일 업로드 및 다운로드를 구현하는 방법을 살펴보겠습니다. 먼저 파일을 업로드하는 방법을 살펴본 다음 파일을 다운로드하는 방법을 살펴보겠습니다.

## 파일 업로드

Nest.js에서 파일을 업로드하는 두 가지 주요 방법은 `multer` 모듈 또는 ` Nest.js uploadFile` 방법을 사용하는 것입니다.

### `multer` 모듈 사용

`multer` 모듈은 Node.js 애플리케이션에서 파일 업로드를 처리하는 데 널리 사용되는 옵션입니다. 사용하기 쉽고 다양한 기능이 있습니다.

`multer`를 사용하려면 먼저 npm에서 설치해야 합니다.

```
npm install multer
```

`multer`가 설치되면 다음과 같이 Nest.js 애플리케이션에서 사용할 수 있습니다.

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

위의 코드에서 파일 업로드를 허용하는 `/upload` 엔드포인트가 있는 컨트롤러를 정의했습니다. 파일 업로드를 처리하는 데 사용되는 `FileInterceptor` Nest.js 인터셉터를 사용하기 위해 `@UseInterceptors` 데코레이터도 추가했습니다.

`FileInterceptor` 인터셉터는 파일을 포함하는 양식 필드의 이름인 `name` 매개변수를 허용합니다. 이 예에서 양식 필드의 이름은 `file`입니다.

마지막으로 `uploadFile` 메서드의 `file` 매개변수에 `@UploadedFile` 데코레이터를 추가했습니다. 이 데코레이터는 업로드된 파일에 대한 정보를 얻는 데 사용됩니다.

애플리케이션을 실행하고 파일을 업로드하면 다음 출력이 표시됩니다.

```
{ fieldname: 'file',
  originalname: 'test.txt',
  encoding: '7bit',
  mimetype: 'text/plain',
  buffer: <Buffer 74 65 73 74 0d 0a>,
  size: 9 }
```

보시다시피 `@UploadedFile` 데코레이터는 원본 이름 및 mimetype과 같은 업로드된 파일에 대한 정보를 제공합니다.

### `Nest.js uploadFile` 메서드 사용

Nest.js에서 파일을 업로드하는 또 다른 옵션은 `Nest.js uploadFile` 메서드를 사용하는 것입니다. 이 방법은 `@nestjs/common` 패키지의 일부이므로 추가 종속성을 설치할 필요가 없습니다.

`Nest.js uploadFile` 메서드를 사용하려면 먼저 컨트롤러에서 `uploadFile` 메서드를 생성해야 합니다.

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

위의 코드에서 파일 업로드를 허용하는 `/upload` 엔드포인트가 있는 컨트롤러를 정의했습니다. 또한 HTTP 상태 코드를 `200`으로 설정하는 `@HttpCode` 데코레이터와 요청 본문을 가져오는 `@Body` 데코레이터를 추가했습니다.

다음으로 서비스에서 ` uploadFile` 메서드를 만들어야 합니다.

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

위의 코드에서 `HttpService` 및 `ConfigService`를 `AppService`에 삽입했습니다. 또한 `file` 매개변수를 허용하는 `uploadFile` 메소드도 생성했습니다.

이 메서드는 `/upload` 엔드포인트에 파일을 제출하는 데 사용되는 `FormData` 객체를 생성합니다. 발생하는 모든 오류를 포착하기 위해 try/catch 블록도 추가했습니다.

마지막으로 컨트롤러에서 `uploadFile` 메서드를 호출해야 합니다.

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

위의 코드에서 컨트롤러에 `AppService`를 삽입했습니다. 또한 서비스에서 `uploadFile` 메서드를 호출하는 `uploadFile` 메서드를 만들었습니다.

애플리케이션을 실행하고 파일을 업로드하면 다음 출력이 표시됩니다.

```
{ file:
   { fieldname: 'file',
     originalname: 'test.txt',
     encoding: '7bit',
     mimetype: 'text/plain',
     buffer: <Buffer 74 65 73 74 0d 0a>,
     size: 9 } }
```

보시다시피 `Nest.js uploadFile` 메서드는 원래 이름 및 mimetype과 같은 업로드된 파일에 대한 정보를 제공합니다.

## 파일 다운로드 중

Nest.js에서 파일을 다운로드하는 두 가지 주요 방법은 ` Nest.js downloadFile` 방법 또는 `Nest.js sendFile` 방법을 사용하는 것입니다.

### `Nest.js downloadFile` 메서드 사용

`Nest.js downloadFile` 메서드는 `@nestjs/common` 패키지의 일부이므로 추가 종속성을 설치할 필요가 없습니다.

`Nest.js downloadFile` 메서드를 사용하려면 먼저 컨트롤러에서 `downloadFile` 메서드를 생성해야 합니다.

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

위의 코드에서 파일을 반환하는 `/download` 엔드포인트가 있는 컨트롤러를 정의했습니다. 또한 HTTP 상태 코드를 `200`으로 설정하기 위해 `@HttpCode` 데코레이터를 추가했습니다.

다음으로 서비스에서 `downloadFile` 메서드를 생성해야 합니다.

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

위의 코드에서 `HttpService` 및 `ConfigService`를 `AppService`에 삽입했습니다. 또한 `file` 매개변수를 허용하는 `downloadFile` 메소드도 생성했습니다.

이 메서드는 `file` 쿼리 매개변수를 사용하여 `/download` 엔드포인트에 대한 GET 요청을 만듭니다. 발생하는 모든 오류를 포착하기 위해 try/catch 블록도 추가했습니다.

마지막으로 컨트롤러에서 `downloadFile` 메서드를 호출해야 합니다.

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

위의 코드에서 컨트롤러에 `AppService`를 삽입했습니다. 또한 서비스에서 `downloadFile` 메서드를 호출하는 `downloadFile` 메서드를 만들었습니다.

애플리케이션을 실행하고 `/download` 엔드포인트를 방문하면 `test.txt` 파일의 내용이 표시되어야 합니다.

### `Nest.js sendFile` 메소드 사용

Nest.js에서 파일을 다운로드하는 또 다른 옵션은 `Nest.js sendFile` 메서드를 사용하는 것입니다. 이 방법은 `@nestjs/common` 패키지의 일부이므로 추가 종속성을 설치할 필요가 없습니다.

`Nest.js sendFile` 메서드를 사용하려면 먼저 컨트롤러에서 `sendFile` 메서드를 생성해야 합니다.

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

위의 코드에서 파일을 반환하는 `/download` 엔드포인트가 있는 컨트롤러를 정의했습니다. 또한 HTTP 상태 코드를 `200`으로 설정하는 `@HttpCode` 데코레이터와 응답 객체를 가져오는 `@Res` 데코레이터를 추가했습니다.

다음으로 서비스에서 `sendFile` 메서드를 생성해야 합니다.

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

위의 코드에서 `HttpService` 및 `ConfigService`를 `AppService`에 삽입했습니다. 또한 `file` 매개변수를 허용하는 `sendFile` 메소드도 생성했습니다.

이 메서드는 `file` 쿼리 매개변수를 사용하여 `/download` 엔드포인트에 대한 GET 요청을 만듭니다. 발생하는 모든 오류를 포착하기 위해 try/catch 블록도 추가했습니다.

마지막으로 컨트롤러에서 `sendFile` 메서드를 호출해야 합니다.

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

위의 코드에서 컨트롤러에 `AppService`를 삽입했습니다. 또한 서비스에서 `sendFile` 메서드를 호출하는 `downloadFile` 메서드를 만들었습니다.

애플리케이션을 실행하고 `/download` 엔드포인트를 방문하면 `test.txt` 파일의 내용이 표시되어야 합니다.

## 결론

이 게시물에서는 Nest.js 애플리케이션에서 파일 업로드 및 다운로드를 구현하는 방법을 살펴보았습니다.

파일을 업로드하는 두 가지 다른 방법인 `multer` 모듈 또는 `Nest.js uploadFile` 방법을 살펴보았습니다. 또한 파일을 다운로드하는 두 가지 다른 방법인 `Nest.js downloadFile` 방법 또는 `Nest.js sendFile` 방법을 살펴보았습니다.

선택하는 방법은 특정 요구 사항에 따라 다릅니다.