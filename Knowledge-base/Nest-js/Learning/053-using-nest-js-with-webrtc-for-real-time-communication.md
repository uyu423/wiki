---
title: 053: 실시간 통신을 위해 WebRTC와 함께 Nest.js 사용
description: 
published: true
date: 2023-02-06T23:55:58.357Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:55:56.698Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [053: Using Nest.js with WebRTC for real-time communication***English** document is available*](/en/Knowledge-base/Nest-js/Learning/053-using-nest-js-with-webrtc-for-real-time-communication)
{.links-list}


# 05: 실시간 통신을 위해 WebRTC와 함께 Nest.js 사용

WebRTC는 실시간 커뮤니케이션을 포함한 다양한 애플리케이션에 사용할 수 있는 강력한 도구입니다. Nest.js는 확장 가능한 애플리케이션을 구축하는 데 사용할 수 있는 Node.js 프레임워크입니다. 이 게시물에서는 WebRTC와 함께 Nest.js를 사용하여 실시간 통신 애플리케이션을 구축하는 방법을 보여줍니다.

## 전제 조건

시작하기 전에 따라가기 위해 필요한 몇 가지 사항이 있습니다. 먼저 Node.js와 npm이 설치되어 있어야 합니다. [Node.js](https://nodejs.org/en/download/) 및 [npm](https://www.npmjs.com/get-npm)에서 이를 수행하는 방법에 대한 지침을 찾을 수 있습니다.

다음으로 Nest.js CLI를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install -g @nestjs/cli
```

## Nest.js 프로젝트 만들기

이제 Nest.js CLI를 설치했으므로 이를 사용하여 새 Nest.js 프로젝트를 만들 수 있습니다. 이렇게 하려면 다음 명령을 실행합니다.

```
nest new project-name
```

"project-name"을 프로젝트 이름으로 바꿉니다. 그러면 동일한 이름의 새 디렉터리가 생성되고 그 안에 새 Nest.js 프로젝트가 초기화됩니다.

## 종속성 설치

이제 Nest.js 프로젝트가 있으므로 몇 가지 종속 항목을 설치해야 합니다. 필요한 첫 번째 종속 항목은 [Socket.io](https://socket.io/)입니다. Socket.io는 클라이언트와 서버 간의 통신을 처리하는 데 사용되는 실시간 통신 라이브러리입니다. 설치하려면 다음 명령을 실행하십시오.

```
npm install socket.io
```

다음으로 필요한 종속 항목은 [Express](https://expressjs.com/)입니다. Express는 클라이언트용 정적 파일을 제공하는 데 사용되는 Node.js용 웹 애플리케이션 프레임워크입니다. 설치하려면 다음 명령을 실행하십시오.

```
npm install express
```

## Socket.io 구성

종속성을 설치했으므로 이제 Socket.io를 구성해야 합니다. 이렇게 하려면 "src/main.ts" 파일을 열고 다음 코드를 추가합니다.

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as socketIo from 'socket.io';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  const server = app.getHttpServer();
  const io = socketIo(server);

  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('hbs');

  await app.listen(3000);
}
bootstrap();
```

이 코드는 Nest.js 서버를 사용하도록 Socket.io를 구성합니다. 또한 "public" 디렉토리의 정적 파일과 "views" 디렉토리의 보기를 제공하도록 Express를 구성합니다.

## 컨트롤러 만들기

이제 Socket.io가 구성되었으므로 컨트롤러를 만들 수 있습니다. 이렇게 하려면 다음 명령을 실행합니다.

```
nest generate controller controller-name
```

"controller-name"을 컨트롤러 이름으로 바꿉니다. 그러면 "controller-name.controller.ts"라는 이름으로 "src/controllers" 디렉토리에 새 파일이 생성됩니다.

"src/controllers/controller-name.controller.ts" 파일을 열고 다음 코드를 추가합니다.

```javascript
import { Controller, Post, Body, Req, UseGuards } from '@nestjs/common';
import { Socket } from 'socket.io';
import { AuthGuard } from '@nestjs/passport';

@Controller('controller-name')
export class ControllerNameController {

  @UseGuards(AuthGuard())
  @Post('message')
  async message(@Req() req, @Body() body, @Socket() socket: Socket) {
    socket.emit('message', body);
  }

}
```

이 코드는 단일 끝점이 있는 컨트롤러를 만듭니다. 끝점은 메시지 본문을 수락하는 POST 요청입니다. 그런 다음 메시지는 Socket.io를 사용하여 클라이언트로 내보내집니다.

## 보기 만들기

이제 컨트롤러를 만들었으므로 보기를 만들 수 있습니다. 이렇게 하려면 "views" 디렉토리에 "index.hbs"라는 이름으로 새 파일을 만듭니다. "index.hbs" 파일에 다음 코드를 추가합니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>WebRTC with Nest.js</title>
  </head>
  <body>
    <form id="form">
      <input type="text" id="message">
      <button type="submit">Send</button>
    </form>
    <div id="messages"></div>
    <script src="/socket.io/socket.io.js"></script>
    <script>
      const socket = io();
      const form = document.getElementById('form');
      const message = document.getElementById('message');
      const messages = document.getElementById('messages');

      form.addEventListener('submit', (e) => {
        e.preventDefault();
        socket.emit('message', message.value);
        message.value = '';
      });

      socket.on('message', (msg) => {
        const li = document.createElement('li');
        li.innerHTML = msg;
        messages.appendChild(li);
      });
    </script>
  </body>
</html>
```

이 코드는 사용자가 메시지를 입력할 수 있는 간단한 HTML 양식을 만듭니다. 그런 다음 메시지는 Socket.io를 사용하여 서버로 내보내집니다. 그런 다음 서버는 모든 클라이언트에 메시지를 내보냅니다. 메시지가 페이지에 표시됩니다.

## 애플리케이션 실행

이제 애플리케이션이 생성되었으므로 다음 명령을 실행하여 실행할 수 있습니다.

```
npm start
```

그런 다음 http://localhost:3000에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 게시물에서는 WebRTC와 함께 Nest.js를 사용하여 실시간 통신 애플리케이션을 구축하는 방법을 보여주었습니다. 또한 Socket.io를 사용하여 클라이언트와 서버 간의 통신을 처리하는 방법도 보여 주었습니다.