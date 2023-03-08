---
title: Socket.io로 실시간 애플리케이션 구축
description: 
published: true
date: 2023-02-17T18:00:58.029Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:21:07.677Z
---

- [Building Real-time Applications with Socket.io***English** version of this document is available*](/en/Knowledge-base/Backend/building-real-time-applications-with-socket-io)
{.links-list}


# Socket.io로 실시간 애플리케이션 구축

이 기사에서는 Socket.io로 실시간 애플리케이션을 구축하는 방법을 살펴보겠습니다. Socket.io는 실시간 양방향 통신 애플리케이션을 쉽게 만들 수 있게 해주는 JavaScript 라이브러리입니다.

우리는 간단한 채팅 애플리케이션을 만들 것입니다. 채팅 애플리케이션은 HTML, CSS 및 JavaScript를 사용하여 구축할 프런트 엔드 웹 인터페이스와 Node.js 및 Socket.io를 사용하여 구축할 백엔드 서버의 두 부분으로 구성됩니다.

## 개발 환경 설정

코드 작성을 시작하기 전에 개발 환경을 설정해야 합니다. Node.js와 Socket.io 라이브러리를 설치해야 합니다.

### Node.js 설치하기

Node.js는 웹 브라우저 외부의 컴퓨터에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다. Socket.io 채팅 애플리케이션이 작동하려면 Node.js가 필요합니다.

Node.js를 설치하는 몇 가지 방법이 있습니다. 가장 쉬운 방법은 [Node.js 웹사이트](https://nodejs.org/en/)에서 Node.js 설치 프로그램을 다운로드하는 것입니다. 설치 프로그램을 실행하고 지침을 따릅니다.

Node.js가 설치되면 터미널 또는 명령 프롬프트를 열고 `node -v`를 입력합니다. 설치한 Node.js 버전이 인쇄됩니다. `v10.16.0`과 같은 내용이 표시되어야 합니다.

### Socket.io 설치

이제 Node.js가 설치되었으므로 Socket.io를 설치할 수 있습니다. Socket.io는 실시간 양방향 통신 응용 프로그램을 쉽게 만들 수 있는 JavaScript 라이브러리입니다.

Socket.io를 설치하는 방법에는 두 가지가 있습니다. 첫 번째 방법은 [Socket.io 웹사이트](https://socket.io/)를 이용하는 것입니다. 두 번째 방법은 Node.js에 포함된 [npm](https://www.npmjs.com/) 패키지 관리자를 사용하는 것입니다.

npm 패키지 관리자를 사용하여 Socket.io를 설치합니다. Socket.io를 설치하려면 터미널 또는 명령 프롬프트를 열고 `npm install socket.io`를 입력합니다. 이렇게 하면 Socket.io 라이브러리가 프로젝트에 설치됩니다.

## 채팅 애플리케이션 만들기

이제 개발 환경이 설정되었으므로 코드 작성을 시작할 수 있습니다.

`index.html`이라는 파일을 만드는 것으로 시작하겠습니다. 이것은 프론트엔드 웹 인터페이스가 내장될 HTML 파일이 될 것입니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Socket.io Chat</title>
  </head>
  <body>
    <h1>Socket.io Chat</h1>
    
    <form id="message-form">
      <input type="text" id="message-input" placeholder="Enter a message...">
      <button type="submit">Send</button>
    </form>
    
    <ul id="message-list"></ul>
    
    <script src="/socket.io/socket.io.js"></script>
    <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
    <script src="/js/index.js"></script>
  </body>
</html>
```

`index.html` 파일에는 Socket.io JavaScript 라이브러리와 jQuery 라이브러리가 포함되어 있습니다. 우리는 또한 잠시 후에 만들 자체 `index.js` 파일을 포함했습니다.

다음으로 `index.js` 파일을 생성합니다. 이것은 우리의 자바스크립트 코드가 들어갈 곳입니다.

```js
$(function() {
  var socket = io();
  
  $('#message-form').submit(function(e) {
    e.preventDefault();
    
    var message = $('#message-input').val();
    
    socket.emit('message', message);
    
    $('#message-input').val('');
    
    return false;
  });
  
  socket.on('message', function(message) {
    $('#message-list').append($('<li>').text(message));
  });
});
```

`index.js` 파일에서 Socket.io 서버에 대한 연결을 만들었습니다. 또한 사용자가 메시지 양식을 제출할 때 호출되는 이벤트 핸들러를 설정했습니다.

메시지 양식이 제출되면 메시지 입력에서 메시지를 가져와 Socket.io 서버로 내보냅니다. 또한 사용자가 다른 메시지를 입력할 수 있도록 메시지 입력을 지울 것입니다.

마지막으로 Socket.io 서버가 메시지를 내보낼 때 호출되는 이벤트 핸들러를 설정했습니다. 이 경우 메시지 목록에 메시지를 추가합니다.

이제 프런트 엔드 웹 인터페이스가 설정되었으므로 백엔드 서버에서 작업을 시작할 수 있습니다.

먼저 `server.js`라는 파일을 생성합니다. 이것이 우리의 Node.js 코드가 들어갈 곳입니다.

```js
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res) {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket) {
  socket.on('message', function(message) {
    io.emit('message', message);
  });
});

http.listen(3000, function() {
  console.log('listening on *:3000');
});
```

`server.js` 파일에는 `express` 및 `socket.io` 라이브러리가 필요했습니다. HTTP 서버와 Socket.io 서버도 만들었습니다.

Socket.io 서버가 메시지를 수신할 때 호출될 이벤트 핸들러를 설정했습니다. 이 경우 연결된 모든 클라이언트에 메시지를 내보냅니다.

마지막으로 포트 3000에서 수신 대기하도록 HTTP 서버를 설정했습니다.

## 채팅 애플리케이션 실행

이제 채팅 애플리케이션을 작성했으므로 실행할 수 있습니다.

채팅 애플리케이션을 실행하려면 터미널이나 명령 프롬프트를 열고 `server.js` 파일이 있는 디렉토리로 이동합니다. 그런 다음 `node server.js`를 입력합니다. 그러면 Node.js 서버가 시작됩니다.

웹 브라우저를 열고 `http://localhost:3000`으로 이동합니다. 채팅 애플리케이션이 표시되어야 합니다. 메시지를 보내보십시오. 브라우저 창에 메시지가 표시되어야 합니다.

## 결론

이 기사에서는 Socket.io로 실시간 애플리케이션을 구축하는 방법을 살펴보았습니다. 실시간으로 메시지를 보내고 받을 수 있는 간단한 채팅 응용 프로그램을 만들었습니다.