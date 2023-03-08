---
title: 052: 서버 전송 이벤트(SSE)와 함께 Nest.js 사용
description: 
published: true
date: 2023-02-05T18:55:21.291Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:55:19.661Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [052: Using Nest.js with Server-Sent Events (SSE)***English** document is available*](/en/Knowledge-base/Nest-js/Learning/052-using-nest-js-with-server-sent-events-sse)
{.links-list}


# 서버 전송 이벤트(SSE)와 함께 Nest.js 사용

이 게시물에서는 SSE(Server-Sent Events)와 함께 Nest.js를 사용하는 방법을 살펴보겠습니다. Nest.js는 서버 측 애플리케이션을 쉽게 구축할 수 있도록 도와주는 Node.js 프레임워크입니다. SSE는 실시간으로 서버에서 클라이언트로 데이터를 푸시할 수 있는 기술입니다.

Nest.js 프로젝트를 설정하는 것으로 시작하겠습니다. 그런 다음 SSE를 사용하여 클라이언트에 데이터를 푸시할 컨트롤러를 만듭니다. 마지막으로 서버에서 데이터를 수신할 클라이언트를 만듭니다.

## Nest.js 프로젝트 설정

먼저 새로운 Nest.js 프로젝트를 생성해 보겠습니다. Nest CLI를 사용하여 새 프로젝트를 생성할 수 있습니다. 다음 명령을 실행합니다.

```
nest new sse-project
```

이렇게 하면 `sse-project`라는 디렉토리에 새 Nest.js 프로젝트가 생성됩니다.

## 컨트롤러 만들기

다음으로 클라이언트에 데이터를 푸시할 컨트롤러를 만들어 보겠습니다. `src/controllers/data.controller.ts`라는 새 파일을 만들고 다음 코드를 추가합니다.

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';

@Controller('data')
export class DataController {
  @Get()
  getData(@Res() res: Response) {
    // Set the content type of the response to "text/event-stream"
    res.setHeader('Content-Type', 'text/event-stream');
    // Push some data to the client
    res.write('data: This is some data\n\n');
    // Close the connection
    res.end();
  }
}
```

이 컨트롤러에는 `@Get` 데코레이터로 장식된 `getData` 메서드가 있습니다. 이 메소드는 클라이언트가 `/data` 엔드포인트에 `GET` 요청을 할 때 호출됩니다.

`@Res` 데코레이터는 메소드에 `express` `Response` 객체를 주입합니다. 우리는 이 객체를 사용하여 `text/event-stream`에 대한 응답의 `Content-Type` 헤더를 설정하고 데이터를 클라이언트에 푸시합니다.

## 클라이언트 생성

이제 클라이언트에 데이터를 푸시할 수 있는 서버가 있으므로 데이터를 받을 수 있는 클라이언트를 생성해 보겠습니다. `client.html`이라는 새 파일을 만들고 다음 코드를 추가합니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>SSE Client</title>
  </head>
  <body>
    <h1>SSE Client</h1>
    <div id="data">
      <!-- Data from the server will be placed here -->
    </div>
    <script>
      const source = new EventSource('http://localhost:3000/data');
      source.onmessage = (event) => {
        const data = event.data;
        document.getElementById('data').innerHTML = data;
      };
    </script>
  </body>
</html>
```

이 파일에는 `id`가 `data`인 `<div>` 요소가 있습니다. 여기에 서버의 데이터가 배치됩니다.

또한 새로운 `EventSource` 객체를 생성하는 `<script>` 요소도 있습니다. 이 개체는 서버의 `/data` 끝점에 연결됩니다. 그런 다음 서버가 클라이언트에 데이터를 푸시할 때 호출될 `onmessage` 이벤트 핸들러를 등록합니다.

## 애플리케이션 실행

이제 서버와 클라이언트가 있으므로 애플리케이션을 실행해 보겠습니다. 먼저 다음 명령을 실행하여 서버를 시작합니다.

```
nest start
```

그런 다음 브라우저에서 `client.html` 파일을 엽니다. 브라우저에 표시되는 서버의 데이터를 확인해야 합니다.