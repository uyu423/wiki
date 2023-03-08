---
title: TypeScript 및 WebSocket으로 실시간 채팅 애플리케이션 구축
description: 
published: true
date: 2023-02-24T20:32:44.018Z
tags: 
editor: markdown
dateCreated: 2023-02-24T20:32:42.618Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Real-Time Chat Applications with TypeScript and WebSockets***English** document is available*](/en/Knowledge-base/TypeScript/building-real-time-chat-applications-with-typescript-and-websockets)
{.links-list}


# TypeScript 및 WebSocket으로 실시간 채팅 애플리케이션 구축

WebSocket은 클라이언트와 서버 간의 양방향 실시간 통신을 가능하게 하는 비교적 새로운 기술입니다. 사용자에게 실시간 몰입형 경험을 제공하기 위해 일반적으로 채팅 애플리케이션에서 사용됩니다.

WebSocket은 채팅 응용 프로그램에 적합하지만 게임, 협업 및 알림 응용 프로그램과 같이 클라이언트와 서버 간의 실시간 통신이 필요한 다른 유형의 응용 프로그램에도 사용할 수 있습니다.

이 기사에서는 TypeScript 및 WebSocket을 사용하여 실시간 채팅 애플리케이션을 구축하는 방법을 보여줍니다. 우리는 Node.js WebSocket 라이브러리 ws와 Express 웹 프레임워크를 사용할 것입니다.

## 시작하기

시작하기 전에 사용할 종속성을 설치해야 합니다. 우리는 Node.js WebSocket 라이브러리 ws와 Express 웹 프레임워크를 사용할 것입니다.

이러한 종속성을 설치하려면 다음 명령을 사용할 수 있습니다.

```
npm install --save ws express
```

## 서버 생성

종속성을 설치했으므로 이제 서버를 만들 수 있습니다. 먼저 server.ts라는 파일을 만들고 다음 코드를 추가합니다.

```typescript
import * as WebSocket from 'ws';
import * as express from 'express';

const app = express();

const server = app.listen(8080, () => {
    console.log('Server is listening on port 8080');
});

const wss = new WebSocket.Server({ server });
```

이 코드를 분해하여 무엇을 하는지 살펴보겠습니다. WebSocket 및 익스프레스 모듈을 가져오는 것으로 시작합니다. 그런 다음 익스프레스 애플리케이션의 인스턴스를 생성하고 포트 8080에서 수신 대기하는 서버를 생성합니다.

마지막으로 WebSocket 서버의 인스턴스를 생성합니다. 연결된 모든 클라이언트에 메시지를 브로드캐스트하는 데 사용됩니다.

## 클라이언트 연결

이제 서버를 설정했으므로 서버에 연결할 수 있는 클라이언트를 만들어야 합니다. 먼저 client.ts라는 파일을 만들고 다음 코드를 추가합니다.

```typescript
import * as WebSocket from 'ws';

const ws = new WebSocket('ws://localhost:8080');

ws.on('open', () => {
    console.log('Connected to server');
});

ws.on('message', (message: string) => {
    console.log(`Received message from server: ${message}`);
});
```

이전에 WebSocket을 사용해 본 적이 있다면 이 코드가 익숙할 것입니다. WebSocket 인스턴스를 생성하여 시작하고 서버에 연결합니다. 그런 다음 열기 및 메시지 이벤트에 대한 이벤트 핸들러를 설정합니다.

연결이 설정되면 open 이벤트가 시작되고 서버에서 메시지를 수신하면 message 이벤트가 시작됩니다.

## 메시지 보내기

이제 서버와 클라이언트가 설정되었으므로 이들 간에 메시지를 보낼 수 있습니다.

먼저 server.ts 파일에 다음 코드를 추가합니다.

```typescript
wss.on('connection', (ws: WebSocket) => {
    ws.on('message', (message: string) => {
        console.log(`Received message from client: ${message}`);

        // Broadcast the message to all connected clients
        wss.clients.forEach((client: WebSocket) => {
            if (client != ws) {
                client.send(message);
            }
        });
    });
});
```

이 코드는 연결 이벤트에 대한 이벤트 핸들러를 설정합니다. 이 이벤트는 클라이언트가 서버에 연결할 때 시작됩니다.

그런 다음 메시지 이벤트에 대한 다른 이벤트 핸들러를 설정합니다. 이 이벤트는 클라이언트에서 메시지를 받으면 시작됩니다.

마지막으로 서버에 연결된 모든 클라이언트를 반복하고 메시지를 보낸 클라이언트를 제외한 모든 클라이언트에게 메시지를 보냅니다. 이렇게 하면 연결된 모든 클라이언트에 메시지가 브로드캐스트됩니다.

이제 client.ts 파일에 다음 코드를 추가하면:

```typescript
ws.send('Hello, world!');
```

콘솔에 다음 출력이 표시됩니다.

```
Connected to server
Received message from server: Hello, world!
```

## 결론

이 기사에서는 TypeScript 및 WebSocket을 사용하여 실시간 채팅 애플리케이션을 구축하는 방법을 보여주었습니다. 또한 연결된 모든 클라이언트에 메시지를 브로드캐스트하는 방법도 보여 주었습니다.

TypeScript 및 WebSocket에 대해 자세히 알아보려면 다음 리소스를 확인할 수 있습니다.

- [TypeScript 핸드북](https://www.typescriptlang.org/docs/handbook/basic-types.html)
- [WebSockets 튜토리얼](https://www.tutorialspoint.com/websockets/index.htm)
- [Node.js로 WebSocket 서버 구축하기](https://www.sitepoint.com/websockets-node-js/)