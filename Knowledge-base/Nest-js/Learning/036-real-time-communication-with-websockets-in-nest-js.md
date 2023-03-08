---
title: 036: Nest.js에서 WebSocket과 실시간 통신
description: 
published: true
date: 2023-02-08T11:56:10.497Z
tags: 
editor: markdown
dateCreated: 2023-02-08T11:56:08.839Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [036: Real-time communication with WebSockets in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/036-real-time-communication-with-websockets-in-nest-js)
{.links-list}


# Nest.js에서 WebSocket과 실시간 통신

WebSocket은 단일 TCP 연결을 통해 전이중 통신 채널을 제공하는 컴퓨터 통신 프로토콜입니다. WebSocket 프로토콜은 2011년에 표준화되었으며 Web IDL의 WebSocket API는 W3C에서 표준화되고 있습니다.

WebSocket은 웹 브라우저와 웹 서버에서 구현되도록 설계되었지만 모든 클라이언트 또는 서버 애플리케이션에서 사용할 수 있습니다. WebSocket 프로토콜은 브라우저와 웹 사이트 간의 더 많은 상호 작용을 가능하게 하여 라이브 콘텐츠와 실시간 게임 생성을 용이하게 합니다. 이는 클라이언트가 요청하지 않고 서버가 브라우저에 콘텐츠를 보낼 수 있는 표준화된 방법을 제공하고 연결을 열린 상태로 유지하면서 메시지를 앞뒤로 전달할 수 있도록 함으로써 가능합니다. 이러한 방식으로 브라우저와 서버 간에 양방향(양방향) 진행 중인 대화가 발생할 수 있습니다.

## WebSocket은 어떻게 작동하나요?

WebSocket은 클라이언트와 서버 간에 오래 유지되는(양방향) TCP 소켓 연결을 사용합니다. 연결이 설정되면 클라이언트나 서버가 연결을 닫기로 결정할 때까지 열린 상태로 유지됩니다. 이는 일반적으로 각 요청/응답 주기 후에 닫히는 일반적인 HTTP 연결과 다릅니다.

업그레이드 헤더가 있는 HTTP 요청에 의해 WebSocket 연결이 시작됩니다. 클라이언트는 일반 HTTP 연결에서 WebSocket으로의 연결 업그레이드를 요청하는 요청을 서버에 보냅니다. 서버가 연결 업그레이드에 동의하면 업그레이드 헤더가 포함된 HTTP 응답으로 응답합니다. 연결이 업그레이드되면 클라이언트와 서버는 양방향으로 서로 데이터를 보낼 수 있습니다.

클라이언트와 서버 간에 교환되는 데이터는 메시지 형식입니다. 각 메시지에는 유형과 데이터 페이로드가 있습니다. 메시지 유형에 따라 페이로드의 데이터가 해석되는 방식이 결정됩니다.

네 가지 메시지 유형이 있습니다.

- **텍스트**: 메시지의 페이로드는 UTF-8 인코딩 문자열로 해석됩니다.
- **이진**: 메시지의 페이로드는 원시 이진 데이터로 해석됩니다.
- **닫기**: 연결이 닫힙니다.
- **Ping**: 클라이언트가 서버에 아직 있는지 묻고 있습니다. 서버는 Pong 메시지로 응답합니다.

## WebSocket을 사용하는 이유는 무엇입니까?

HTTP는 훌륭한 프로토콜이지만 몇 가지 제한 사항이 있습니다. 주요 제한 사항 중 하나는 요청/응답 프로토콜이라는 것입니다. 이것은 클라이언트가 서버에 요청을 보낸 다음 응답을 기다려야 함을 의미합니다. 서버는 클라이언트가 먼저 요청하지 않으면 클라이언트에 데이터를 보낼 수 없습니다.

이 제한은 폴링을 사용하여 해결할 수 있습니다. 클라이언트는 서버에 새로운 데이터가 있는지 묻는 요청을 보낼 수 있고, 서버는 새로운 데이터가 있으면 응답할 수 있습니다. 이것은 효과가 있지만 몇 가지 단점이 있습니다.

- 클라이언트는 새로운 데이터가 없어도 계속 요청을 보내야 하므로 비효율적이다.
- 클라이언트가 다른 요청을 보내기 전에 응답을 기다려야 하므로 대기 시간이 추가됩니다.
- 새로운 데이터를 생성하는 서버와 이를 수신하는 클라이언트 사이에 지연이 있으므로 실시간이 아닙니다.

WebSocket은 단일 TCP 연결을 통해 전이중 통신 채널을 제공하여 이러한 제한을 제거합니다. 이는 클라이언트와 서버가 응답을 기다리지 않고 동시에 서로에게 데이터를 보낼 수 있음을 의미합니다.

