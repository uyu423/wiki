---
title: 032: Node.js로 TensorFlow.js 모델 배포
description: 
published: true
date: 2023-02-02T14:36:46.681Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:36:44.819Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [032: Deploying TensorFlow.js Models with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/032-deploying-tensorflow-js-models-with-node-js)
{.links-list}


# 032: Node.js로 TensorFlow.js 모델 배포

TensorFlow.js는 개발자가 브라우저 또는 Node.js에서 ML 모델을 교육하고 배포할 수 있게 해주는 기계 학습용 오픈 소스 JavaScript 라이브러리입니다.

이 게시물에서는 TensorFlow.js를 사용하여 Node.js 애플리케이션에 사전 훈련된 ML 모델을 배포하는 방법을 알아봅니다. 또한 Node.js API를 사용하여 모델에서 추론을 실행하는 방법도 배웁니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

* Node.js
* 텍스트 편집기
* 웹 브라우저

## 시작하기

먼저 TensorFlow.js 라이브러리를 설치해야 합니다. NPM(노드 패키지 관리자)을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 사전 학습된 ML 모델을 다운로드해야 합니다. 이 예에서는 [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet) 이미지 분류 모델을 사용합니다.

모델이 다운로드되면 Node.js 애플리케이션에 배포할 수 있습니다.

## 모델 배포

모델을 배포하려면 `index.js`라는 새 파일을 만들어야 합니다. 이 파일에서 `tf.loadModel()` 함수를 사용하여 사전 학습된 모델을 로드합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
  });
```

## 모델 사용

모델이 로드되면 이를 사용하여 이미지에 대한 추론을 실행할 수 있습니다. 이 예시에서는 [TensorFlow.js 이미지 분류 예시](https://github.com/tensorflow/tfjs-examples/tree/master/image-classification)를 사용합니다.

먼저 이미지를 `tf.Tensor`에 로드해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);
  });
```

다음으로 `mobilenet.preprocessInput()` 함수를 사용하여 이미지를 사전 처리해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);
  });
```

마지막으로 `model.predict()` 함수를 사용하여 이미지에 대한 추론을 실행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the model.
tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json')
  .then(model => {
    // Use the model.
    const img = tf.tensor3d(imageData, [224, 224, 3]);

    // Pre-process the image.
    const preprocessedImg = tf.mobilenet.preprocessInput(img);

    // Run inference.
    model.predict(preprocessedImg).then(predictions => {
      // Use the predictions.
    });
  });
```

'예측' 변수에는 추론 결과가 포함됩니다.

## 결론

이 게시물에서는 TensorFlow.js를 사용하여 Node.js 애플리케이션에서 사전 훈련된 ML 모델을 배포하는 방법을 배웠습니다. 또한 Node.js API를 사용하여 모델에서 추론을 실행하는 방법도 배웠습니다.