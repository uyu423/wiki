---
title: 037: Nest.js 및 WebSockets로 실시간 채팅 구현
description: 
published: true
date: 2023-02-02T05:47:42.310Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:47:40.625Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [037: Implementing real-time chat with Nest.js and WebSockets***English** document is available*](/en/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}


# 037: Nest.js와 WebSockets로 실시간 채팅 구현하기

이 게시물에서는 WebSocket 프로토콜을 사용하여 Nest.js 웹 애플리케이션에 실시간 채팅 기능을 쉽게 추가하는 방법을 보여줍니다.

## 웹소켓이란?

WebSocket은 웹 브라우저와 웹 서버 간의 전이중 양방향 통신을 허용하는 통신 프로토콜입니다. 즉, 실시간으로 클라이언트와 서버 간의 양방향 통신이 가능합니다.

## WebSocket을 사용하는 이유는 무엇입니까?

WebSocket은 클라이언트와 서버 간의 지속적인 연결을 제공하므로 채팅 앱과 같은 실시간 애플리케이션을 구축하는 데 탁월한 선택입니다. 즉, 연결이 설정되면 클라이언트와 서버 모두 언제든지 데이터를 보내고 받을 수 있습니다.

## WebSocket은 어떻게 작동하나요?

WebSocket 프로토콜은 핸드셰이크를 사용하여 클라이언트와 서버 간의 연결을 설정합니다. 연결이 설정되면 클라이언트와 서버는 실시간으로 데이터를 주고받을 수 있습니다.

## Nest.js가 무엇인가요?

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 최신 JavaScript를 사용하고 TypeScript(강력한 타이핑 제공)로 구축되었으며 객체 지향 프로그래밍, 기능 프로그래밍 및 반응 프로그래밍의 요소를 결합합니다.

## Nest.js를 사용하는 이유는 무엇인가요?

Nest.js는 확장성으로 알려진 플랫폼인 Node.js를 기반으로 구축되기 때문에 서버 측 애플리케이션 구축에 탁월한 선택입니다. 또한 Nest.js는 강력한 타이핑과 보다 구조화된 코드베이스를 제공하는 TypeScript를 사용합니다. 마지막으로 Nest.js는 객체 지향 프로그래밍, 기능적 프로그래밍 및 반응형 프로그래밍의 요소를 결합하여 매우 강력한 프레임워크가 됩니다.

## Nest.js는 어떻게 작동하나요?

Nest.js는 확장성으로 알려진 플랫폼인 Node.js 위에 구축됩니다. 또한 Nest.js는 강력한 타이핑과 보다 구조화된 코드베이스를 제공하는 TypeScript를 사용합니다. 마지막으로 Nest.js는 객체 지향 프로그래밍, 기능적 프로그래밍 및 반응형 프로그래밍의 요소를 결합하여 매우 강력한 프레임워크가 됩니다.

## WebSocket을 사용하여 Nest.js 웹 애플리케이션에 실시간 채팅을 추가하는 방법

이 섹션에서는 WebSocket 프로토콜을 사용하여 Nest.js 웹 애플리케이션에 실시간 채팅 기능을 추가하는 방법을 보여줍니다.

### 1단계: Nest.js 프로젝트 만들기

먼저 Nest.js 프로젝트를 만들어야 합니다. Nest.js가 설치되어 있지 않은 경우 다음 명령을 사용하여 설치할 수 있습니다.

```
npm install -g @nestjs/cli
```

Nest.js가 설치되면 다음 명령을 사용하여 새 Nest.js 프로젝트를 만들 수 있습니다.

```
nest new project-name
```

### 2단계: WebSocket 모듈 설치

다음으로 WebSocket 모듈을 설치해야 합니다. WebSocket 모듈은 WebSocket 프로토콜로 작업할 수 있는 Node.js 모듈입니다.

다음 명령을 사용하여 WebSocket 모듈을 설치할 수 있습니다.

```
npm install --save @nestjs/websockets
```

### 3단계: WebSocket 모듈 활성화

WebSocket 모듈이 설치되면 Nest.js 애플리케이션에서 활성화해야 합니다. src/app.module.ts 파일에 다음 코드 줄을 추가하면 됩니다.

```typescript
@Module({
  imports: [
    // ...
    WebsocketsModule.forRoot(),
  ],
  // ...
})
export class AppModule {}
```

### 4단계: WebSocket 게이트웨이 만들기

다음으로 WebSocket 게이트웨이를 만들어야 합니다. WebSocket 게이트웨이는 들어오는 WebSocket 연결을 처리하는 Nest.js 서비스입니다.

다음 명령을 사용하여 WebSocket 게이트웨이를 생성할 수 있습니다.

```
nest generate gateway websocket
```

이렇게 하면 src/websocket/websocket.gateway.ts라는 새 파일이 생성됩니다.

### 5단계: 들어오는 WebSocket 연결 처리

WebSocket 게이트웨이를 만든 후에는 들어오는 WebSocket 연결을 처리해야 합니다. src/websocket/websocket.gateway.ts 파일에 다음 코드를 추가하여 이를 수행할 수 있습니다.

```typescript
@WebSocketGateway()
export class WebsocketGateway {

  @WebSocketServer()
  server;

  @WebSocketConnect()
  connect(@ConnectedSocket() socket) {
    // ...
  }

  @WebSocketDisconnect()
  disconnect(@ConnectedSocket() socket) {
    // ...
  }

}
```

