---
title: Socket.io와 실시간 통신
description: 
published: true
date: 2023-01-29T20:20:56.030Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:20:56.030Z
---

- [Real-time communication with Socket.io***English** version of this document is available*](/en/Knowledge-base/Backend/real-time-communication-with-socket-io)
{.links-list}

# Socket.io와 실시간 통신

이 게시물에서는 Socket.io를 사용하여 클라이언트와 서버 간의 실시간 통신을 설정하는 방법을 살펴보겠습니다. Socket.io는 실시간 양방향 이벤트 기반 통신을 구현하는 기능을 제공하는 JavaScript 라이브러리입니다.

우리는 서버 측의 Node.js와 클라이언트 측의 Socket.io 클라이언트 라이브러리와 함께 Socket.io를 사용할 것입니다.

## 프로젝트 설정

이 프로젝트에서 다음 라이브러리를 사용합니다.

- [소켓.io](https://socket.io/)
- [익스프레스](https://expressjs.com/)
- [Node.js](https://nodejs.org/)

먼저 새 프로젝트를 만들고 종속 항목을 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
mkdir real-time-communication
cd real-time-communication
npm init -y
npm install --save socket.io
npm install --save express
```

## 서버 생성

이제 프로젝트가 설정되었으므로 서버 생성을 시작할 수 있습니다. Express를 사용하여 서버를 설정합니다.

`server.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```

이 코드는 포트 3000에서 수신하는 매우 기본적인 Express 서버를 설정합니다. 다음 명령을 실행하여 서버를 시작할 수 있습니다.

```
node server.js
```

브라우저에서 http://localhost:3000을 방문하면 "Hello World!"라는 메시지가 표시됩니다.

## Socket.io 추가

이제 서버가 설정되었으므로 여기에 Socket.io를 추가할 수 있습니다.

먼저 `socket.io` 라이브러리를 요구하고 인스턴스화해야 합니다. `server.js` 파일에 다음 코드를 추가하여 이를 수행할 수 있습니다.

```javascript
const io = require('socket.io')();
```

다음으로 들어오는 연결을 수신 대기하도록 Socket.io에 알려야 합니다. `server.js` 파일에 다음 코드를 추가하여 이를 수행할 수 있습니다.

```javascript
io.on('connection', (socket) => {
  console.log('a user connected');
});
```

이 코드는 `connection` 이벤트에 대한 이벤트 리스너를 설정합니다. 이 이벤트는 클라이언트가 서버에 연결할 때 발생합니다.

서버를 시작하고 브라우저에서 http://localhost:3000을 방문하여 코드가 작동하는지 테스트할 수 있습니다. JavaScript 콘솔을 열면 "a user connected"라는 메시지가 출력되는 것을 볼 수 있습니다.

## 메시지 보내기

이제 서버가 설정되었고 들어오는 연결을 수신할 수 있으므로 메시지 전송을 시작할 수 있습니다.

소켓 개체에서 `emit` 메서드를 사용하여 클라이언트에 메시지를 보낼 수 있습니다. `emit` 메서드는 이벤트 이름과 보낼 데이터의 두 가지 인수를 사용합니다.

`server.js` 파일에 다음 코드를 추가합니다.

```javascript
io.on('connection', (socket) => {
  socket.emit('message', 'Welcome to the chat!');
});
```

이 코드는 "Welcome to the chat!" 데이터와 함께 `message` 이벤트를 클라이언트에 내보냅니다.

서버를 시작하고 브라우저에서 http://localhost:3000을 방문하여 코드가 작동하는지 테스트할 수 있습니다. JavaScript 콘솔을 열면 "채팅에 오신 것을 환영합니다!"라는 메시지가 표시됩니다. 인쇄되었습니다.

## 메시지 수신

메시지를 보낼 수 있는 것 외에도 메시지를 받을 수 있어야 합니다.

소켓 개체의 'on' 메서드를 사용하여 클라이언트로부터 메시지를 받을 수 있습니다. 'on' 메소드는 이벤트 이름과 이벤트가 수신될 때 실행될 콜백 함수의 두 가지 인수를 사용합니다.

`server.js` 파일에 다음 코드를 추가합니다.

```javascript
io.on('connection', (socket) => {
  socket.on('message', (message) => {
    console.log(message);
  });
});
```

이 코드는 `message` 이벤트에 대한 이벤트 리스너를 설정합니다. 이 이벤트는 메시지가 전송될 때 클라이언트에서 발생합니다. 콜백 함수는 단순히 메시지를 콘솔에 출력합니다.

서버를 시작하고 브라우저에서 http://localhost:3000을 방문하고 입력 필드에 메시지를 입력하여 코드가 작동하는지 테스트할 수 있습니다. JavaScript 콘솔을 열면 입력한 메시지가 출력되는 것을 볼 수 있습니다.

## 방송 메시지

지금까지 개별 고객에게만 메시지를 보낼 수 있었습니다. 그러나 때로는 모든 클라이언트에게 메시지를 보낼 수 있어야 합니다. 이것을 방송이라고 합니다.

소켓 개체에서 `broadcast` 메서드를 사용하여 메시지를 브로드캐스트할 수 있습니다. `broadcast` 메서드는 이벤트 이름과 보낼 데이터의 두 가지 인수를 사용합니다.

`server.js` 파일에 다음 코드를 추가합니다.

```javascript
io.on('connection', (socket) => {
  socket.broadcast.emit('message', 'A new user has joined the chat!');
});
```

이 코드는 `connection` 이벤트를 생성한 클라이언트를 제외한 모든 클라이언트에 `message` 이벤트를 브로드캐스트합니다.

서버를 시작하고 브라우저에서 http://localhost:3000을 방문하고 입력 필드에 메시지를 입력하여 코드가 작동하는지 테스트할 수 있습니다. JavaScript 콘솔을 열면 "새 사용자가 채팅에 참여했습니다!"라는 메시지가 표시되어야 합니다. 인쇄되었습니다.

## 결론

이 게시물에서는 Socket.io를 사용하여 클라이언트와 서버 간의 실시간 통신을 설정하는 방법을 살펴보았습니다. 기본 서버를 설정하고 메시지를 보내고 받는 방법을 살펴보았습니다. 또한 모든 클라이언트에게 메시지를 브로드캐스트하는 방법도 살펴보았습니다.