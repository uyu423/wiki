---
title: 059: TensorFlow.js와 Node.js의 WebSockets 통합
description: 
published: true
date: 2023-02-02T20:44:16.079Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:44:11.371Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [059: Integrating TensorFlow.js with WebSockets in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/059-integrating-tensorflow-js-with-websockets-in-node-js)
{.links-list}


# 059: TensorFlow.js와 Node.js의 WebSockets 통합

TensorFlow.js는 브라우저에서 기계 학습 모델을 교육하고 배포하기 위한 강력한 도구입니다. 그러나 브라우저의 교육 모델은 사용 가능한 리소스가 제한되어 있어 느리고 비효율적일 수 있습니다.

교육 속도를 높이는 한 가지 방법은 WebSocket을 사용하여 교육용 서버로 데이터를 보내는 것입니다. 이러한 방식으로 서버는 리소스를 사용하여 모델을 더 빠르게 훈련할 수 있습니다.

이 게시물에서는 Node.js 서버를 설정하고 WebSocket을 사용하여 TensorFlow.js 모델 교육을 위해 데이터를 서버로 보내는 방법을 보여줍니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- 텍스트 편집기. [Visual Studio Code](https://code.visualstudio.com/)를 권장합니다.
- [Node.js](https://nodejs.org/en/)가 컴퓨터에 설치되었습니다.
- [NPM](https://www.npmjs.com/)(Node.js와 함께 제공)이 컴퓨터에 설치됩니다.
- 컴퓨터에 [TensorFlow.js](https://js.tensorflow.org/) 설치.

## Node.js 서버 설정

먼저 Node.js 서버를 설정해야 합니다. 우리는 [ Express ](https://expressjs.com/) 웹 프레임워크를 사용하여 일을 더 쉽게 할 것입니다.

`server.js`라는 새 파일을 만들고 다음 코드를 붙여넣습니다.

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

이 코드는 포트 3000에서 수신 대기하는 기본 Express 서버를 생성합니다.

다음으로 서버에 대한 종속성을 설치해야 합니다. 터미널에서 `server.js`가 있는 디렉토리로 이동하고 다음 명령을 실행하십시오.

```
npm install express --save
```

이렇게 하면 Express 프레임워크가 설치되고 `package.json` 파일에 종속 항목으로 저장됩니다.

이제 서버가 설정되었으므로 터미널에서 다음 명령을 실행하여 서버를 시작할 수 있습니다.

```
node server.js
```

다음 출력이 표시되어야 합니다.

```
Example app listening on port 3000!
```

## 서버로 데이터 보내기

이제 서버가 가동되어 실행 중이므로 데이터 전송을 시작할 수 있습니다. [ WebSockets ](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)를 사용하여 브라우저에서 서버로 데이터를 보냅니다.

먼저 [ ws ](https://github.com/websockets/ws) WebSocket 라이브러리를 설치해야 합니다. 터미널에서 `server.js`가 있는 디렉토리로 이동하고 다음 명령을 실행하십시오.

```
npm install ws --save
```

그러면 `ws` 라이브러리가 설치되고 `package.json` 파일에 종속 항목으로 저장됩니다.

다음으로 `ws` 라이브러리를 사용하려면 `server.js` 파일을 수정해야 합니다. `server.js`의 내용을 다음 코드로 바꿉니다.

```javascript
const express = require('express');
const app = express();
const port = 3000;
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });
  ws.send('Hello!');
});

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

이 코드는 포트 8080에서 수신 대기하는 새 WebSocket 서버를 생성합니다. 연결이 설정되면 서버는 수신하는 모든 메시지를 기록합니다.

이제 서버가 데이터를 수신하도록 설정되었으므로 서버에 데이터를 보내는 코드를 작성할 수 있습니다. `client.html`이라는 새 파일을 만들고 다음 코드를 붙여넣습니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket Client</title>
  </head>
  <body>
    <h1>WebSocket Client</h1>
    <script>
      const ws = new WebSocket('ws://localhost:8080');
      ws.onopen = () => {
        // Send a message when the WebSocket is opened
        ws.send('Hello!');
      };
      ws.onmessage = (event) => {
        // Log the message when a message is received
        console.log(event.data);
      };
    </script>
  </body>
</html>
```

이 코드는 서버에 대한 새 WebSocket 연결을 생성하고 연결이 열리면 메시지를 보냅니다. 또한 수신하는 모든 메시지를 기록합니다.

브라우저에서 `client.html`을 열면 콘솔에 다음 출력이 표시되어야 합니다.

```
Hello!
```

## 학습을 위해 서버로 데이터 전송

이제 데이터를 서버로 보낼 수 있으므로 이를 사용하여 TensorFlow.js 모델을 교육할 수 있습니다. [ Iris Dataset ](https://en.wikipedia.org/wiki/Iris_flower_data_set)을 사용하여 간단한 분류 모델을 학습합니다.

먼저 TensorFlow.js 라이브러리를 포함하도록 `server.js` 파일을 수정해야 합니다. `server.js`의 내용을 다음 코드로 바꿉니다.

```javascript
const express = require('express');
const app = express();
const port = 3000;
const WebSocket = require('ws');
const tf = require('@tensorflow/tfjs');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (message) => {
    console.log(`Received message => ${message}`);
  });
  ws.send('Hello!');
});

app.get('/', (req, res) => res.send('Hello World!'));

app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

이 코드는 TensorFlow.js 라이브러리를 포함하며 기본 분류 모델을 생성합니다.

다음으로, 학습을 위해 데이터를 서버로 보내도록 `client.html` 파일을 수정해야 합니다. `client.html`의 내용을 다음 코드로 바꿉니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebSocket Client</title>
  </head>
  <body>
    <h1>WebSocket Client</h1>
    <script>
      const ws = new WebSocket('ws://localhost:8080');
      ws.onopen = () => {
        // Send data to the server when the WebSocket is opened
        ws.send('1,2,3,4');
      };
      ws.onmessage = (event) => {
        // Log the message when a message is received
        console.log(event.data);
      };
    </script>
  </body>
</html>
```

이 코드는 연결이 열릴 때 서버에 데이터를 보냅니다. 또한 수신하는 모든 메시지를 기록합니다.

브라우저에서 `client.html`을 열면 콘솔에 다음 출력이 표시되어야 합니다.

```
Received message => 1,2,3,4
```

## 결론

이 게시물에서는 Node.js 서버를 설정하고 WebSocket을 사용하여 TensorFlow.js 모델 교육을 위해 데이터를 서버로 보내는 방법을 보여 주었습니다.

이는 브라우저에서 머신 러닝 모델을 학습시키는 강력한 방법입니다. 서버의 리소스를 사용하여 모델을 보다 빠르고 효율적으로 교육할 수 있습니다.