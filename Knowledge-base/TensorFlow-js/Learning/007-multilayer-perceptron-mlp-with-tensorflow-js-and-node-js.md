---
title: 007: TensorFlow.js 및 Node.js를 사용한 다층 퍼셉트론(MLP)
description: 
published: true
date: 2023-02-02T08:17:32.607Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:17:30.974Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [007: Multilayer Perceptron (MLP) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/007-multilayer-perceptron-mlp-with-tensorflow-js-and-node-js)
{.links-list}


## 소개

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 다층 퍼셉트론(MLP)을 구축하는 방법을 다룰 것입니다. 신경망과 딥 러닝의 기본 개념과 TensorFlow.js를 사용하여 이를 구현하는 방법을 살펴보겠습니다. 이 게시물을 마치면 자신만의 신경망을 구축하고 이를 사용하여 실제 문제를 해결할 수 있습니다.

## 다층 퍼셉트론이란?

다층 퍼셉트론(MLP)은 신경망의 한 유형입니다. 신경망은 데이터의 복잡한 패턴을 모델링하는 데 사용되는 일종의 기계 학습 알고리즘입니다. MLP는 여러 계층의 뉴런으로 구성된 특정 유형의 신경망입니다.

MLP의 첫 번째 계층은 입력 데이터를 받는 입력 계층입니다. 두 번째 계층은 입력 데이터를 새로운 표현으로 변환하는 숨겨진 계층입니다. 숨겨진 레이어 다음에는 MLP의 출력을 생성하는 출력 레이어가 옵니다.

## TensorFlow.js로 MLP 구축

TensorFlow.js는 신경망 및 기계 학습 모델을 구축하기 위한 JavaScript 라이브러리입니다. 브라우저와 Node.js 모두에서 사용할 수 있습니다.

TensorFlow.js를 사용하려면 먼저 TensorFlow.js를 설치해야 합니다. NPM(노드 패키지 관리자)을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

TensorFlow.js가 설치되면 프로젝트로 가져올 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');
```

이제 TensorFlow.js를 설치하고 가져왔으므로 MLP 구축을 시작할 수 있습니다.

첫 번째 단계는 입력 레이어를 정의하는 것입니다. `input` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const inputLayer = tf.input({shape: [2]});
```

`input` 함수는 객체를 인수로 받습니다. 이 개체의 '모양' 속성은 입력 데이터의 모양을 정의합니다. 이 경우에는 2차원 입력을 사용하므로 `shape` 속성이 `[2]`로 설정됩니다.

다음으로 히든 레이어를 정의해야 합니다. `layers` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const hiddenLayer = tf.layers.dense({
  units: 4,
  activation: 'sigmoid',
  inputShape: [2]
});
```

`layers` 함수는 개체를 인수로 사용합니다. `units` 속성은 레이어의 뉴런 수를 정의합니다. 'activation' 속성은 레이어의 활성화 기능을 정의합니다. 이 경우 시그모이드 활성화 기능을 사용하고 있습니다. 'inputShape' 속성은 입력 데이터의 모양을 정의합니다.

마지막으로 출력 레이어를 정의해야 합니다. `layers` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const outputLayer = tf.layers.dense({
  units: 1,
  activation: 'sigmoid',
  inputShape: [4]
});
```

숨겨진 레이어와 마찬가지로 `units` 속성은 레이어의 뉴런 수를 정의합니다. 'activation' 속성은 레이어의 활성화 기능을 정의합니다. 이 경우 다시 시그모이드 활성화 함수를 사용합니다. 'inputShape' 속성은 입력 데이터의 모양을 정의합니다.

이제 MLP의 레이어를 정의했으므로 연결해야 합니다. `sequential` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const model = tf.sequential();
```

'sequential' 함수는 레이어 배열을 인수로 사용합니다. 이 경우 입력 레이어, 숨겨진 레이어 및 출력 레이어를 전달합니다.

이제 모델이 정의되었으므로 모델을 컴파일해야 합니다. `compile` 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
model.compile({
  optimizer: 'sgd',
  loss: 'meanSquaredError'
});
```

`compile` 함수는 객체를 인수로 받습니다. `옵티마이저` 속성은 모델 학습에 사용될 옵티마이저를 정의합니다. 이 경우 확률적 경사하강법(SGD) 옵티마이저를 사용하고 있습니다. 'loss' 속성은 모델을 평가하는 데 사용할 손실 함수를 정의합니다. 이 경우 평균 제곱 오차(MSE) 손실 함수를 사용하고 있습니다.

이제 모델이 컴파일되었으므로 학습할 수 있습니다. 우리는 `fit` 함수를 사용하여 이것을 할 수 있습니다:

```javascript
model.fit(x, y, {
  epochs: 100,
  batchSize: 32
});
```

'fit' 함수는 훈련 데이터(`x`), 대상 데이터(`y`) 및 훈련 매개변수를 지정하는 개체의 세 가지 인수를 사용합니다. 'epochs' 속성은 훈련 epoch의 수를 정의합니다. `batchSize` 속성은 각 학습 배치의 샘플 수를 정의합니다.

모델이 훈련되면 모델을 사용하여 예측할 수 있습니다. `predict` 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
model.predict(x).print();
```

`predict` 함수는 입력 데이터 배열(`x`)을 사용하여 예측 배열을 반환합니다. `print` 함수는 예측을 콘솔에 인쇄합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 다층 퍼셉트론(MLP)을 빌드하는 방법을 다루었습니다. 신경망과 딥 러닝의 기본 개념과 TensorFlow.js를 사용하여 이를 구현하는 방법을 살펴보았습니다. 이 게시물을 마치면 자신만의 신경망을 구축하고 실제 문제를 해결하는 데 사용할 수 있을 것입니다.