---
title: 실시간 통신을 위한 Node.js 및 WebSockets 작업
description: 
published: true
date: 2023-02-17T01:55:39.089Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:55:30.792Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Working with Node.js and WebSockets for Real-Time Communication***English** document is available*](/en/Knowledge-base/Nodejs/working-with-node-js-and-websockets-for-real-time-communication)
{.links-list}


      IT 개발 학습 블로그

# 실시간 통신을 위한 Node.js 및 WebSockets 작업

Node.js는 브라우저 외부에서 Javascript 코드를 실행할 수 있는 Javascript 런타임 환경입니다. 다목적이며 서버 측 응용 프로그램, 명령줄 도구 및 데스크톱 응용 프로그램을 개발하는 데 사용할 수 있습니다.

WebSockets는 클라이언트와 서버 간의 전이중 양방향 통신을 허용하는 웹 기술입니다. 실시간 통신을 위해 설계되었으며 채팅 응용 프로그램, 공동 편집 응용 프로그램 및 게임 응용 프로그램과 같은 응용 프로그램에서 자주 사용됩니다.

이 기사에서는 실시간 통신을 위해 Node.js 및 WebSocket을 사용하는 방법을 살펴봅니다. WebSocket 요청을 처리할 수 있는 Node.js 서버를 설정하는 방법에 대해 설명하고 실시간 통신을 위해 WebSocket을 사용하는 간단한 채팅 애플리케이션도 빌드합니다.

## Node.js 서버 설정

Node.js에서 WebSocket 작업을 위해 [ws](https://www.npmjs.com/package/ws) npm 패키지를 사용할 것입니다.

먼저 `ws` 패키지를 설치해야 합니다.

```
npm install ws
```

다음으로 `server.js`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });

  ws.send('Hello!');
});
```

위의 코드에서 우리는 `ws` 패키지를 사용하여 포트 8080에 WebSocket 서버를 생성하고 있습니다. 또한 클라이언트가 서버에 연결할 때 발생하는 `connection` 이벤트도 처리하고 있습니다. 연결이 설정되면 클라이언트에서 메시지를 수신할 때 발생하는 `message` 이벤트에 대한 이벤트 핸들러를 설정합니다. 마지막으로 연결이 설정되면 클라이언트에 메시지를 보냅니다.

서버를 실행하려면 다음 명령을 사용할 수 있습니다.

```
node server.js
```

## 채팅 애플리케이션 만들기

이제 WebSocket 요청을 처리할 수 있는 Node.js 서버가 있으므로 실시간 통신을 위해 WebSocket을 사용하는 간단한 채팅 애플리케이션을 빌드해 보겠습니다.

먼저 `client.html`이라는 파일을 만들고 다음 코드를 추가해야 합니다.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>WebSocket Chat</title>
</head>
<body>
  <h1>WebSocket Chat</h1>
  <form id="form">
    <label for="message">Message:</label>
    <input type="text" id="message" />
    <input type="submit" value="Send" />
  </form>
  <ul id="messages"></ul>
  <script>
    const form = document.getElementById('form');
    const messages = document.getElementById('messages');
    const message = document.getElementById('message');

    const ws = new WebSocket('ws://localhost:8080');

    ws.onopen = () => {
      console.log('Connected');
    };

    ws.onmessage = (event) => {
      const li = document.createElement('li');
      li.innerText = event.data;
      messages.appendChild(li);
    };

    ws.onerror = (error) => {
      console.log(error);
    };

    ws.onclose = () => {
      console.log('Disconnected');
    };

    form.addEventListener('submit', (event) => {
      event.preventDefault();

      ws.send(message.value);
      message.value = '';
    });
  </script>
</body>
</html>
```

위의 코드에서는 HTML과 Javascript를 사용하여 간단한 채팅 애플리케이션을 만들고 있습니다. 우리는 `WebSocket` API를 사용하여 서버와의 연결을 설정하고 `message` 이벤트를 사용하여 서버에서 메시지를 수신하고 브라우저에 표시합니다. 또한 `send` 메서드를 사용하여 서버에 메시지를 보냅니다.

## 결론

이 기사에서는 실시간 통신을 위해 Node.js 및 WebSocket을 사용하는 방법을 살펴보았습니다. 우리는 WebSocket 요청을 처리할 수 있는 Node.js 서버를 설정했으며 실시간 통신을 위해 WebSocket을 사용하는 간단한 채팅 애플리케이션도 구축했습니다.