@WebSocketGateway() 데코레이터는 WebSocket 게이트웨이를 만드는 데 사용됩니다. @WebSocketServer() 데코레이터는 WebSocket 서버를 WebSocket 게이트웨이에 삽입하는 데 사용됩니다. @WebSocketConnect() 데코레이터는 들어오는 WebSocket 연결을 처리하는 데 사용됩니다. @WebSocketDisconnect() 데코레이터는 WebSocket 연결 해제를 처리하는 데 사용됩니다.

### 6단계: 채팅 서비스 만들기

다음으로 채팅 서비스를 만들어야 합니다. 채팅 서비스는 메시지 송수신을 담당합니다.

다음 명령을 사용하여 채팅 서비스를 만들 수 있습니다.

```
nest generate service chat
```

이렇게 하면 src/chat/chat.service.ts라는 새 파일이 생성됩니다.

### 7단계: 채팅 서비스 구현

채팅 서비스를 만든 후에는 구현해야 합니다. src/chat/chat.service.ts 파일에 다음 코드를 추가하면 됩니다.

```typescript
@Injectable()
export class ChatService {

  constructor(
    private readonly websocketGateway: WebsocketGateway,
  ) {}

  sendMessage(message: string) {
    // ...
  }

  getMessages() {
    // ...
  }

}
```

ChatService 클래스에는 sendMessage() 및 getMessages()의 두 가지 메서드가 있습니다. sendMessage() 메서드는 채팅 서비스에 메시지를 보내는 데 사용됩니다. getMessages() 메서드는 채팅 서비스에서 메시지를 받는 데 사용됩니다.

### 8단계: 채팅 컨트롤러 만들기

다음으로 채팅 컨트롤러를 만들어야 합니다. 채팅 컨트롤러는 HTTP 요청 처리를 담당합니다.

다음 명령을 사용하여 채팅 컨트롤러를 만들 수 있습니다.

```
nest generate controller chat
```

이렇게 하면 src/chat/chat.controller.ts라는 새 파일이 생성됩니다.

### 9단계: 채팅 컨트롤러 구현

채팅 컨트롤러를 만들었으면 구현해야 합니다. src/chat/chat.controller.ts 파일에 다음 코드를 추가하면 됩니다.

```typescript
@Controller('chat')
export class ChatController {

  constructor(
    private readonly chatService: ChatService,
  ) {}

  @Get()
  getMessages() {
    // ...
  }

  @Post()
  sendMessage(@Body() message: string) {
    // ...
  }

}
```

ChatController 클래스에는 getMessages() 및 sendMessage()의 두 가지 메서드가 있습니다. getMessages() 메서드는 GET 요청을 처리하는 데 사용됩니다. sendMessage() 메서드는 POST 요청을 처리하는 데 사용됩니다.

### 10단계: 채팅 서비스를 WebSocket 게이트웨이에 연결

이 단계에서는 채팅 서비스를 WebSocket 게이트웨이에 연결해야 합니다. src/chat/chat.service.ts 파일에 다음 코드를 추가하면 됩니다.

```typescript
@Injectable()
export class ChatService {

  constructor(
    private readonly websocketGateway: WebsocketGateway,
  ) {}

  sendMessage(message: string) {
    this.websocketGateway.server.emit('message', message);
  }

  getMessages() {
    // ...
  }

}
```

sendMessage() 메서드는 emit() 메서드를 사용하여 WebSocket 서버에 메시지를 보냅니다.

### 11단계: 채팅 컨트롤러를 채팅 서비스에 연결

이 단계에서는 채팅 컨트롤러를 채팅 서비스에 연결해야 합니다. src/chat/chat.controller.ts 파일에 다음 코드를 추가하면 됩니다.

```typescript
@Controller('chat')
export class ChatController {

  constructor(
    private readonly chatService: ChatService,
  ) {}

  @Get()
  getMessages() {
    return this.chatService.getMessages();
  }

  @Post()
  sendMessage(@Body() message: string) {
    this.chatService.sendMessage(message);
  }

}
```

getMessages() 메서드는 getMessages() 메서드를 사용하여 채팅 서비스에서 메시지를 가져옵니다. sendMessage() 메서드는 sendMessage() 메서드를 사용하여 채팅 서비스에 메시지를 보냅니다.

### 12단계: 채팅 애플리케이션 테스트

채팅 애플리케이션을 테스트하려면 Postman과 같은 도구를 사용할 수 있습니다.

먼저 Nest.js 애플리케이션을 시작해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm start
```

다음으로 /chat 끝점에 POST 요청을 보내야 합니다. 다음 URL을 사용하여 이 작업을 수행할 수 있습니다.

```
http://localhost:3000/chat
```

요청 본문에 메시지를 포함해야 합니다. 예를 들어 다음 메시지를 사용할 수 있습니다.

```
Hello, world!
```

요청을 보내고 나면 콘솔에 메시지가 표시되어야 합니다.

## 결론

이 게시물에서는 WebSocket 프로토콜을 사용하여 Nest.js 웹 애플리케이션에 실시간 채팅 기능을 쉽게 추가하는 방법을 보여주었습니다.