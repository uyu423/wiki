---
title: 061: TensorFlow.js 및 Node.js를 사용한 실시간 개체 감지
description: 
published: true
date: 2023-02-02T21:17:45.230Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:17:43.579Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [061: Real-Time Object Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/061-real-time-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# 061: TensorFlow.js 및 Node.js를 사용한 실시간 객체 감지

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 실시간 개체 감지를 수행하는 방법을 알아봅니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 자바스크립트 기계 학습을 위한 오픈 소스 라이브러리입니다. 이를 통해 브라우저 또는 Node.js 환경에서 기계 학습 모델을 훈련하고 실행할 수 있습니다.

## Node.js가 무엇인가요?

Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있는 JavaScript 런타임 환경입니다.

## TensorFlow.js 및 Node.js를 사용하여 실시간 객체 감지를 수행하려면 어떻게 해야 합니까?

TensorFlow.js 및 Node.js를 사용하여 다음을 통해 실시간 객체 감지를 수행할 수 있습니다.

1. 이미지에서 객체를 감지하도록 기계 학습 모델을 교육합니다.
2. 모델을 Node.js 서버에 배포합니다.
3. 서버를 사용하여 들어오는 이미지를 처리하고 실시간으로 개체를 감지합니다.

## 1. 이미지에서 객체를 감지하도록 기계 학습 모델 교육

이미지에서 개체를 감지하는 기계 학습 모델을 교육하는 것부터 시작하겠습니다. 이를 위해 MobileNet 모델을 사용합니다. MobileNet은 대규모 이미지 데이터 세트에 대해 훈련된 사전 훈련된 모델입니다.

MobileNet을 사용하여 다음을 통해 물체 감지를 수행할 수 있습니다.

1. MobileNet 모델을 로드합니다.
2. 이미지를 모델에 전달합니다.
3. 모델의 예측을 얻습니다.

코드에서 이 작업을 수행하는 방법을 살펴보겠습니다.

```javascript
// Load the MobileNet model.
const model = await mobilenet.load();

// Classify the image.
const predictions = await model.classify(image);

// Get the model's predictions.
console.log(predictions);
```

## 2. Node.js 서버에 모델 배포

모델을 교육하고 나면 Node.js 서버에 배포할 수 있습니다. 이를 통해 들어오는 이미지를 처리하고 실시간으로 개체를 감지할 수 있습니다.

이렇게 하려면 다음이 필요합니다.

1. TensorFlow.js 라이브러리를 설치합니다.
2. Node.js 라이브러리를 설치합니다.
3. Node.js 서버를 생성합니다.
4. 모델을 서버에 배포합니다.

코드에서 이 작업을 수행하는 방법을 살펴보겠습니다.

```javascript
// Install the TensorFlow.js library.
npm install @tensorflow/tfjs

// Install the Node.js library.
npm install node

// Create a Node.js server.
const tf = require('@tensorflow/tfjs');
const express = require('express');
const app = express();

//Deploy the model to the server.
app.use(express.static(__dirname + '/model'));

// Process incoming images and detect objects in real-time.
app.post('/api/detect', async (req, res) => {
  // Classify the image.
  const predictions = await model.classify(req.body.image);

  // Send the predictions to the client.
  res.json(predictions);
});

// Start the server.
app.listen(3000, () => console.log('Server is running on port 3000'));
```

## 3. 서버를 사용하여 들어오는 이미지를 처리하고 실시간으로 개체를 감지합니다.

서버가 가동되고 실행되면 서버를 사용하여 들어오는 이미지를 처리하고 객체를 실시간으로 감지할 수 있습니다.

이렇게 하려면 다음이 필요합니다.

1. 이미지를 서버로 보냅니다.
2. 서버는 이미지를 처리하고 예측을 반환합니다.
3. 예측을 사용하여 이미지에서 객체를 감지할 수 있습니다.

코드에서 이 작업을 수행하는 방법을 살펴보겠습니다.

```javascript
// Send an image to the server.
const image = 'some-image.jpg';

fetch('/api/detect', {
  method: 'POST',
  body: JSON.stringify({ image }),
})
  .then(res => res.json())
  .then(predictions => {
    // Use the predictions to detect objects in the image.
    console.log(predictions);
  });
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 실시간 객체 감지를 수행하는 방법을 배웠습니다.