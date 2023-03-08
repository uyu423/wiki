---
title: 081: TensorFlow.js 및 Node.js로 대화형 시각화 구축
description: 
published: true
date: 2023-02-03T01:44:02.577Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:44:00.872Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [081: Building Interactive Visualizations with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/081-building-interactive-visualizations-with-tensorflow-js-and-node-js)
{.links-list}


# 081: TensorFlow.js 및 Node.js로 대화형 시각화 구축

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 대화형 시각화를 구축하는 방법을 살펴보겠습니다.

TensorFlow.js는 브라우저에서 기계 학습을 가능하게 하는 수치 계산을 위한 강력한 JavaScript 라이브러리입니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

이 두 가지 기술을 함께 사용하여 데이터를 탐색하고 분석하는 데 사용할 수 있는 대화형 시각화를 구축할 수 있습니다.

## 시작하기

시작하려면 Node.js 및 TensorFlow.js를 설치해야 합니다.

Node.js는 공식 웹 사이트에서 다운로드하여 설치할 수 있습니다. https://nodejs.org/en/

TensorFlow.js는 Node.js 패키지 관리자를 사용하여 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

## 헬로월드

Node.js와 TensorFlow.js가 설치되면 다음 코드를 사용하여 간단한 "Hello World" 프로그램을 만들 수 있습니다.

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js graph
tf.tensor([1, 2, 3, 4]).print();
```

위의 코드를 "hello.js"라는 파일에 저장하고 Node.js 런타임을 사용하여 실행합니다.

```
node hello.js
```

다음 출력이 표시되어야 합니다.

```
Tensor
    [[1, 2, 3, 4]]
```

 축하합니다! 첫 번째 TensorFlow.js 프로그램을 방금 실행했습니다.

## 대화형 시각화 구축

TensorFlow.js 및 Node.js를 시작하는 방법을 살펴보았으므로 이제 이러한 기술을 사용하여 대화형 시각화를 구축하는 방법을 살펴보겠습니다.

다음 라이브러리를 사용하여 시각화를 구축할 것입니다.

- TensorFlow.js: 수치 계산 및 기계 학습용
- Node.js: 브라우저 외부에서 JavaScript 코드 실행
- Express: 웹 서버 생성용
- Socket.IO: 웹 서버와 브라우저 간의 실시간 통신용

우리의 시각화는 실시간으로 업데이트되는 간단한 라인 차트가 될 것입니다.

### 데이터 정의

먼저 시각화할 데이터를 정의하겠습니다. TensorFlow.js 그래프를 사용하여 임의의 데이터 포인트를 생성합니다.

```javascript
// Define a TensorFlow.js graph that generates random data
const data = tf.tensor(new Array(100).fill(0).map(() => Math.random()));
```

위의 코드는 100개의 임의 데이터 포인트를 생성하는 TensorFlow.js 그래프를 정의합니다.

### 웹 서버 만들기

다음으로 Node.js와 Express를 사용하여 웹 서버를 만들어 보겠습니다.

```javascript
// Load the Express.js library
const express = require('express');

// Create an Express.js app
const app = express();

// Define the port that the app will listen on
const port = 3000;

// Start the Express.js app
app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

위의 코드는 포트 3000에서 수신 대기하는 Express.js 앱을 만듭니다.

### HTML 페이지 제공

이제 웹 서버를 가동하고 실행 중이므로 시각화를 표시하는 데 사용할 HTML 페이지를 제공하겠습니다.

```javascript
// Serve the HTML page
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
```

위의 코드는 루트 URL에 액세스할 때 HTML 페이지를 제공하는 경로를 정의합니다.

HTML 페이지에는 다음 내용이 있어야 합니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>081: Building Interactive Visualizations with TensorFlow.js and Node.js</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0/dist/tf.min.js"></script>
    <script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.3/Chart.min.js"></script>
  </head>
  <body>
    <canvas id="chart"></canvas>
    <script>
      // Your code here
    </script>
  </body>
</html>
```

HTML 페이지에는 다음 라이브러리가 포함되어 있습니다.

- TensorFlow.js: 수치 계산 및 기계 학습용
- Socket.IO: 웹 서버와 브라우저 간의 실시간 통신용
- Chart.js: 차트 및 그래프 생성용

HTML 페이지에는 라인 차트를 표시하는 데 사용되는 ```<canvas>``` 요소도 포함되어 있습니다.

### 브라우저로 데이터 보내기

이제 웹 서버를 가동하고 실행 중이며 HTML 페이지를 제공하고 있으므로 데이터를 브라우저로 전송해 보겠습니다.

우리는 Socket.IO를 사용하여 웹 서버와 브라우저 사이에 실시간 연결을 설정할 것입니다.

```javascript
// Load the Socket.IO library
const io = require('socket.io')(server);

// Send the data to the browser
io.on('connection', socket => {
  setInterval(() => {
    socket.emit('data', data.toArray());
  }, 1000);
});
```

위의 코드는 Socket.IO를 사용하여 매초마다 브라우저에 데이터를 보냅니다.

### 브라우저에서 데이터 받기

이제 브라우저에서 데이터를 수신하고 있으므로 Chart.js를 사용하여 시각화해 보겠습니다.

```javascript
// Connect to the socket.io server
const socket = io('http://localhost:3000');

// Receive the data from the server
socket.on('data', data => {
  // Visualize the data using Chart.js
  const chart = new Chart(document.getElementById('chart'), {
    type: 'line',
    data: {
      labels: data.map((_, i) => i),
      datasets: [{
        label: 'Random Data',
        data: data,
        borderColor: '#ff0000',
        fill: false
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false
    }
  });
});
```

위의 코드는 Chart.js를 사용하여 데이터를 선형 차트로 시각화합니다. 새로운 데이터 포인트가 수신되면 차트가 실시간으로 업데이트됩니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 대화형 시각화를 구축하는 방법을 살펴보았습니다.

TensorFlow.js는 브라우저에서 기계 학습을 가능하게 하는 수치 계산을 위한 강력한 JavaScript 라이브러리입니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

이 두 가지 기술을 함께 사용하여 데이터를 탐색하고 분석하는 데 사용할 수 있는 대화형 시각화를 구축할 수 있습니다.