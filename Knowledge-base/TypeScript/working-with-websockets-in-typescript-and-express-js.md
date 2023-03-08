---
title: TypeScript 및 Express.js에서 WebSocket 작업
description: 
published: true
date: 2023-02-17T18:11:59.810Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:57:49.577Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Working with WebSockets in TypeScript and Express.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/working-with-websockets-in-typescript-and-express-js)
{.links-list}





WebSocket은 클라이언트와 서버 간의 통신에 매우 널리 사용되는 방법입니다. 단일 TCP 연결을 통해 양방향 전이중 통신 채널을 제공하며 모든 주요 브라우저에서 매우 잘 지원됩니다.

이 기사에서는 TypeScript 및 Express.js에서 WebSocket을 사용하는 방법을 보여줍니다. 또한 웹 애플리케이션에서 이를 사용하는 방법에 대한 몇 가지 실용적인 예를 제공합니다.

## WebSocket이 무엇인가요?

WebSocket은 웹 브라우저와 서버 간의 양방향 실시간 통신을 가능하게 하는 비교적 새로운 기술입니다. 기존 HTTP 요청-응답 모델의 대안이며 훨씬 더 효율적인 통신 채널을 제공합니다.

 WebSocket은 TCP 프로토콜을 기반으로 하며 전이중 통신 채널을 사용합니다. 이는 클라이언트와 서버가 동시에 데이터를 보내고 받을 수 있음을 의미합니다.

WebSocket은 모든 주요 브라우저에서 지원되며 웹 애플리케이션에서 WebSocket을 쉽게 사용할 수 있도록 잘 지원되는 여러 라이브러리 및 프레임워크가 있습니다.

## WebSocket을 사용하는 이유는 무엇입니까?

WebSocket은 기존 HTTP 요청-응답 모델에 비해 많은 이점을 제공합니다.

통신 기간 동안 열려 있는 단일 TCP 연결만 필요하므로 훨씬 더 효율적입니다. 이는 HTTP의 경우와 같이 각 요청에 대해 새 연결을 설정할 필요가 없음을 의미합니다.

또한 다음 요청을 보내기 전에 요청이 완료될 때까지 기다릴 필요가 없기 때문에 대기 시간이 훨씬 짧습니다. 이는 채팅 애플리케이션, 온라인 게임 등과 같이 실시간 통신이 필요한 애플리케이션에 특히 중요합니다.

## WebSocket은 어떻게 작동합니까?

WebSocket은 HTTP 프로토콜의 확장인 ws://라는 프로토콜을 사용합니다. 클라이언트가 서버에 대한 WebSocket 연결을 설정하려는 경우 이 프로토콜을 사용하여 요청을 보냅니다.

그러면 서버가 WebSocket 프로토콜 상태 코드에 대한 HTTP 101 스위치로 응답하고 연결이 WebSocket 연결로 업그레이드됩니다.

연결이 설정되면 클라이언트와 서버는 언제든지 데이터를 보내고 받을 수 있습니다.

## TypeScript에서 WebSocket 사용

ws 및 socket.io와 같이 TypeScript에서 WebSocket 지원을 제공하는 데 사용할 수 있는 여러 라이브러리가 있습니다. 이 기사에서는 socket.io 라이브러리를 사용합니다.

Socket.io는 TypeScript 애플리케이션에서 WebSocket을 쉽게 사용할 수 있도록 지원하는 대중적이고 잘 지원되는 라이브러리입니다. WebSocket 프로토콜의 세부 정보를 추상화하고 데이터를 보내고 받는 데 사용할 수 있는 간단한 API를 제공합니다.

Socket.io는 게시/구독 메시징, 회의실 등과 같은 여러 다른 기능도 제공합니다.

## Socket.io 설치

npm 패키지 관리자를 사용하여 Socket.io를 설치할 수 있습니다.

```
npm install socket.io
```

## Socket.io 서버 생성

Socket.io 애플리케이션은 브라우저에서 실행되는 클라이언트 측 라이브러리와 Node.js 플랫폼에서 실행되는 서버 측 라이브러리의 두 부분으로 구성됩니다.

이 섹션에서는 연결된 모든 클라이언트에 "hello world" 메시지를 브로드캐스트하는 간단한 Socket.io 서버를 만듭니다.

먼저 socket.io 라이브러리를 가져와야 합니다.

```typescript
import * as io from "socket.io";
```

다음으로 Express.js 프레임워크를 사용하여 HTTP 서버를 만듭니다.

```typescript
const app = express();
const server = http.createServer(app);
```

그런 다음 Socket.io 라이브러리를 HTTP 서버에 바인딩할 수 있습니다.

```typescript
const io = socketIO(server);
```

이제 Socket.io 서버가 실행 중이므로 들어오는 연결을 처리하는 코드를 작성해야 합니다. ```connection``` event:

```타입스크립트
io.on("연결", (소켓) => {
  //
});
```

The ```connection``` event is emitted when a client connects to the server. The ```socket``` object that is passed to the callback function represents the client connection.

We can now write some code to send a message to the client:

```타입스크립트
io.on("연결", (소켓) => {
  socket.emit("안녕하세요", "안녕하세요!");
});
```

The ```emit``` method is used to send a message to the client. The first argument is the name of the event, and the second argument is the data to be sent.

## Creating a Socket.io client

Now that we have a Socket.io server up and running, let's create a client that will connect to it and print out the "hello world" message.

First, we need to include the Socket.io client library in our HTML page:

```html
<스크립트 src="/socket.io/socket.io.js"></스크립트>
```

Next, we'll create a new ```Socket``` instance, and connect it to our server:

```자바스크립트
const 소켓 = io("http://localhost:8080");
```

We can then listen for the ```hello``` event that we defined on the server:

```자바스크립트
socket.on("hello", (데이터) => {
  console.log(데이터); // "안녕하세요!"
});
```

## Sending and receiving data

In the previous section, we saw how to send data from the server to the client. In this section, we'll see how to do the reverse: send data from the client to the server.

We can do this using the ```send``` method:

```자바스크립트
socket.send("안녕하세요", "안녕하세요!");
```

On the server, we can listen for the ```message``` event:

```타입스크립트
socket.on("메시지", (데이터) => {
  console.log(데이터); // "안녕하세요!"
});
```

##결론

이 기사에서는 TypeScript 및 Express.js에서 WebSocket을 사용하는 방법을 살펴보았습니다. 또한 Socket.io 서버와 클라이언트를 만드는 방법과 이들 간에 데이터를 주고받는 방법도 살펴보았습니다.