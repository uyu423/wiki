---
title: 005: TensorFlow.js 및 Node.js를 사용한 선형 회귀
description: 
published: true
date: 2023-02-02T07:43:33.586Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:43:31.955Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [005: Linear Regression with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/005-linear-regression-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 선형 회귀

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 선형 회귀를 수행하는 방법을 알아봅니다. 선형 회귀를 간략하게 검토한 다음 TensorFlow.js를 사용하여 구현하는 방법을 살펴보겠습니다.

## 선형 회귀란 무엇입니까?

선형 회귀는 종속 변수와 하나 이상의 독립 변수 간의 관계를 모델링하는 데 사용되는 통계 기법입니다. 종속 변수는 예측되는 변수이고 독립 변수는 종속 변수를 예측하는 데 사용되는 변수입니다.

선형 회귀 모델에서 종속 변수는 독립 변수의 선형 함수입니다. 즉, 종속 변수는 독립 변수의 선형 함수입니다.

## TensorFlow.js를 사용하여 선형 회귀를 수행하는 방법은 무엇입니까?

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 숫자 계산에도 사용됩니다. 이 섹션에서는 선형 회귀에 TensorFlow.js를 사용하는 방법을 살펴봅니다.

선형 회귀 예제에 다음 데이터를 사용합니다.

| 엑스 | Y |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 6 |

첫 번째 단계는 TensorFlow.js 라이브러리를 가져오는 것입니다. 다음과 같이 require() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');
```

다음으로 독립 변수와 종속 변수를 정의해야 합니다. tf.tensor() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
// Define the independent variable
const x = tf.tensor([1, 2, 3], [3, 1]);

// Define the dependent variable
const y = tf.tensor([2, 4, 6], [3, 1]);
```

이제 독립 변수와 종속 변수를 정의했으므로 선형 회귀 모델을 정의할 수 있습니다. tf.layers.dense() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
// Define the linear regression model
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

다음 단계는 선형 회귀 모델을 컴파일하는 것입니다. tf.model.compile() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
// Compile the linear regression model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});
```

마지막으로 선형 회귀 모델을 훈련할 수 있습니다. tf.model.fit() 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
// Train the linear regression model
model.fit(x, y, {epochs: 100}).then(() => {
  // Use the model to predict the value of y for x = 4
  model.predict(tf.tensor([4], [1, 1])).print();
});
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 선형 회귀를 수행하는 방법을 살펴보았습니다. 또한 주어진 독립 변수에 대한 종속 변수의 값을 예측하기 위해 선형 회귀 모델을 사용하는 방법도 살펴보았습니다.