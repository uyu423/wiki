---
title: 085: TensorFlow.js 및 Node.js를 사용하여 엔드투엔드 기계 학습 워크플로 구축
description: 
published: true
date: 2023-02-03T02:44:28.119Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:44:26.394Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [085: Building End-to-End Machine Learning Workflows with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/085-building-end-to-end-machine-learning-workflows-with-tensorflow-js-and-node-js)
{.links-list}


# 085: TensorFlow.js 및 Node.js로 엔드투엔드 기계 학습 워크플로 구축

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 종단 간 기계 학습 워크플로를 구축하는 방법을 살펴보겠습니다.

TensorFlow.js는 브라우저에서 기계 학습 모델을 생성하고 교육하기 위한 강력한 툴킷입니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

이 두 가지 기술을 함께 사용하면 어디에나 배포할 수 있는 완전한 기계 학습 워크플로를 구축할 수 있습니다.

## 환경 설정

엔드투엔드 기계 학습 워크플로를 구축하는 방법에 대해 자세히 알아보기 전에 잠시 시간을 내어 개발 환경을 설정해 보겠습니다.

머신에 Node.js와 npm이 설치되어 있어야 합니다. 여기에서 지침을 찾을 수 있습니다.

https://nodejs.org/en/download/

Node.js 및 npm이 설치되면 다음 명령을 실행하여 TensorFlow.js CLI 도구를 설치할 수 있습니다.

```
npm install -g @tensorflow/tfjs-node
```

## 새 프로젝트 생성

이제 환경이 설정되었으므로 새 프로젝트를 생성해 보겠습니다. 새 npm 프로젝트를 초기화하는 것으로 시작하겠습니다.

```
npm init
```

이렇게 하면 프로젝트 디렉토리에 `package.json`이라는 파일이 생성됩니다. 이 파일에는 프로젝트에 필요한 종속성을 포함하여 프로젝트에 대한 정보가 들어 있습니다.

다음으로 프로젝트에 필요한 TensorFlow.js 및 Node.js 종속 항목을 설치합니다.

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

## 기계 학습 모델 구축

이제 프로젝트가 설정되었으므로 기계 학습 모델 구축을 시작하겠습니다.

프로젝트 디렉토리에 `model.js`라는 파일을 생성하는 것으로 시작하겠습니다. 이 파일에는 기계 학습 모델의 코드가 포함됩니다.

