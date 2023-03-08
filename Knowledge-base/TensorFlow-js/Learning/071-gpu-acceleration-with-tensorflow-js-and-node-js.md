---
title: 071: TensorFlow.js 및 Node.js를 사용한 GPU 가속
description: 
published: true
date: 2023-02-02T20:24:33.638Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:24:31.989Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [071: GPU Acceleration with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/071-gpu-acceleration-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 GPU 가속

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 강력하고 유연한 JavaScript 라이브러리입니다. Node.js는 서버 측 스크립팅과 빠른 네트워크 애플리케이션을 지원하는 JavaScript 런타임입니다.

TensorFlow.js 및 Node.js를 사용하면 웹과 Node.js 서버에서 기계 학습 모델을 교육하고 배포할 수 있습니다. TensorFlow.js는 웹 브라우저 및 Node.js 서버에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript API를 제공합니다. Node.js를 사용하면 서버에서 JavaScript를 실행할 수 있습니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 웹 및 Node.js 서버에서 기계 학습 모델을 교육하고 배포하는 방법을 보여줍니다.

## 전제 조건

이 게시물을 따라하려면 다음이 필요합니다.

- 웹 브라우저와 인터넷 연결이 가능한 컴퓨터
- 텍스트 편집기
- 컴퓨터에 설치된 Node.js

## TensorFlow.js 설치하기

TensorFlow.js를 설치하려면 Node.js 패키지 관리자(npm)를 사용할 수 있습니다.

```
npm install @tensorflow/tfjs
```

## 안녕하세요, TensorFlow.js

TensorFlow.js로 간단한 기계 학습 모델을 교육하고 배포하는 것부터 시작하겠습니다. 우리는 손으로 쓴 숫자의 이미지로 구성된 MNIST 데이터 세트를 사용할 것입니다.

먼저 MNIST 데이터 세트를 로드해야 합니다. TensorFlow.js MNIST Dataset 클래스를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = new tf.MNISTDataset();
```

다음으로 MNIST 데이터 세트에서 기계 학습 모델을 교육해야 합니다. CNN(Convolutional Neural Network)이라는 딥 러닝 모델을 사용합니다. CNN은 이미지와 함께 작동하도록 설계된 일종의 신경망입니다.

TensorFlow.js 레이어 API를 사용하여 CNN을 교육할 수 있습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});
```

이제 기계 학습 모델이 있으므로 MNIST 데이터 세트에서 훈련할 수 있습니다. TensorFlow.js 적합 API를 사용하여 모델을 교육합니다.

```javascript
const trainXs = mnistData.getTrainImagesAsTensors();
const trainYs = mnistData.getTrainLabelsAsTensors();

model.fit(trainXs, trainYs, {
  epochs: 10,
  batchSize: 64
});
```

모델이 학습된 후 MNIST 테스트 데이터 세트에서 평가할 수 있습니다. TensorFlow.js 평가 API를 사용하여 모델을 평가합니다.

```javascript
const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);
```

평가 API는 테스트 데이터 세트에서 모델의 손실 및 정확도를 반환합니다.

## TensorFlow.js 모델 배포

기계 학습 모델이 학습되면 웹 서버 또는 Node.js 서버에 배포할 수 있습니다.

모델을 웹 서버에 배포하는 것으로 시작하겠습니다. TensorFlow.js 모델 변환기 API를 사용하여 이를 수행할 수 있습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);
```

모델 변환기 API는 모델의 JSON 표현을 반환합니다. 이 JSON 표현은 모델을 웹 서버에 배포하는 데 사용할 수 있습니다.

모델을 웹 서버에 배포하려면 HTML 파일과 JavaScript 파일을 만들어야 합니다. HTML 파일에는 TensorFlow.js 모델이 로드될 요소가 포함됩니다. JavaScript 파일에는 모델을 요소에 로드하는 코드가 포함됩니다.

다음은 HTML 파일의 예입니다.

```html
<html>
  <head>
    <title>TensorFlow.js MNIST Example</title>
  </head>
  <body>
    <h1>TensorFlow.js MNIST Example</h1>
    <div id="container"></div>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="mnist.js"></script>
  </body>
</html>
```

다음은 JavaScript 파일의 예입니다.

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

HTML 파일에는 TensorFlow.js 스크립트와 mnist.js 스크립트가 포함되어 있습니다. mnist.js 스크립트에는 id가 "container"인 요소에 모델을 로드하는 코드가 포함되어 있습니다.

HTML 파일을 실행하려면 웹 서버를 시작해야 합니다. Node.js http-server 모듈을 사용하여 웹 서버를 시작할 수 있습니다.

```
npm install http-server -g

http-server
```

http-server 모듈은 포트 8080에서 웹 서버를 시작합니다. http://localhost:8080에서 HTML 파일에 액세스할 수 있습니다.

## Node.js 서버에서 TensorFlow.js 모델 실행

Node.js 서버에서 TensorFlow.js 모델을 실행할 수도 있습니다. 이렇게 하려면 TensorFlow.js Node.js API를 사용해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');

const model = tf.sequential();

model.add(tf.layers.conv2d({
  inputShape: [28, 28, 1],
  filters: 32,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.conv2d({
  filters: 64,
  kernelSize: 3,
  activation: 'relu'
}));

model.add(tf.layers.maxPooling2d({ poolSize: [2, 2] }));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({ units: 64, activation: 'relu' }));

model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));

model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

const mnistData = new tf.MNISTDataset();

const testXs = mnistData.getTestImagesAsTensors();
const testYs = mnistData.getTestLabelsAsTensors();

model.evaluate(testXs, testYs);

const converter = tf.modelConverter.createConverter({
  from: 'tensorflowjs_layers_model'
});

const json = converter.toJSON(model);

tf.loadLayersModel('http://localhost:8080/model.json').then(function(model) {
  model.predict(testXs).then(function(predictions) {
    console.log(predictions);
  });
});
```

위의 코드에서 MNIST 데이터 세트를 로드하고 머신 러닝 모델을 교육했습니다. 그런 다음 모델을 JSON 표현으로 변환하고 Node.js 서버에 로드했습니다.

위의 코드를 실행하려면 Node.js 서버를 시작해야 합니다. Node.js Express 모듈을 사용하여 Node.js 서버를 시작할 수 있습니다.

```
npm install express -g

express
```

Express 모듈은 포트 3000에서 Node.js 서버를 시작합니다. http://localhost:3000에서 서버에 액세스할 수 있습니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 웹 및 Node.js 서버에서 기계 학습 모델을 교육하고 배포하는 방법을 보여 주었습니다.

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 강력하고 유연한 JavaScript 라이브러리입니다. Node.js는 서버 측 스크립팅과 빠른 네트워크 애플리케이션을 지원하는 JavaScript 런타임입니다.

TensorFlow.js 및 Node.js를 사용하면 웹과 Node.js 서버에서 기계 학습 모델을 교육하고 배포할 수 있습니다. TensorFlow.js는 웹 브라우저 및 Node.js 서버에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript API를 제공합니다. Node.js를 사용하면 서버에서 JavaScript를 실행할 수 있습니다.