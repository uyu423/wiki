---
title: 044: TensorFlow.js 및 Node.js를 사용한 경사 하강법
description: 
published: true
date: 2023-02-02T17:18:33.766Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:18:32.059Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [044: Gradient Descent with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/044-gradient-descent-with-tensorflow-js-and-node-js)
{.links-list}


# 044: TensorFlow.js 및 Node.js를 사용한 경사 하강법

경사하강법은 비용 함수를 최소화하는 매개변수 값(예: 가중치 및 편향)을 찾는 데 사용되는 최적화 알고리즘입니다. 신경망 훈련에 널리 사용되는 알고리즘입니다.

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. Node.js는 서버에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

이 자습서에서는 TensorFlow.js 및 Node.js를 사용하여 선형 회귀를 수행하도록 간단한 신경망을 훈련합니다. 네트워크의 가중치와 편향에 대한 최적의 값을 찾기 위해 경사 하강법을 사용할 것입니다.

## 선형 회귀란 무엇입니까?

선형 회귀는 연속 값을 예측하는 데 사용되는 기계 학습 알고리즘입니다. 예를 들어 선형 회귀를 사용하여 크기, 침실 수 및 욕실 수를 기반으로 주택 가격을 예측할 수 있습니다.

선형 회귀는 지도 학습의 한 유형이므로 알고리즘에 교육 데이터를 제공해야 합니다. 학습 데이터는 입력 값(x)과 해당 출력 값(y)의 집합으로 구성됩니다. 주택 가격 예의 경우 입력 값은 크기, 침실 수, 욕실 수일 수 있고 출력 값은 가격이 될 수 있습니다.

## 선형 회귀는 어떻게 작동합니까?

선형 회귀는 예측 값(ŷ)과 실제 값(y) 사이의 오차를 최소화하는 일련의 가중치(w)와 편향(b)을 찾는 방식으로 작동합니다.

