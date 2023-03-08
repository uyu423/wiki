---
title: 045: TensorFlow.js 및 Node.js를 사용한 Stochastic Gradient Descent(SGD)
description: 
published: true
date: 2023-02-02T17:36:46.296Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:36:41.300Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [045: Stochastic Gradient Descent (SGD) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/045-stochastic-gradient-descent-sgd-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 Stochastic Gradient Descent(SGD)

SGD(Stochastic Gradient Descent)는 딥 러닝 모델 훈련에 널리 사용되는 최적화 방법입니다. SGD는 비용 함수를 최소화하는 방향으로 모델의 가중치를 반복적으로 업데이트하여 작동합니다.

TensorFlow.js는 브라우저 또는 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 이 자습서에서는 TensorFlow.js 및 SGD를 사용하여 간단한 선형 회귀 모델을 교육하는 방법을 보여줍니다.

## 시작하기

먼저 TensorFlow.js와 해당 종속 항목을 설치해 보겠습니다. 이를 위해서는 Node.js와 npm이 설치되어 있어야 합니다.

    $ npm 설치 @tensorflow/tfjs @tensorflow/tfjs-노드

다음으로 코드용 파일을 만들어야 합니다. 우리는 그것을 `sgd.js`라고 부를 것입니다.

## 자료

이 자습서에서는 매우 간단한 데이터 세트를 사용합니다. `x`와 `y`의 두 열로 구성됩니다. `x`는 1에서 100까지의 숫자 목록이고 `y`는 해당 숫자의 제곱 목록입니다.

TensorFlow.js를 사용하여 이 데이터 세트를 쉽게 생성할 수 있습니다.

```javascript
const xs = tf.range(1, 100, 1);
const ys = xs.square();
```

## 모델

우리 모델은 매우 간단한 선형 회귀 모델이 될 것입니다. 선형 회귀 모델은 가격이나 수량과 같은 연속 값을 예측하는 데 사용됩니다.

우리 모델은 단 하나의 가중치와 하나의 편향을 가집니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

## 비용 함수

비용 함수는 모델이 얼마나 잘 작동하는지 측정한 것입니다. 우리는 비용 함수를 최소화하려고 합니다. 즉, 모델의 예측을 실제 값에 최대한 가깝게 만드는 가중치 및 편향 집합을 찾고자 합니다.

선형 회귀에 사용할 수 있는 다양한 비용 함수가 있습니다. 이 자습서에서는 평균 제곱 오차 비용 함수를 사용합니다.

```javascript
function meanSquaredError(labels, predictions) {
  const error = labels.sub(predictions).square().mean();
  return error;
}
```

## 옵티마이저

옵티마이저는 모델의 가중치와 편향을 업데이트하는 데 사용하는 알고리즘입니다. SGD는 옵티마이저를 위한 인기 있는 선택이지만 선택할 수 있는 다른 많은 옵션이 있습니다.

이 자습서에서는 학습률이 0.1인 SGD 옵티마이저를 사용합니다.

```javascript
const optimizer = tf.train.sgd(0.1);
```

## 모델 교육

이제 데이터, 모델, 비용 함수 및 옵티마이저가 있으므로 모델을 교육할 준비가 되었습니다.

TensorFlow.js에서 모델을 교육하는 것은 쉽습니다. 모델에서 'fit' 메서드를 호출하여 데이터와 훈련할 에포크(반복) 수를 전달하기만 하면 됩니다.

```javascript
model.fit(xs, ys, {
  epochs: 100,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

## 모델 평가

모델이 훈련되면 새로운 데이터로 모델을 평가할 수 있습니다. 이 자습서에서는 1에서 10까지의 `x` 값과 1에서 100까지의 `y` 값을 사용하여 새 데이터 세트를 생성합니다.

```javascript
const xs = tf.range(1, 10, 1);
const ys = tf.range(1, 100, 1);
```

`predict` 메서드를 사용하여 이 새로운 데이터에 대한 예측을 할 수 있습니다.

```javascript
const predictions = model.predict(xs);
```

마지막으로 예측을 실제 값과 비교하여 모델이 얼마나 잘 수행되었는지 확인할 수 있습니다.

```javascript
predictions.print();
ys.print();
```

## 추가 정보

- [TensorFlow.js 문서](https://js.tensorflow.org/)
- [선형 회귀 튜토리얼](https://machinelearningmastery.com/linear-regression-tutorial-machine-learning/)
- [SGD 최적화 문서](https://www.tensorflow.org/api_docs/python/tf/train/GradientDescentOptimizer)