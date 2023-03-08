---
title: 047: TensorFlow.js 및 Node.js를 사용한 Adagrad 최적화
description: 
published: true
date: 2023-02-02T18:04:38.948Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:04:37.335Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [047: Adagrad Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/047-adagrad-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 Adagrad 최적화

TensorFlow.js는 자바스크립트에서 기계 학습을 수행할 수 있게 해주는 강력한 도구입니다. 이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 Adagrad 최적화 알고리즘을 사용하여 기계 학습 모델을 최적화하는 방법을 보여줍니다.

## 아다그라드란?

Adagrad는 심층 신경망 훈련에 적합한 최적화 알고리즘입니다. 학습률을 모델의 개별 매개변수에 맞게 조정하는 그래디언트 기반 알고리즘입니다. 이는 매개변수 기울기의 제곱합의 제곱근에 반비례하는 요인으로 학습률을 조정하여 수행됩니다.

## TensorFlow.js와 함께 Adagrad를 사용하는 방법

TensorFlow.js와 함께 Adagrad를 사용하려면 TensorFlow.js Node.js 라이브러리를 설치해야 합니다. 다음 명령으로 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

라이브러리가 설치되면 새 파일을 만들고 다음 코드를 사용하여 라이브러리를 요구할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
```

다음으로 간단한 선형 회귀 모델을 만듭니다. `tf.sequential` 함수를 사용하여 모델을 생성하고 `tf.layers.dense` 함수를 사용하여 dense layer를 생성합니다. 밀집 계층은 모든 노드가 이전 계층의 다른 모든 노드에 연결된 계층입니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

모델이 생성되면 컴파일해야 합니다. 이것은 `tf.model.compile` 함수로 수행됩니다. 손실 함수와 옵티마이저를 지정해야 합니다. 손실 함수의 경우 `tf.losses.meanSquaredError`를 사용합니다. 이 손실 함수는 회귀 문제에 사용됩니다. 옵티마이저는 `tf.train.adagrad`를 사용합니다.

```javascript
model.compile({
  loss: tf.losses.meanSquaredError,
  optimizer: tf.train.adagrad(0.1),
});
```

`tf.train.adagrad` 함수는 학습률을 인수로 사용합니다. Adagrad 알고리즘에서 사용할 학습 속도입니다.

## 모델 훈련 방법

이제 모델을 컴파일했으므로 학습할 수 있습니다. 우리는 `tf.model.fit` 함수를 사용하여 모델을 훈련할 것입니다. 학습 데이터, Epoch 수 및 배치 크기를 지정해야 합니다.

```javascript
const xs = tf.tensor1d([1, 2, 3, 4]);
const ys = tf.tensor1d([1, 3, 5, 7]);

model.fit(xs, ys, {
  epochs: 10,
  batchSize: 4,
});
```

학습 데이터는 입력 값과 출력 값을 포함하는 TensorFlow.js 텐서입니다. 입력 값은 x 값이고 출력 값은 y 값입니다. 배치 크기는 각 교육 반복에서 사용되는 교육 예제의 수입니다. Epoch 수는 훈련 알고리즘이 훈련 데이터를 통과하는 횟수입니다.

## 훈련된 모델을 사용하는 방법

모델이 학습된 후 모델을 사용하여 예측할 수 있습니다. 우리는 `tf.model.predict` 함수를 사용하여 예측을 할 것입니다. 입력 데이터를 지정해야 합니다.

```javascript
const xs = tf.tensor1d([5, 6, 7, 8]);
const ys = model.predict(xs);
```

입력 데이터는 입력 값을 포함하는 TensorFlow.js 텐서입니다. `tf.model.predict` 함수의 출력은 예측을 포함하는 TensorFlow.js 텐서입니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 Adagrad 최적화 알고리즘을 사용하여 기계 학습 모델을 최적화하는 방법을 보여주었습니다.