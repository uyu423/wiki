---
title: 006: TensorFlow.js 및 Node.js를 사용한 로지스틱 회귀
description: 
published: true
date: 2023-02-02T08:04:27.329Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:04:25.790Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [006: Logistic Regression with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/006-logistic-regression-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 로지스틱 회귀

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 로지스틱 회귀 모델을 빌드하는 방법을 알아봅니다.

로지스틱 회귀는 이진 결과를 예측하기 위한 통계적 방법입니다. 즉, 이벤트가 발생할지 여부를 예측하는 데 사용할 수 있습니다. 예를 들어 로지스틱 회귀를 사용하여 특정 특성을 기반으로 환자가 질병에 걸릴지 여부를 예측할 수 있습니다.

로지스틱 회귀는 일종의 선형 회귀이지만 몇 가지 중요한 차이점이 있습니다. 첫째, 결과 변수는 이진법입니다. 즉, 두 값(0 또는 1)만 사용할 수 있습니다. 둘째, 모델은 최소 제곱이 아닌 최대 우도 추정을 사용하여 적합합니다.

## 시작하기

시작하려면 TensorFlow.js 및 Node.js를 설치해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
npm install -g tensorflow
npm install -g node
```

TensorFlow.js와 Node.js가 설치되면 `logistic-regression.js`라는 새 파일을 만들고 코딩을 시작할 수 있습니다.

## 데이터

첫 번째 단계는 데이터를 로드하는 것입니다. `tensorflow.js` 라이브러리를 사용하여 `tf.tensor` 개체에 데이터를 로드합니다.

```javascript
const tf = require('tensorflow');

// Load the data
const data = tf.tensor([
  [1, 2],
  [2, 3],
  [3, 4],
  [4, 5],
]);
```

## 모델

다음으로 모델을 정의해야 합니다. 두 개의 입력 기능(`x1` 및 `x2`)과 하나의 출력(`y`)이 있는 로지스틱 회귀 모델을 사용합니다.

```javascript
// Define the model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [2] }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'sgd' });
```

## 훈련

이제 데이터와 모델이 있으므로 모델을 교육할 수 있습니다. 우리는 `fit` 방법을 사용하여 데이터에 대해 모델을 훈련할 것입니다.

```javascript
// Train the model
model.fit(data, tf.tensor([1, 1, 0, 0]), {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    },
  },
});
```

## 예측

모델이 학습되면 모델을 사용하여 예측할 수 있습니다. `predict` 메서드를 사용하여 새 데이터의 출력을 예측합니다.

```javascript
// Make predictions
model.predict(tf.tensor([[5, 6]])).print(); // [[0.5]]
model.predict(tf.tensor([[6, 7]])).print(); // [[0.5]]
```

보시다시피 모델은 두 입력 모두에 대해 출력을 0.5로 예측합니다. 이는 우리 모델이 이벤트 발생 확률을 50%로 예측하고 있음을 의미합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 로지스틱 회귀 모델을 빌드하는 방법을 배웠습니다. 또한 모델을 사용하여 새 데이터에 대한 예측을 수행하는 방법도 살펴보았습니다.