---
title: WebSocket으로 실시간 애플리케이션을 구축하는 방법
description: 
published: true
date: 2023-02-17T18:03:14.913Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:54:19.544Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [How to Build a Real-Time Application with WebSockets***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-real-time-application-with-websockets)
{.links-list}


# WebSocket으로 실시간 애플리케이션을 구축하는 방법

이 기사에서는 WebSocket을 사용하여 실시간 애플리케이션을 구축하는 방법을 보여줍니다. WebSocket의 기본 사항과 WebSocket을 사용하여 간단한 채팅 애플리케이션을 만드는 방법을 살펴보겠습니다.

WebSocket은 클라이언트와 서버 간의 전이중 통신을 허용하는 프로토콜입니다. 이는 클라이언트와 서버가 동시에 데이터를 보내고 받을 수 있음을 의미합니다. WebSocket은 채팅 애플리케이션, 멀티플레이어 게임, 협업 도구와 같이 실시간 통신이 필요한 애플리케이션에 특히 적합합니다.

## WebSocket 서버 생성

애플리케이션에서 WebSocket을 사용하려면 WebSocket 서버를 생성해야 합니다. WebSocket 프로토콜을 지원하는 모든 웹 서버에서 이 작업을 수행할 수 있습니다. 이 기사의 목적을 위해 Node.js 웹 서버를 사용합니다.

```javascript
var WebSocketServer = require('ws').Server;

var wss = new WebSocketServer({
  port: 8080
});

wss.on('connection', function(ws) {
  ws.on('message', function(message) {
    console.log('Received: %s', message);
  });

  ws.send('Hello, world!');
});
```

이 코드는 들어오는 연결을 포트 8080에서 수신 대기하는 WebSocket 서버를 만듭니다. 연결이 이루어지면 서버는 해당 연결에 대한 WebSocket 인스턴스를 생성합니다. 그런 다음 서버는 클라이언트의 메시지를 수신합니다. 메시지를 받으면 콘솔에 기록됩니다. 서버는 또한 처음 연결될 때 클라이언트에 메시지를 보냅니다.

WebSocket 서버는 Node.js 명령줄 인터페이스로 실행할 수 있습니다.

```
node server.js
```

## WebSocket 클라이언트 생성

이제 WebSocket 서버가 실행 중이므로 WebSocket 클라이언트를 생성하여 연결해야 합니다. 이 문서의 목적을 위해 브라우저 기반 JavaScript 클라이언트를 사용합니다.

```javascript
var ws = new WebSocket('ws://localhost:8080');

ws.onopen = function() {
  ws.send('Hello, world!');
};

ws.onmessage = function(event) {
  console.log(event.data);
};
```

이 코드는 WebSocket 인스턴스를 생성하고 WebSocket 서버에 연결합니다. 이 코드는 두 개의 이벤트 핸들러도 정의합니다. 첫 번째 이벤트 핸들러는 ```open``` event. This event is fired when the connection is established. The second event handler is for the ```message``` event. This event is fired when the server sends a message to the client.

## Sending and Receiving Messages

Now that we have a WebSocket server and client set up, we can start sending and receiving messages. The ```send``` method can be used to send messages from the client to the server. The ```onmessage``` event handler can be used to receive messages from the server.

```자바스크립트
ws.send('안녕, 세상!');

ws.onmessage = 함수(이벤트) {
  console.log(event.data);
};
```

In this code, the ```send``` 메소드는 클라이언트에서 서버로 메시지를 보내는 데 사용됩니다. ```onmessage``` 이벤트 핸들러는 서버에서 메시지를 수신하는 데 사용됩니다. 메시지가 콘솔에 기록됩니다.