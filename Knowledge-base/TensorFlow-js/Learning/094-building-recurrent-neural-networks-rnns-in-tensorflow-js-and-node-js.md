---
title: 094: TensorFlow.js 및 Node.js에서 순환 신경망(RNN) 구축
description: 
published: true
date: 2023-02-03T05:05:04.341Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:05:02.678Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [094: Building Recurrent Neural Networks (RNNs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/094-building-recurrent-neural-networks-rnns-in-tensorflow-js-and-node-js)
{.links-list}


# 소개

순환 신경망(RNN)은 노드 간의 연결이 시간적 또는 공간적 순서를 따라 방향성 그래프를 형성하는 일종의 인공 신경망입니다. 이를 통해 시계열 또는 일련의 이벤트에 대한 시간적 동적 동작을 나타낼 수 있습니다.

이 게시물에서는 TensorFlow.js 및 Node.js에서 RNN을 빌드할 것입니다. TensorFlow.js는 웹 및 JavaScript용 오픈 소스 하드웨어 가속 기계 학습 라이브러리입니다. Node.js는 서버 측 JavaScript 코드를 작성할 수 있는 교차 플랫폼 런타임 환경입니다.

2013년 1월 1일부터 2016년 12월 31일까지 Apple, Inc.(AAPL)의 일일 주가 데이터 세트를 사용할 것입니다. 목표는 2017년 1월 1일의 시가를 예측하는 것입니다.

# 전제 조건

시작하기 전에 다음과 같은 몇 가지 사항이 필요합니다.

- 인공 신경망에 대한 기본 지식
- 자바스크립트에 익숙하신 분
- 텍스트 편집기
- 웹 브라우저

# 시작하기

## TensorFlow.js 설치하기

TensorFlow.js를 설치하려면 npm 또는 yarn과 같은 패키지 관리자를 사용할 수 있습니다.

```
npm install @tensorflow/tfjs
```

```
yarn add @tensorflow/tfjs
```

또는 스크립트 태그가 있는 HTML 파일에 TensorFlow.js 라이브러리를 포함할 수 있습니다.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

## Node.js 설치하기

Node.js를 설치하려면 [Node.js 웹사이트](https://nodejs.org/en/)에서 설치 프로그램을 다운로드할 수 있습니다.

## 데이터세트 다운로드

우리가 사용할 데이터 세트는 [여기](https://www.kaggle.com/camnugent/sandp500)에서 사용할 수 있습니다. CSV 파일을 다운로드하고 JavaScript 파일과 동일한 디렉터리에 저장합니다.

# RNN 구축

## 데이터세트 로드

TensorFlow.js에 데이터세트를 로드하는 것으로 시작하겠습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const data = tf.loadCSV('AAPL.csv');
```

## 데이터 전처리

다음으로 데이터를 교육 및 테스트 세트로 분할합니다. 또한 0과 1 사이가 되도록 데이터의 크기를 조정합니다. 이는 신경망에 대한 일반적인 전처리 단계입니다.

```javascript
const train_data = data.slice(0, data.length - 7);
const test_data = data.slice(data.length - 7);

const train_x = train_data.map(row => row.slice(1, row.length - 1));
const train_y = train_data.map(row => row[row.length - 1]);

const test_x = test_data.map(row => row.slice(1, row.length - 1));
const test_y = test_data.map(row => row[row.length - 1]);

const x_min = Math.min(...train_x.map(row => Math.min(...row)));
const x_max = Math.max(...train_x.map(row => Math.max(...row)));

const y_min = Math.min(...train_y);
const y_max = Math.max(...train_y);

const train_x_scaled = train_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));
const test_x_scaled = test_x.map(row => row.map(col => (col - x_min) / (x_max - x_min)));

const train_y_scaled = train_y.map(val => (val - y_min) / (y_max - y_min));
const test_y_scaled = test_y.map(val => (val - y_min) / (y_max - y_min));
```

## 모델 구축

이제 RNN을 구축할 수 있습니다. 순차 모델을 만드는 것부터 시작하겠습니다.

```javascript
const model = tf.sequential();
```

다음으로 모델에 반복 레이어를 추가합니다. 이 레이어는 10개의 유닛과 1의 입력 형태를 가집니다.

```javascript
model.add(tf.layers.simpleRNN({units: 10, inputShape: [1]}));
```

마지막으로 단일 단위와 출력 모양이 1인 dense 레이어를 추가합니다. 이것은 예측 주가를 출력할 레이어입니다.

```javascript
model.add(tf.layers.dense({units: 1, inputShape: [10]}));
```

## 모델 컴파일

이제 모델을 구축했으므로 모델을 훈련시키기 전에 컴파일해야 합니다. 우리는 평균 제곱 오차(MSE)를 손실 함수와 Adam 옵티마이저로 사용할 것입니다.

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

## 모델 교육

이제 모델을 교육할 준비가 되었습니다. 우리는 그것을 10 에포크 동안 훈련시키고 배치 크기 1을 사용할 것입니다.

```javascript
model.fit(tf.tensor2d(train_x_scaled, [train_x_scaled.length, 1]), tf.tensor2d(train_y_scaled, [train_y_scaled.length, 1]), {
  epochs: 10,
  batchSize: 1
});
```

## 주가 예측

이제 모델이 학습되었으므로 이를 사용하여 테스트 세트에 대한 예측을 수행할 수 있습니다.

```javascript
const test_predictions = model.predict(tf.tensor2d(test_x_scaled, [test_x_scaled.length, 1]));
```

## 모델 평가

마지막으로 테스트 세트에서 모델의 성능을 평가할 수 있습니다.

```javascript
const test_loss = tf.losses.meanSquaredError(test_predictions, tf.tensor2d(test_y_scaled, [test_y_scaled.length, 1]));

console.log(test_loss.dataSync());
```

# 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 순환 신경망을 구축하는 방법을 살펴보았습니다. 또한 데이터를 사전 처리하고 모델을 교육하는 방법도 살펴보았습니다.

우리가 구축한 모델은 상당히 단순하지만 더 복잡한 모델로 확장할 수 있습니다. 예를 들어 모델에 더 많은 레이어 또는 단위를 추가하거나 다른 최적화 프로그램을 사용할 수 있습니다.

# 자원

- [TensorFlow.js 문서](https://js.tensorflow.org/)
- [Node.js 문서](https://nodejs.org/en/docs/)
- [반복 신경망](https://en.wikipedia.org/wiki/Recurrent_neural_network)
- [반복 신경망을 이용한 주식 시장 예측](https://t.co/GbU6XfjlbO?amp=1)