먼저 사용할 TensorFlow.js 및 Node.js 라이브러리를 로드해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
```

다음으로 모델을 구성하는 데 사용할 몇 가지 상수를 정의합니다.

```javascript
const MODEL_PATH = './model.json';
const INPUT_SHAPE = [28, 28, 1];
const NUM_CLASSES = 10;
```

`MODEL_PATH` 상수는 훈련된 모델을 포함할 파일의 경로를 정의합니다. 'INPUT_SHAPE' 상수는 모델이 훈련될 입력 데이터의 모양을 정의합니다. `NUM_CLASSES` 상수는 모델이 예측하도록 학습할 출력 클래스의 수를 정의합니다.

다음으로 기계 학습 모델을 구축할 함수를 정의합니다.

```javascript
function buildModel() {
  // We're building a simple machine learning model here
  const model = tf.sequential();
  
  // The first layer of our model is a convolutional layer
  model.add(tf.layers.conv2d({
    inputShape: INPUT_SHAPE,
    kernelSize: 3,
    filters: 16,
    activation: 'relu'
  }));
  
  // The second layer of our model is a pooling layer
  model.add(tf.layers.maxPooling2d({poolSize: 2, strides: 2}));
  
  // The third layer of our model is a flatten layer
  model.add(tf.layers.flatten());
  
  // The fourth layer of our model is a dense layer
  model.add(tf.layers.dense({units: NUM_CLASSES, activation: 'softmax'}));
  
  // We need to compile our model before we can train it
  model.compile({
    optimizer: tf.train.adam(),
    loss: 'categoricalCrossentropy',
    metrics: ['accuracy']
  });
  
  return model;
}
```

이 함수는 4개 계층으로 구성된 간단한 기계 학습 모델을 정의합니다.

- 컨볼루션 레이어
- 풀링 레이어
- 평평한 층
- 조밀한 층

컨볼루션 계층은 입력 데이터에서 특징을 추출하는 역할을 합니다. 풀링 계층은 데이터 다운샘플링을 담당합니다. 병합 레이어는 데이터를 병합하는 역할을 합니다. 밀집 계층은 추출된 기능을 출력 클래스에 매핑하는 역할을 합니다.

모델을 정의한 후에는 모델을 훈련시키기 전에 컴파일해야 합니다. 모델을 컴파일하면 훈련을 위해 모델이 구성됩니다. 사용하려는 옵티마이저, 손실 함수 및 메트릭을 지정해야 합니다.

이 경우에는 `adam` 옵티마이저, `categoricalCrossentropy` 손실 함수 및 `accuracy` 메트릭을 사용하고 있습니다.

## 모델 교육

이제 모델을 정의했으므로 모델을 훈련해 보겠습니다. 교육 데이터를 로드하는 것으로 시작하겠습니다.

학습 데이터는 `./data/train.csv` 파일에 저장됩니다. 이 파일에는 레이블과 함께 손으로 쓴 숫자의 28x28 이미지가 포함되어 있습니다.

이 파일의 내용을 읽기 위해 `fs` 모듈을 사용할 것입니다:

```javascript
const trainData = fs.readFileSync('./data/train.csv', {encoding: 'utf8'});
```

다음으로 이 데이터를 `tf.tensor`의 배열로 구문 분석합니다.

```javascript
const trainTensors = tf.tensor2d(trainData.split('\n').map(row => row.split(',').map(Number)));
```

이제 교육 데이터가 로드되어 사용할 준비가 되었습니다.

다음으로 모델을 교육할 함수를 정의합니다.

```javascript
async function trainModel(model, trainTensors) {
  // We're training our model for 10 epochs
  const epochs = 10;
  
  // We're using a batch size of 32
  const batchSize = 32;
  
  // We're using the fit method to train our model
  await model.fit(trainTensors, {
    epochs: epochs,
    batchSize: batchSize
  });
}
```

이 함수는 배치 크기 32를 사용하여 10 epoch 동안 모델을 훈련합니다.

모델이 훈련되면 모델을 `MODEL_PATH` 파일에 저장합니다.

```javascript
model.save(MODEL_PATH);
```

## 모델 평가

이제 모델이 학습되었으므로 모델을 평가해 보겠습니다. 테스트 데이터를 로드하는 것으로 시작하겠습니다.

테스트 데이터는 `./data/test.csv` 파일에 저장됩니다. 이 파일에는 레이블과 함께 손으로 쓴 숫자의 28x28 이미지가 포함되어 있습니다.

이 파일의 내용을 읽기 위해 `fs` 모듈을 사용할 것입니다:

```javascript
const testData = fs.readFileSync('./data/test.csv', {encoding: 'utf8'});
```

다음으로 이 데이터를 `tf.tensor`의 배열로 구문 분석합니다.

```javascript
const testTensors = tf.tensor2d(testData.split('\n').map(row => row.split(',').map(Number)));
```

이제 테스트 데이터가 로드되어 사용할 준비가 되었습니다.

다음으로 모델을 평가할 함수를 정의합니다.

```javascript
async function evaluateModel(model, testTensors) {
  // We're using the evaluate method to evaluate our model
  const results = await model.evaluate(testTensors);
  
  // We're logging the loss and accuracy of our model
  console.log(`loss: ${results[0]} - accuracy: ${results[1]}`);
}
```

이 함수는 테스트 데이터에서 모델을 평가합니다.

## 모델로 예측하기

모델이 훈련되고 평가되었으므로 모델을 사용하여 예측해 보겠습니다.

예측하려는 이미지를 로드하는 것으로 시작하겠습니다. 이미지는 `./data/image.png` 파일에 저장됩니다.

이 파일의 내용을 읽기 위해 `fs` 모듈을 사용할 것입니다:

```javascript
const imageData = fs.readFileSync('./data/image.png');
```

다음으로 이 데이터를 `tf.tensor`로 구문 분석합니다.

```javascript
const imageTensor = tf.tensor3d(imageData, [28, 28, 1]);
```

이제 이미지 데이터가 로드되어 사용할 준비가 되었습니다.

다음으로 모델을 사용하여 예측을 수행할 함수를 정의합니다.

```javascript
async function predict(model, imageTensor) {
  // We're using the predict method to make a prediction
  const prediction = await model.predict(imageTensor);
  
  // We're logging the prediction that our model made
  console.log(prediction);
}
```

이 함수는 이미지 데이터를 예측합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 종단 간 기계 학습 워크플로를 구축하는 방법을 살펴보았습니다.

개발 환경을 설정하는 방법, 새 프로젝트를 만드는 방법, 기계 학습 모델을 구축하는 방법, 모델을 교육하는 방법, 모델을 평가하는 방법 및 모델을 사용하여 예측하는 방법을 살펴보았습니다.

TensorFlow.js 및 Node.js에 대해 자세히 알아보려면 다음 리소스를 참조하세요.

- TensorFlow.js 문서: https://js.tensorflow.org/
- Node.js 문서: https://nodejs.org/en/docs/