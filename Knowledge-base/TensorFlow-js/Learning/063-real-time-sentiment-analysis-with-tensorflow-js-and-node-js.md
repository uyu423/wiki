---
title: 063: TensorFlow.js 및 Node.js를 사용한 실시간 감정 분석
description: 
published: true
date: 2023-02-02T21:43:47.137Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:43:45.469Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [063: Real-Time Sentiment Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/063-real-time-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 통한 실시간 감정 분석

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 실시간 감정 분석 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

## 감정 분석이란?

감정 분석은 텍스트에서 의견 기반 정보를 추출하는 프로세스입니다. 이것은 고객 피드백을 이해하거나 뉴스 이벤트에 대한 대중의 반응을 측정하는 것과 같은 다양한 애플리케이션에 유용할 수 있습니다.

## 애플리케이션 구축

다음 도구를 사용하여 애플리케이션을 빌드할 것입니다.

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [소켓.io](https://socket.io/)

### 환경 설정

먼저 개발 환경을 설정해야 합니다. 이 프로젝트에 [Node.js](https://nodejs.org/en/)를 사용할 예정이므로 설치했는지 확인하세요.

Node.js가 설치되면 새 프로젝트 디렉토리를 생성하고 [npm](https://www.npmjs.com/)으로 초기화할 수 있습니다.

```
mkdir sentiment-analysis
cd sentiment-analysis
npm init -y
```

그러면 `sentiment-analysis`라는 새 디렉토리가 생성되고 `package.json` 파일로 초기화됩니다.

다음으로 프로젝트에 대한 종속성을 설치해야 합니다. [TensorFlow.js](https://js.tensorflow.org/) 및 [Socket.io](https://socket.io/)를 사용합니다.

```
npm install @tensorflow/tfjs socket.io
```

그러면 프로젝트에 `@tensorflow/tfjs` 및 `socket.io` 패키지가 설치됩니다.

### 모델 만들기

이제 환경이 설정되었으므로 감정 분석 모델 구축을 시작할 수 있습니다. TensorFlow Hub의 [사전 훈련된 모델](https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2)을 사용할 것입니다.

이 모델을 사용하려면 먼저 TensorFlow.js에 로드해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
const model = await tf.loadModel('https://tfhub.dev/google/tfjs-models/tfjs-sentiment/2/default/1');
```

다음으로 텍스트 문자열을 가져와 0과 1 사이의 점수를 반환하는 함수를 만들어야 합니다. 여기서 0은 음수이고 1은 양수입니다. 텍스트를 모델에 공급하고 출력의 argmax를 취함으로써 이를 수행할 수 있습니다.

```javascript
function getSentiment(text) {
  // Convert the text to a tensor.
  const input = tf.tensor1d([text]);

  // Get the model's predictions.
  const predictions = model.predict(input);

  // Get the highest scoring prediction.
  const argMax = predictions.argMax(-1);

  // We only need the highest scoring prediction's index.
  const index = argMax.dataSync()[0];

  // Get the predicted label.
  const label = (index === 0) ? 'negative' : 'positive';

  // Get the predicted probability.
  const probability = predictions.dataSync()[index];

  return { label, probability };
}
```

이제 모델을 설정했으므로 서버 생성으로 넘어갈 수 있습니다.

### 서버 생성

[Node.js](https://nodejs.org/) 및 [Socket.io](https://socket.io/)를 사용하여 애플리케이션용 서버를 만들 것입니다.

먼저 종속성을 요구해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const io = require('socket.io')();
```

다음으로 소켓에서 들어오는 텍스트를 처리하는 함수를 만들어야 합니다.

```javascript
function handleText(socket, text) {
  // Get the sentiment of the text.
  const { label, probability } = getSentiment(text);

  // Emit the results to the socket.
  socket.emit('results', { label, probability });
}
```

마지막으로 서버를 시작하고 들어오는 연결을 수신 대기해야 합니다.

```javascript
// Start the server.
io.listen(3000);

// Listen for incoming connections.
io.on('connection', (socket) => {
  // Listen for text from the socket.
  socket.on('text', (text) => handleText(socket, text));
});
```

이제 서버를 설정했으므로 클라이언트 생성으로 넘어갈 수 있습니다.

### 클라이언트 만들기

우리는 [Socket.io](https://socket.io/)를 사용하여 애플리케이션용 클라이언트를 만들 것입니다.

먼저 Socket.io 클라이언트 라이브러리를 로드해야 합니다.

```html
<script src="/socket.io/socket.io.js"></script>
```

다음으로 소켓을 만들고 서버에 연결해야 합니다.

```javascript
// Connect to the server.
const socket = io.connect('http://localhost:3000');
```

이제 소켓이 설정되었으므로 서버에 텍스트를 보낼 수 있습니다. 사용자 입력을 수신하고 소켓으로 방출하여 이를 수행합니다.

```javascript
// Listen for user input.
document.querySelector('#text-input').addEventListener('input', (event) => {
  // Get the input text.
  const text = event.target.value;

  // Emit the text to the socket.
  socket.emit('text', text);
});
```

마지막으로 서버에서 결과를 수신하고 사용자에게 표시해야 합니다.

```javascript
// Listen for results from the server.
socket.on('results', (results) => {
  // Get the results element.
  const element = document.querySelector('#results');

  // Clear the element.
  element.innerHTML = '';

  // Create a new paragraph for each result.
  results.forEach((result) => {
    const { label, probability } = result;
    const paragraph = document.createElement('p');
    paragraph.innerHTML = `${label}: ${probability}`;
    element.appendChild(paragraph);
  });
});
```

이제 클라이언트를 설정했으므로 애플리케이션을 테스트할 수 있습니다.

## 애플리케이션 테스트

애플리케이션을 테스트하려면 브라우저에서 `index.html`을 엽니다. 그런 다음 텍스트 입력에 텍스트를 입력하고 Enter 키를 누릅니다. 결과 요소에 결과가 표시되어야 합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 실시간 감정 분석 애플리케이션을 빌드하는 방법을 살펴보았습니다. 또한 TensorFlow Hub에서 사전 훈련된 모델을 사용하는 방법도 살펴보았습니다.

감정 분석에 대해 자세히 알아보려면 다음 리소스를 참조하세요.

- [TensorFlow.js를 이용한 감성 분석](https://medium.com/tensorflow/sentiment-analysis-with-tensorflow-js-bccd4d9d4a30)
- [TensorFlow.js를 이용한 실시간 감정 분석](https://www.tensorflow.org/js/tutorials/sentiment/index)