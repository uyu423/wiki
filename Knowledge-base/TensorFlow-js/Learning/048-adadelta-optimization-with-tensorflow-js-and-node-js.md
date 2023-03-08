---
title: 048: TensorFlow.js 및 Node.js를 사용한 Adadelta 최적화
description: 
published: true
date: 2023-02-02T18:17:52.336Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:17:47.722Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [048: Adadelta Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/048-adadelta-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 Adadelta 최적화

Adadelta는 심층 신경망을 훈련하기 위해 기존의 확률적 경사 하강법(SGD) 대신 사용할 수 있는 최적화 알고리즘입니다. 이는 신경망을 훈련하는 보다 강력하고 효율적인 방법이며 TensorFlow.js 및 Node.js와 함께 사용할 수 있습니다.

## 아다델타란?

Adadelta는 심층 신경망 훈련에 적합한 적응형 학습률 최적화 알고리즘입니다. 2012년 Matthew D. Zeiler와 Rob Fergus가 "[ADADELTA: An Adaptive Learning Rate Method](https://arxiv.org/abs/1212.5701)" 논문에서 제안하여 International에서 Best Paper Award를 수상했습니다. 2013년 학습 표현 회의(ICLR).

Adadelta는 Duchi 등이 2011년에 제안한 또 다른 적응형 학습 속도 최적화 알고리즘인 Adagrad의 확장입니다. "[온라인 학습 및 확률적 최적화를 위한 적응형 하위 그라데이션 방법](https://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)" 논문에서.

Adagrad와 Adadelta는 모두 매개변수에 대한 손실 함수의 기울기에 따라 조정되는 매개변수당 학습률의 개념을 기반으로 합니다.

## Adadelta는 어떻게 작동합니까?

Adadelta 최적화 알고리즘은 신경망의 각 매개변수에 대한 매개변수별 학습률을 계산하여 작동합니다. 학습률은 매개변수에 대한 손실 함수의 기울기에 따라 조정됩니다.

알고리즘에는 두 개의 매개변수가 있습니다.

- `rho`: 학습률의 감소율을 제어하는 매개변수입니다. 일반적으로 '0.95' 값이 사용됩니다.
- `epsilon`: 수치적 안정성을 위해 사용되는 작은 매개변수입니다. 일반적으로 '1e-6' 값이 사용됩니다.

Adadelta 최적화 알고리즘은 다음과 같이 요약할 수 있습니다.

1. 파라미터별 학습률 'Delta_p'를 '0'으로 초기화합니다.
2. 각 훈련 예시 `x` 및 해당 대상 `y`에 대해:
    1. 파라미터 `Delta_p = gradient(loss(x, y), p)`에 대한 손실 함수의 기울기를 계산합니다.
    2. 파라미터별 학습률 업데이트: `Delta_p = rho * Delta_p + (1 - rho) * Delta_p^2`.
    3. 매개변수 업데이트: `p = p - learning_rate * Delta_p / sqrt(epsilon + stacked_gradients)`.

## 아다델타 대 SGD

Adadelta는 기존의 확률적 경사하강법(SGD)보다 신경망을 훈련하는 더 강력하고 효율적인 방법입니다.

SGD는 신경망 훈련에 널리 사용되는 최적화 알고리즘이지만 학습 속도를 조정하기 어려울 수 있습니다. 학습률이 너무 낮으면 학습 과정이 느려집니다. 학습률이 너무 높으면 학습 과정이 분기될 수 있습니다.

Adadelta는 학습률을 지정할 필요가 없습니다. 학습률은 손실 함수의 기울기에 따라 자동으로 조정됩니다. 따라서 SGD보다 강력하고 효율적입니다.

## TensorFlow.js 및 Node.js를 사용하는 Adadelta

Adadelta는 TensorFlow.js 및 Node.js와 함께 사용할 수 있습니다.

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. Node.js는 TensorFlow.js 애플리케이션을 실행하는 데 사용할 수 있는 JavaScript 런타임입니다.

TensorFlow.js 및 Node.js와 함께 Adadelta를 사용하려면 `tensorflow` 및 `@tensorflow/tfjs-node` 모듈을 설치해야 합니다.

```
$ npm install --save tensorflow
$ npm install --save @tensorflow/tfjs-node
```

그런 다음 `tf.train.adadelta` 함수를 사용하여 Adadelta 최적화 알고리즘을 사용하여 신경망을 훈련할 수 있습니다.

```javascript
const tf = require('tensorflow');

// Define the neural network.
const model = tf.sequential();
model.add(tf.layers.dense({ units: 10, inputShape: [5], activation: 'relu' }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model.
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: tf.train.adadelta(),
  metrics: ['accuracy']
});

// Train the model.
model.fit({ x: tf.ones([100, 5]), y: tf.zeros([100]) }, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js와 함께 Adadelta 최적화 알고리즘을 사용하는 방법을 살펴보았습니다. Adadelta는 기존의 확률적 경사하강법(SGD)보다 신경망을 훈련하는 더 강력하고 효율적인 방법입니다.