## Nest.js에서 WebSocket 시작하기

Nest.js는 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. Node.js 위에 구축되었으며 TypeScript를 사용합니다.

Nest.js는 @nestjs/websockets 모듈과 함께 WebSocket을 사용하는 방법을 제공합니다.

@nestjs/websockets를 사용하려면 npm에서 설치해야 합니다.

```
npm install @nestjs/websockets
```

@nestjs/websockets가 설치되면 다음과 같이 Nest.js 서버를 만들 수 있습니다.

```typescript
import { NestFactory } from '@nestjs/core';
import { WsAdapter } from '@nestjs/platform-ws';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useWebSocketAdapter(new WsAdapter(app));
  await app.listen(3000);
}
bootstrap();
```

위의 예에서는 @nestjs/platform-ws에서 WsAdapter를 가져와서 useWebSocketAdapter() 메서드에 전달했습니다. 이렇게 하면 Nest.js 서버가 HTTP 대신 WebSocket 프로토콜을 사용하게 됩니다.

그런 다음 WebSocket 메시지를 처리하는 컨트롤러를 만들 수 있습니다.

```typescript
import {
  Controller,
  OnGatewayConnection,
  OnGatewayDisconnect,
  SubscribeMessage,
  WebSocketGateway,
  WsResponse,
} from '@nestjs/websockets';
import { Observable, of } from 'rxjs';
import { map } from 'rxjs/operators';

@Controller()
@WebSocketGateway()
export class AppController {
  @SubscribeMessage('events')
  findAll(client, data): Observable<WsResponse<number[]>> {
    return of([1, 2, 3]).pipe(map(item => ({ event: 'events', data: item })));
  }

  @SubscribeMessage('identity')
  identity(client, data: number): Observable<number> {
    return of(data);
  }

  @OnGatewayConnection()
  handleConnection(client) {
    console.log('Client connected');
  }

  @OnGatewayDisconnect()
  handleDisconnect(client) {
    console.log('Client disconnected');
  }
}
```

위의 예에서는 두 가지 방법으로 컨트롤러를 만들었습니다. 첫 번째 메서드인 findAll()은 'events' 주제를 구독합니다. 즉, 클라이언트가 'events' 항목에 메시지를 보낼 때마다 호출됩니다. findAll() 메서드는 클라이언트에 메시지를 보낼 Observable을 반환합니다.

두 번째 메서드인 identity()는 'identity' 항목을 구독합니다. 즉, 클라이언트가 'identity' 주제에 메시지를 보낼 때마다 호출됩니다. identity() 메서드는 클라이언트가 보낸 데이터를 내보내는 Observable을 반환합니다.

또한 클라이언트가 WebSocket 서버에 연결하고 연결을 끊을 때 호출되는 두 가지 메서드인 handleConnection() 및 handleDisconnect()를 정의했습니다.

## 메시지 보내기 및 받기

Nest.js 서버가 실행되면 WebSocket 클라이언트를 사용하여 메시지를 보낼 수 있습니다. 많은 WebSocket 클라이언트를 사용할 수 있지만 이 예에서는 ws NPM 패키지를 사용합니다.

ws 패키지를 설치하려면 다음 명령을 실행하십시오.

```
npm install ws
```

ws 패키지가 설치되면 다음과 같은 클라이언트를 만들 수 있습니다.

```javascript
const WebSocket = require('ws');

const ws = new WebSocket('ws://localhost:3000');

ws.on('open', function open() {
  console.log('connected');
  ws.send(JSON.stringify({ event: 'events', data: 'hello world' }));
});

ws.on('message', function incoming(data) {
  console.log(data);
});
```

위의 예에서는 Nest.js 서버에 연결하는 WebSocket 클라이언트를 만들었습니다. 두 개의 이벤트 핸들러를 정의했습니다. 하나는 연결이 열릴 때이고 다른 하나는 메시지가 수신될 때입니다.

open 이벤트 핸들러에서 우리는 서버에 메시지를 보내고 있습니다. 메시지에는 '이벤트' 유형과 'hello world' 페이로드가 있습니다.

메시지 이벤트 핸들러에서 서버로부터 받은 데이터를 인쇄하고 있습니다.

## 결론

이 기사에서는 WebSocket을 사용하여 Nest.js로 실시간 애플리케이션을 만드는 방법을 살펴보았습니다. Nest.js 서버를 만드는 방법과 WebSocket 클라이언트로 메시지를 보내고 받는 방법을 살펴보았습니다.