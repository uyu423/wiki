---
title: 053: Node.js에서 Express.js와 함께 TensorFlow.js 사용
description: 
published: true
date: 2023-02-02T19:17:22.832Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:17:21.181Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [053: Using TensorFlow.js with Express.js in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/053-using-tensorflow-js-with-express-js-in-node-js)
{.links-list}


# Node.js에서 Express.js와 함께 TensorFlow.js 사용

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. Node.js에서 Express.js 웹 프레임워크와 함께 사용하여 강력한 애플리케이션을 만들 수 있습니다. 이 게시물에서는 TensorFlow.js 및 Express.js를 시작하는 방법을 보여줍니다.

## 종속성 설치

먼저 프로젝트에 대한 종속성을 설치해야 합니다. Express.js와 TensorFlow.js가 필요합니다. 다음 명령으로 설치할 수 있습니다.

```
npm install express @tensorflow/tfjs
```

## 안녕하세요 세상

종속성을 설치했으므로 이제 간단한 "Hello world" 애플리케이션을 만들어 보겠습니다. 프로젝트의 루트 디렉터리에 `index.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const tf = require('@tensorflow/tfjs');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

이 코드는 포트 3000에서 수신하고 "Hello, world!"로 응답하는 Express.js 서버를 생성합니다. 루트 URL에 액세스할 때.

## TensorFlow.js 사용

간단한 Express.js 서버를 가동하고 실행 중이므로 TensorFlow.js 코드를 추가해 보겠습니다. TensorFlow.js 모델에서 생성된 문자열로 응답하는 경로를 추가하는 것으로 시작하겠습니다.

먼저 모델을 만들어야 합니다. `model.js`라는 파일에서 이 작업을 수행합니다. 입력 문자열을 받아서 출력 문자열을 생성하는 간단한 모델을 만들 것입니다. 입력 문자열은 원-핫 인코딩된 벡터로 모델에 공급됩니다. 출력 문자열은 sequence-to-sequence 아키텍처를 사용하여 모델에서 생성됩니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Create the model
const model = tf.sequential();

// Add an LSTM layer
model.add(tf.layers.lstm({
  units: 8,
  inputShape: [8],
  returnSequences: true
}));

// Add a second LSTM layer
model.add(tf.layers.lstm({
  units: 8,
  returnSequences: true
}));

// Add a dense layer
model.add(tf.layers.dense({
  units: 8,
  activation: 'softmax'
}));

// Compile the model
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'rmsprop'
});

// Export the model
module.exports = model;
```

이 코드는 간단한 LSTM 기반 모델을 생성합니다. 이 모델은 8자의 입력 문자열을 사용하여 8자의 문자열을 출력합니다.

이제 모델이 있으므로 모델을 사용하는 경로를 추가할 수 있습니다. `index.js` 파일에 다음 경로를 추가합니다.

```javascript
app.get('/generate', (req, res) => {
  // Load the model
  const model = require('./model');

  // Generate a string
  const string = model.predict(tf.oneHot('Hello, world!'.split(''), 8));

  // Send the string to the client
  res.send(string);
});
```

이 경로는 `model.js`에서 생성한 모델을 로드하고 이를 사용하여 문자열을 생성합니다. 그런 다음 생성된 문자열이 클라이언트로 전송됩니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Express.js를 시작하는 방법을 보여 주었습니다. 간단한 "Hello world" 애플리케이션과 TensorFlow.js 모델을 사용하여 문자열을 생성하는 경로를 만들었습니다.

## 자원

- [TensorFlow.js](https://js.tensorflow.org/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)