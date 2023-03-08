---
title: TypeScript 및 WebSocket으로 실시간 애플리케이션 만들기
description: 
published: true
date: 2023-01-31T10:57:33.922Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:57:32.374Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Creating Real-Time Applications with TypeScript and WebSockets***English** version of this document is available*](/en/Knowledge-base/TypeScript/creating-real-time-applications-with-typescript-and-websockets)
{.links-list}



# TypeScript와 WebSocket으로 실시간 애플리케이션 만들기

WebSocket은 실시간 애플리케이션을 만들기 위한 강력한 도구입니다. TypeScript와 결합하면 정적 유형 검사, 코드 완성 등을 통해 훌륭한 개발 경험을 제공할 수 있습니다. 이 기사에서는 TypeScript와 WebSocket을 사용하여 간단한 채팅 애플리케이션을 만드는 방법을 살펴보겠습니다.

## WebSocket이 무엇인가요?

WebSocket은 기존 TCP 연결을 통해 양방향 실시간 통신 채널을 만드는 기술입니다. 모든 주요 브라우저에서 지원되며 간단한 채팅 클라이언트에서 복잡한 멀티플레이어 게임에 이르기까지 다양한 애플리케이션을 만드는 데 사용할 수 있습니다.

## 시작하기

시작하려면 WebSocket 연결을 처리할 수 있는 서버를 설정해야 합니다. 이 기사에서는 널리 사용되는 Node.js 프레임워크인 Express를 사용합니다.

먼저 프로젝트의 새 디렉터리를 만들고 종속 항목을 설치합니다.

```
mkdir chat-app
cd chat-app
npm init -y
npm install --save express
npm install --save ws
```

다음으로 서버 코드용 파일을 만듭니다.

```
touch server.js
```

그리고 다음 코드를 붙여넣습니다.

```javascript
const express = require('express');
const WebSocket = require('ws');

const app = express();

const PORT = process.env.PORT || 8080;

const server = app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});

const wss = new WebSocket.Server({ server });

wss.on('connection', (ws) => {
  console.log('Client connected');

  ws.on('message', (message) => {
    console.log(`Received message: ${message}`);
  });

  ws.send('Hello!');
});
```

여기서 무슨 일이 일어나고 있는지 분석해 봅시다. 먼저 Express 및 WebSocket 모듈이 필요합니다. 다음으로 Express 서버를 만들고 포트 8080에서 수신 대기하도록 구성합니다. 그런 다음 Express 서버를 'server' 옵션으로 전달하여 새 WebSocket 서버를 만듭니다.

다음으로 클라이언트가 WebSocket 서버에 연결할 때를 위한 이벤트 핸들러를 설정합니다. 클라이언트가 연결되면 콘솔에 메시지를 기록합니다. 그런 다음 클라이언트가 메시지를 보낼 때 이벤트 핸들러를 설정합니다. 메시지가 수신되면 다시 콘솔에 기록합니다. 마지막으로 클라이언트에게 메시지를 보냅니다.

서버를 실행하려면 node 명령을 사용할 수 있습니다.

```
node server.js
```

## 클라이언트 생성

이제 서버가 가동되어 실행 중이므로 클라이언트를 생성해 보겠습니다. 이 기사에서는 널리 사용되는 React 프레임워크를 사용할 것입니다.

먼저 종속 항목을 설치해야 합니다.

```
npm install --save react
npm install --save react-dom
npm install --save @types/react
npm install --save @types/react-dom
npm install --save ws
npm install --save @types/ws
```

그런 다음 클라이언트 코드용 파일을 만듭니다.

```
touch client.js
```

그리고 다음 코드를 붙여넣습니다.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import * as ws from 'ws';

const socket = new ws('ws://localhost:8080');

socket.onopen = () => {
  console.log('Connected to server');
};

socket.onmessage = (event) => {
  console.log(event.data);
};

socket.send('Hello from the client!');

ReactDOM.render(
  <div>Hello, world!</div>,
  document.getElementById('root')
);
```

먼저 React 및 ReactDOM 모듈을 가져옵니다. 그런 다음 WebSocket 모듈을 가져옵니다. 다음으로 서버의 URL을 전달하여 새 WebSocket 인스턴스를 만듭니다.

그런 다음 소켓이 열리는 시점과 메시지가 수신되는 시점에 대한 이벤트 핸들러를 설정합니다. 소켓이 열리면 콘솔에 메시지를 기록합니다. 메시지가 수신되면 다시 콘솔에 기록합니다. 마지막으로 서버에 메시지를 보냅니다.

## 결론

이 기사에서는 TypeScript와 WebSocket을 사용하여 간단한 채팅 애플리케이션을 만드는 방법을 살펴보았습니다. 이 예제는 간단하지만 실시간 애플리케이션을 생성하기 위한 WebSocket의 기능을 보여줍니다.