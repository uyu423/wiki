---
title: Socket.io와 실시간 통신
description: 
published: true
date: 2023-02-17T06:17:29.804Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:17:28.344Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Real-time Communication with Socket.io***English** document is available*](/en/Knowledge-base/Backend/real-time-communication-with-socket-io)
{.links-list}



# Socket.io와 실시간 통신

이 기사에서는 Socket.io와의 실시간 통신에 대해 설명합니다. Socket.io는 웹 클라이언트와 서버 간에 실시간 양방향 통신을 제공하는 JavaScript 라이브러리입니다. 실시간 메시징, 채팅, 게임 등과 같은 실시간 응용 프로그램에서 사용하기에 이상적인 여러 기능이 있습니다.

Socket.io는 WebSocket 프로토콜을 기반으로 하며 Node.js 플랫폼을 사용합니다. 사용하기 쉽고 설정하기 쉬우므로 실시간 응용 프로그램에 적합합니다.

## Socket.io 설정

Socket.io를 사용하려면 socket.io 모듈을 설치해야 합니다. NPM(노드 패키지 관리자)을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install socket.io
```

모듈이 설치되면 Node.js 애플리케이션에서 요구할 수 있습니다.

```javascript
var io = require('socket.io')();
```

socket.io 모듈은 http 서버 인스턴스로 호출할 수 있는 함수를 반환합니다. 그러면 socket.io 통신이 설정됩니다.

## Socket.io 사용

Socket.io는 두 가지 통신 방법을 제공합니다.

* 이벤트: 클라이언트에서 서버로 또는 서버에서 클라이언트로 이벤트를 내보낼 수 있습니다. 이벤트는 원하는 대로 이름을 지정할 수 있으며 데이터를 전달할 수 있습니다.
* 메시지: 클라이언트와 서버 간에 메시지를 보낼 수 있습니다. 메시지는 이벤트와 비슷하지만 다양한 유형의 데이터(예: 이진 데이터)를 보낼 수 있는 특정 형식으로 전송됩니다.

### 이벤트

클라이언트에서 서버로 이벤트를 내보내려면 emit 메소드를 사용할 수 있습니다.

```javascript
socket.emit('eventName', data);
```

서버에서 클라이언트로 이벤트를 내보내려면 소켓 개체에서 emit 메서드를 사용할 수 있습니다.

```javascript
socket.emit('eventName', data);
```

이벤트를 생성한 클라이언트를 제외하고 연결된 모든 클라이언트에 이벤트를 브로드캐스트할 수도 있습니다. 이렇게 하려면 브로드캐스트 방법을 사용할 수 있습니다.

```javascript
socket.broadcast.emit('eventName', data);
```

이벤트를 수신하려면 on 메소드를 사용할 수 있습니다.

```javascript
socket.on('eventName', function(data) {
  // do something with the data
});
```

### 메시지

클라이언트에서 서버로 메시지를 보내려면 send 메소드를 사용할 수 있습니다.

```javascript
socket.send('message');
```

서버에서 클라이언트로 메시지를 보내려면 소켓 개체에서 send 메서드를 사용할 수 있습니다.

```javascript
socket.send('message');
```

메시지를 보낸 클라이언트를 제외하고 연결된 모든 클라이언트에 메시지를 브로드캐스트하려면 브로드캐스트 메소드를 사용할 수 있습니다.

```javascript
socket.broadcast.send('message');
```

메시지를 수신하려면 on 메소드를 사용할 수 있습니다.

```javascript
socket.on('message', function(data) {
  // do something with the data
});
```

## 결론

Socket.io는 실시간 애플리케이션을 위한 탁월한 선택입니다. 사용하기 쉽고 설정하기 쉽습니다. 또한 실시간 응용 프로그램에서 사용하기에 이상적인 여러 기능을 제공합니다.