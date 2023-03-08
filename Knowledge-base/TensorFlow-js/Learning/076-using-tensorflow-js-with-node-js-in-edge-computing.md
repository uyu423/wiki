---
title: 076: Edge Computing에서 TensorFlow.js를 Node.js와 함께 사용
description: 
published: true
date: 2023-02-03T00:37:57.444Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:37:55.799Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [076: Using TensorFlow.js with Node.js in Edge Computing***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/076-using-tensorflow-js-with-node-js-in-edge-computing)
{.links-list}


# Edge Computing에서 Node.js와 함께 TensorFlow.js 사용

TensorFlow.js는 데이터 흐름 그래프를 사용한 수치 계산을 위한 오픈 소스 라이브러리입니다. 에지 장치에서 기계 학습 모델을 교육하고 배포하기 위해 Node.js에서 사용할 수 있습니다.

이 게시물에서는 TensorFlow.js를 Node.js와 함께 사용하여 에지 장치에서 기계 학습 모델을 교육하고 배포하는 방법을 살펴보겠습니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 데이터 흐름 그래프를 사용한 수치 계산을 위한 오픈 소스 라이브러리입니다. TensorFlow.js는 브라우저와 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

TensorFlow.js는 원래 TensorFlow 기계 학습 플랫폼과 함께 사용하기 위해 Google Brain 팀에서 개발했습니다.

## Node.js가 무엇인가요?

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다. Node.js는 서버 측 애플리케이션 개발을 위한 오픈 소스 크로스 플랫폼 런타임 환경입니다.

Node.js 애플리케이션은 JavaScript로 작성되며 OS X, Microsoft Windows, Linux 및 FreeBSD의 Node.js 런타임 내에서 실행할 수 있습니다.

## 시작하기

TensorFlow.js를 Node.js와 함께 사용하려면 다음을 설치해야 합니다.

- Node.js
- TensorFlow.js

다음 명령을 사용하여 Node.js 및 TensorFlow.js를 설치할 수 있습니다.

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

```
npm install @tensorflow/tfjs
```

## 헬로월드

TensorFlow.js 및 Node.js를 사용하여 간단한 "Hello World" 프로그램을 만들어 보겠습니다.

"hello-world.js"라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
const tf = require('@tensorflow/tfjs');

tf.tensor([1, 2, 3, 4]).print();
```

다음 명령을 사용하여 프로그램을 실행합니다.

```
node hello-world.js
```

다음 출력이 표시되어야 합니다.

```
Tensor
    [[1],
     [2],
     [3],
     [4]]
```

## 기계 학습 모델 교육

TensorFlow.js를 Node.js와 함께 사용하는 방법을 살펴보았으니 이제 간단한 기계 학습 모델을 교육해 보겠습니다.

70,000개의 손글씨 숫자 이미지로 구성된 MNIST 데이터 세트를 사용할 것입니다. 이미지 크기는 28x28픽셀입니다.

MNIST 데이터 세트는 교육용 이미지 60,000개, 테스트용 이미지 10,000개, 검증용 이미지 10,000개로 세 부분으로 나뉩니다.

TensorFlow.js 레이어 API를 사용하여 기계 학습 모델을 구축할 것입니다. 레이어 API는 신경망을 쉽게 구축할 수 있게 해주는 고급 API입니다.

먼저 MNIST 데이터 세트를 로드해야 합니다. tf.data API를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();
}

run();
```

다음으로 tf.sequential API를 사용하여 기계 학습 모델을 정의합니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });
}

run();
```

기계 학습 모델을 정의했으므로 이제 학습해야 합니다. tf.fit API를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  return model.fit(images, labels, {
    batchSize,
    epochs
  });
}

run();
```

기계 학습 모델이 훈련되면 이를 사용하여 새로운 데이터를 예측할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## 기계 학습 모델 배포

기계 학습 모델을 교육하고 나면 추론을 위해 이를 에지 장치에 배포할 수 있습니다.

TensorFlow.js Node.js API를 사용하여 기계 학습 모델을 에지 장치에 배포할 것입니다. Node.js API는 Node.js에서 TensorFlow.js 프로그램을 실행할 수 있게 해주는 저수준 API입니다.

먼저 기계 학습 모델을 TensorFlow.js Node.js 형식으로 변환해야 합니다. tf.node.save API를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');
}

run();
```

기계 학습 모델이 TensorFlow.js Node.js 형식으로 변환되면 에지 장치에 배포할 수 있습니다.

에지 장치에 TensorFlow.js Node.js API를 설치해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

이제 TensorFlow.js Node.js API가 설치되었으므로 tf.node.load API를 사용하여 기계 학습 모델을 로드할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');

async function run() {
  const model = await tf.node.load('model.json');
}

run();
```

기계 학습 모델이 로드되면 이를 사용하여 새 데이터를 예측할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');

const mnistData = require('./mnist_dataset');

async function run() {
  const { images, labels } = await mnistData.getData();

  const model = tf.sequential();

  model.add(tf.layers.conv2d({
    inputShape: [28, 28, 1],
    kernelSize: 5,
    filters: 8,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    activation: 'relu',
    kernelInitializer: 'varianceScaling'
  }));

  model.add(tf.layers.maxPooling2d({ poolSize: [2, 2], strides: [2, 2] }));

  model.add(tf.layers.flatten());

  model.add(tf.layers.dense({
    units: 10,
    kernelInitializer: 'varianceScaling',
    activation: 'softmax'
  }));

  const optimizer = tf.train.adam();

  model.compile({
    optimizer: optimizer,
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy'],
  });

  const batchSize = 64;
  const epochs = 10;

  model.fit(images, labels, {
    batchSize,
    epochs
  });

  tf.node.save(model, 'model.json');

  const testImages = images.slice(0, 1000);
  const testLabels = labels.slice(0, 1000);

  const accuracy = model.evaluate(testImages, testLabels);

  console.log('Accuracy:', accuracy[1]);
}

run();
```

## 결론

이 게시물에서는 TensorFlow.js를 Node.js와 함께 사용하여 에지 장치에서 기계 학습 모델을 교육하고 배포하는 방법을 살펴보았습니다.

TensorFlow.js는 에지 장치에서 기계 학습 모델을 훈련하고 배포하는 데 사용할 수 있는 수치 계산을 위한 강력한 라이브러리입니다.

Node.js는 에지 장치에서 TensorFlow.js 프로그램을 실행하는 데 사용할 수 있는 JavaScript 런타임입니다.

TensorFlow.js Node.js API는 Node.js에서 TensorFlow.js 프로그램을 실행할 수 있게 해주는 저수준 API입니다.

## 자원

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)
- [ MNIST 데이터셋](http://yann.lecun.com/exdb/mnist/)