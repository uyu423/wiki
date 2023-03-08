---
title: 079: 모바일 장치에서 Node.js와 함께 TensorFlow.js 사용
description: 
published: true
date: 2023-02-03T01:17:41.879Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:17:40.285Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [079: Using TensorFlow.js with Node.js on Mobile Devices***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/079-using-tensorflow-js-with-node-js-on-mobile-devices)
{.links-list}


## 소개

TensorFlow.js는 브라우저 또는 Node.js 서버에서 기계 학습 모델을 개발하고 교육하는 데 사용할 수 있는 오픈 소스 라이브러리입니다. 이 게시물에서는 모바일 장치에서 Node.js와 함께 TensorFlow.js를 사용하는 데 중점을 둘 것입니다.

TensorFlow.js는 향상된 유연성 및 이식성과 같은 기존 서버 측 기계 학습 프레임워크에 비해 많은 이점을 제공합니다. 모바일 장치는 리소스가 제한된 경우가 많기 때문에 기계 학습 모델을 장치에서 실행할 수 있다는 것은 큰 이점입니다.

## 환경 설정

시작하기 전에 개발 환경을 설정해야 합니다. Node.js와 TensorFlow.js 라이브러리를 설치해야 합니다.

Node.js는 공식 웹 사이트(https://nodejs.org/en/)에서 다운로드하여 설치할 수 있습니다. Node.js가 설치되면 Node Package Manager(npm)를 사용하여 TensorFlow.js를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

## 안녕하세요, TensorFlow.js!

이제 환경이 설정되었으므로 첫 번째 TensorFlow.js 프로그램을 작성해 보겠습니다.

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Fit the model to the data
const xs = tf.tensor2d([-1.0, 0.0, 1.0, 2.0, 3.0, 4.0], [6, 1]);
const ys = tf.tensor2d([-3.0, -1.0, 1.0, 3.0, 5.0, 7.0], [6, 1]);

model.fit(xs, ys, {epochs: 500}).then(() => {
  // Use the model to predict the output of a new Tensor
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

이 프로그램에서는 먼저 require() 함수를 사용하여 TensorFlow.js 라이브러리를 로드합니다. 그런 다음 tf.sequential() 함수를 사용하여 순차 모델을 정의합니다.

다음으로 tf.layers.dense() 함수를 사용하여 모델에 밀도가 높은 레이어를 추가합니다. 이 계층은 하나의 단위를 가지며 크기 1의 입력을 기대합니다.

레이어를 추가한 후 tf.compile() 함수를 사용하여 모델을 컴파일합니다. 우리는 평균 제곱 오차 손실 함수와 확률적 경사 하강 최적화 프로그램을 사용하기를 원한다고 지정합니다.

마지막으로 tf.fit() 함수를 사용하여 모델을 데이터에 맞춥니다. 우리는 500개의 학습 에포크를 실행하기를 원한다고 지정합니다.

모델이 훈련되면 tf.predict() 함수를 사용하여 새 Tensor의 출력을 예측합니다. 이 경우 Tensor [5]의 출력을 예측합니다.

## 모바일 장치에서 TensorFlow.js 실행

이제 TensorFlow.js 프로그램을 작성하는 방법을 살펴보았으므로 모바일 장치에서 실행하는 방법을 살펴보겠습니다.

모바일 장치에서 TensorFlow.js를 실행하는 방법에는 웹 브라우저를 사용하거나 기본 앱을 사용하는 두 가지 방법이 있습니다.

웹 브라우저를 사용하려면 TensorFlow.js 프로그램이 웹 서버에서 실행 중인지 확인해야 합니다. 모든 웹 서버를 사용할 수 있지만 이 예제에서는 Node.js를 사용합니다.

먼저 http-server npm 패키지를 설치해야 합니다.

```
npm install http-server
```

http-server 패키지가 설치되면 이를 사용하여 명령줄에서 웹 서버를 시작할 수 있습니다.

```
http-server
```

이렇게 하면 포트 8080에서 웹 서버가 시작됩니다. 이제 웹 브라우저에서 http://localhost:8080으로 이동하여 TensorFlow.js 프로그램에 액세스할 수 있습니다.

네이티브 앱을 사용하려면 플랫폼별 TensorFlow.js 라이브러리를 사용해야 합니다. iOS의 경우 TensorFlow Lite Swift 라이브러리(https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/swift)를 사용할 수 있습니다. Android의 경우 TensorFlow Lite Android 라이브러리(https://github.com/tensorflow/tensorflow/tree/master/tensorflow/lite/android)를 사용할 수 있습니다.

## 결론

이 게시물에서는 모바일 장치에서 Node.js와 함께 TensorFlow.js를 사용하는 방법을 살펴보았습니다. TensorFlow.js는 향상된 유연성 및 이식성과 같은 기존 서버 측 기계 학습 프레임워크에 비해 많은 이점을 제공합니다. 모바일 장치는 리소스가 제한된 경우가 많기 때문에 기계 학습 모델을 장치에서 실행할 수 있다는 것은 큰 이점입니다.