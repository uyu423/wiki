---
title: 095: TensorFlow.js 및 Node.js에서 장단기 기억(LSTM) 네트워크 구축
description: 
published: true
date: 2023-02-03T05:17:55.588Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:17:53.920Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [095: Building Long Short-Term Memory (LSTM) Networks in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/095-building-long-short-term-memory-lstm-networks-in-tensorflow-js-and-node-js)
{.links-list}


# 095: TensorFlow.js 및 Node.js에서 LSTM(Long Short-Term Memory) 네트워크 구축

이 게시물에서는 TensorFlow.js 및 Node.js에서 LSTM(Long Short-Term Memory) 네트워크를 구축하는 방법을 살펴보겠습니다.

LSTM은 순차 데이터 작업에 적합한 순환 신경망 유형입니다. 순차 데이터는 시계열 데이터와 같이 각 요소가 이전 요소에 종속되는 데이터입니다.

LSTM은 장기간 정보를 기억할 수 있는 "메모리" 셀을 사용하여 장기 종속성을 학습할 수 있습니다. LSTM은 또한 출력 요소와 동일한 순서가 아닌 입력 요소를 처리할 수 있으며 이는 시계열 데이터 작업에 중요합니다.

## TensorFlow.js에서 LSTM 네트워크 구축

TensorFlow.js에서 LSTM 네트워크를 구축하는 방법부터 살펴보겠습니다.

먼저 TensorFlow.js를 설치해야 합니다. Node.js 패키지 관리자인 npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 `lstm.js`라는 새 파일을 만들고 TensorFlow.js를 가져와야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');
```

이제 LSTM 네트워크 구축을 시작할 준비가 되었습니다.

모델을 정의하는 것으로 시작하겠습니다.

```javascript
const model = tf.sequential();
```

다음으로 모델에 LSTM 계층을 추가합니다. `tf.layers.lstm` 함수의 첫 번째 인수는 LSTM 레이어의 메모리 셀 수인 단위 수입니다. 16개 단위를 사용합니다.

```javascript
model.add(tf.layers.lstm({units: 16, inputShape: [1, 1]}));
```

`inputShape` 인수는 입력 데이터의 모양입니다. 첫 번째 요소는 시간 단계의 수이고 두 번째 요소는 기능의 수입니다. 우리의 경우에는 하나의 시간 단계와 하나의 기능이 있습니다.

다음으로 모델에 조밀한 레이어를 추가합니다. 이것은 단일 값을 출력하는 표준 완전 연결 계층입니다.

```javascript
model.add(tf.layers.dense({units: 1}));
```

이제 모델을 컴파일해야 합니다. 손실 함수와 옵티마이저를 지정해야 합니다. 평균 제곱 오차 손실 함수와 Adam 옵티마이저를 사용합니다.

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

이제 모델을 교육할 준비가 되었습니다. 훈련 데이터를 지정하기 위해 `tf.tensor2d`를 사용할 것입니다. 첫 번째 인수는 데이터이고 두 번째 인수는 데이터의 모양입니다. 우리의 경우 각각 하나의 시간 단계와 하나의 기능이 있는 두 가지 훈련 예제가 있습니다.

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

모델이 교육 데이터를 보는 횟수인 10 epoch 동안 모델을 교육합니다.

```javascript
model.fit(xs, ys, {epochs: 10});
```

모델이 훈련되면 모델을 사용하여 예측할 수 있습니다. 입력 데이터를 지정하기 위해 `tf.tensor2d`를 사용할 것입니다. 우리의 경우에는 하나의 시간 단계와 하나의 기능이 있습니다.

```javascript
const xs = tf.tensor2d([[3]]);
```

그런 다음 `model.predict` 메서드를 호출하여 예측을 수행할 수 있습니다.

```javascript
model.predict(xs).print();
```

그러면 단일 값인 예측이 출력됩니다.

## Node.js에서 LSTM 네트워크 구축

이제 Node.js에서 LSTM 네트워크를 구축하는 방법을 살펴보겠습니다.

먼저 TensorFlow.js를 설치해야 합니다. Node.js 패키지 관리자인 npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 `lstm.js`라는 새 파일을 만들고 TensorFlow.js를 가져와야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');
```

이제 LSTM 네트워크 구축을 시작할 준비가 되었습니다.

모델을 정의하는 것으로 시작하겠습니다.

```javascript
const model = tf.sequential();
```

다음으로 모델에 LSTM 계층을 추가합니다. `tf.layers.lstmLayer` 함수의 첫 번째 인수는 LSTM 레이어의 메모리 셀 수인 단위 수입니다. 16개 단위를 사용합니다.

```javascript
model.add(tf.layers.lstmLayer({units: 16, inputShape: [1, 1]}));
```

`inputShape` 인수는 입력 데이터의 모양입니다. 첫 번째 요소는 시간 단계의 수이고 두 번째 요소는 기능의 수입니다. 우리의 경우에는 하나의 시간 단계와 하나의 기능이 있습니다.

다음으로 모델에 조밀한 레이어를 추가합니다. 이것은 단일 값을 출력하는 표준 완전 연결 계층입니다.

```javascript
model.add(tf.layers.denseLayer({units: 1}));
```

이제 모델을 컴파일해야 합니다. 손실 함수와 옵티마이저를 지정해야 합니다. 평균 제곱 오차 손실 함수와 Adam 옵티마이저를 사용합니다.

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

이제 모델을 교육할 준비가 되었습니다. 훈련 데이터를 지정하기 위해 `tf.tensor2d`를 사용할 것입니다. 첫 번째 인수는 데이터이고 두 번째 인수는 데이터의 모양입니다. 우리의 경우 각각 하나의 시간 단계와 하나의 기능이 있는 두 가지 훈련 예제가 있습니다.

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

모델이 교육 데이터를 보는 횟수인 10 epoch 동안 모델을 교육합니다.

```javascript
model.fit(xs, ys, {epochs: 10});
```

모델이 훈련되면 모델을 사용하여 예측할 수 있습니다. 입력 데이터를 지정하기 위해 `tf.tensor2d`를 사용할 것입니다. 우리의 경우에는 하나의 시간 단계와 하나의 기능이 있습니다.

```javascript
const xs = tf.tensor2d([[3]]);
```

그런 다음 `model.predict` 메서드를 호출하여 예측을 수행할 수 있습니다.

```javascript
model.predict(xs).print();
```

그러면 단일 값인 예측이 출력됩니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 LSTM(Long Short-Term Memory) 네트워크를 구축하는 방법을 살펴보았습니다. LSTM은 순차 데이터 작업에 적합한 순환 신경망 유형입니다.

LSTM에 대해 자세히 알아보고 싶다면 다음 리소스를 추천합니다.

- [순환 신경망의 비합리적인 효율성](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)
- [LSTM 네트워크 이해하기](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [장단기 기억](https://en.wikipedia.org/wiki/Long_short-term_memory)