![선형 회귀](https://cdn-images-1.medium.com/max/1600/1*d7Cg5UC5tM7GtLjTvW0MzA.png)

예측값은 입력값(x)에 가중치(w)를 곱한 다음 편향(b)을 더하여 계산합니다.

![예측값](https://cdn-images-1.medium.com/max/1600/1*j_q-F1lrVxKbV-_d7JKV2w.png)

오류는 예측 값(ŷ)과 실제 값(y)의 차이를 취하여 계산됩니다.

![오류](https://cdn-images-1.medium.com/max/1600/1*7VtEOzAj_sXXuTzXrT7yYQ.png)

그런 다음 기울기 하강법을 사용하여 오류를 최소화하는 가중치와 편향을 찾을 수 있습니다.

## 경사하강법이란?

경사하강법은 비용 함수를 최소화하는 매개변수 값(예: 가중치 및 편향)을 찾는 데 사용되는 최적화 알고리즘입니다.

![비용 함수](https://cdn-images-1.medium.com/max/1600/1*Xu7B5y9gp0iL5ooBj7LtWw.png)

비용 함수는 예측 값(ŷ)이 실제 값(y)에서 얼마나 떨어져 있는지를 측정한 것입니다. 우리는 비용 함수를 최소화하는 가중치와 편향을 찾고자 합니다.

![가중치 및 바이어스](https://cdn-images-1.medium.com/max/1600/1*n6sVxWAz7VUgX6Sj7K1vUw.png)

경사 하강법은 비용 함수를 최소화하는 방향으로 가중치와 편향을 반복적으로 업데이트하여 작동합니다. 업데이트 크기는 학습률에 따라 결정됩니다.

![경사하강법](https://cdn-images-1.medium.com/max/1600/1*jw7UwKLnA0sCgq_QPV-_lA.png)

## TensorFlow.js에서 경사 하강법 구현

이제 경사 하강법이 작동하는 방식을 살펴보았으므로 TensorFlow.js에서 이를 구현하는 방법을 살펴보겠습니다.

먼저 입력 값(x), 출력 값(y), 가중치(w) 및 바이어스(b)의 초기 값을 정의해야 합니다.

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

다음으로 비용 함수를 정의해야 합니다. 평균 제곱 오차 비용 함수를 사용합니다.

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

이제 경사하강법 알고리즘을 정의할 수 있습니다. 비용 함수를 최소화하는 방향으로 가중치와 편향을 반복적으로 업데이트합니다.

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

마지막으로 'train' 함수를 호출하여 모델을 훈련할 수 있습니다. 우리는 학습률 0.1로 100 epoch 동안 모델을 훈련할 것입니다.

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## 모델 교육

이제 TensorFlow.js에서 경사 하강법을 구현하는 방법을 살펴보았으므로 이를 사용하여 선형 회귀를 수행하도록 신경망을 훈련시키는 방법을 살펴보겠습니다.

먼저 입력 값(x), 출력 값(y), 가중치(w) 및 바이어스(b)의 초기 값을 정의해야 합니다.

```javascript
// Define the input values
const x = tf.tensor([
  [1, 2, 3, 4],
  [2, 3, 4, 5],
  [3, 4, 5, 6],
  [4, 5, 6, 7]
]);

// Define the output values
const y = tf.tensor([
  [2],
  [4],
  [6],
  [8]
]);

// Define the initial values for the weights and biases
const w = tf.variable(tf.zeros([4, 1]));
const b = tf.variable(tf.zeros([1]));
```

다음으로 비용 함수를 정의해야 합니다. 평균 제곱 오차 비용 함수를 사용합니다.

```javascript
// Define the cost function
function cost(pred, labels) {
  const diff = pred.sub(labels);
  const sqrDiff = diff.square();
  const meanSqrDiff = sqrDiff.mean();
  return meanSqrDiff;
}
```

이제 경사하강법 알고리즘을 정의할 수 있습니다. 비용 함수를 최소화하는 방향으로 가중치와 편향을 반복적으로 업데이트합니다.

```javascript
// Define the gradient descent algorithm
async function train(x, y, w, b, epochs, learningRate) {
  for (let i = 0; i < epochs; i++) {
    // Calculate the predicted values
    const pred = x.matMul(w).add(b);

    // Calculate the cost
    const c = cost(pred, y);

    // Print the cost
    console.log("Epoch: " + i + " Cost: " + c.dataSync()[0]);

    // Calculate the gradients
    const grads = tf.grads(c, [w, b]);
    const dw = grads[0];
    const db = grads[1];

    // Update the weights and biases
    w.sub(dw.mul(learningRate));
    b.sub(db.mul(learningRate));
  }
}
```

마지막으로 'train' 함수를 호출하여 모델을 훈련할 수 있습니다. 우리는 학습률 0.1로 100 epoch 동안 모델을 훈련할 것입니다.

```javascript
// Train the model
train(x, y, w, b, 100, 0.1);
```

## 모델 테스트

이제 모델을 학습했으므로 일부 테스트 데이터에서 모델이 어떻게 작동하는지 살펴보겠습니다.

먼저 테스트 데이터를 정의해야 합니다.

```javascript
// Define the test data
const xTest = tf.tensor([
  [5, 6, 7, 8],
  [6, 7, 8, 9],
  [7, 8, 9, 10],
  [8, 9, 10, 11]
]);

// Define the expected output values
const yTest = tf.tensor([
  [10],
  [12],
  [14],
  [16]
]);
```

다음으로 예측 값을 계산해야 합니다.

```javascript
// Calculate the predicted values
const pred = xTest.matMul(w).add(b);
```

마지막으로 예측 값을 예상 출력 값과 비교할 수 있습니다.

```javascript
// Compare the predicted values to the expected output values
pred.print();
yTest.print();
```

## 결론

이 자습서에서는 경사 하강법을 사용하여 선형 회귀를 수행하도록 신경망을 훈련시키는 방법을 살펴보았습니다. 또한 TensorFlow.js에서 경사 하강법을 구현하는 방법과 이를 사용하여 신경망을 훈련시키는 방법도 살펴보았습니다.