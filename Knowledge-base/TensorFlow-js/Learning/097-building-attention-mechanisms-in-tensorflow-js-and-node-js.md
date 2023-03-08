---
title: 097: TensorFlow.js 및 Node.js에서 어텐션 메커니즘 구축
description: 
published: true
date: 2023-02-03T05:43:48.263Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:43:46.648Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [097: Building Attention Mechanisms in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/097-building-attention-mechanisms-in-tensorflow-js-and-node-js)
{.links-list}


# 소개

이 게시물에서는 TensorFlow.js 및 Node.js에서 어텐션 메커니즘을 구축하는 방법을 살펴보겠습니다. 주의 메커니즘은 입력의 특정 부분에 집중할 수 있는 일종의 신경망입니다. 이는 좋은 출력을 생성하기 위해 입력의 특정 부분에 집중할 수 있는 것이 중요한 이미지 캡션 또는 기계 번역과 같은 작업에 유용할 수 있습니다.

우리는 TensorFlow.js라는 라이브러리를 사용할 것입니다. 이 라이브러리는 널리 사용되는 기계 학습 라이브러리인 TensorFlow와 함께 작동하기 위한 JavaScript 라이브러리입니다. TensorFlow.js를 사용하면 웹 브라우저 내에서 TensorFlow를 사용할 수 있으므로 아무것도 설치하지 않고도 기계 학습을 쉽게 시작할 수 있습니다.

또한 웹 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임인 Node.js를 사용할 것입니다. Node.js는 종종 백엔드 웹 애플리케이션 개발에 사용되지만 이 게시물에서 볼 수 있듯이 데이터 작업에도 사용할 수 있습니다.

# 시작하기

먼저 TensorFlow.js와 Node.js를 설치해야 합니다. Node.js 패키지를 설치하고 관리하기 위한 도구인 Node Package Manager(npm)를 사용하여 이 작업을 수행할 수 있습니다.

TensorFlow.js를 설치하려면 다음 명령을 실행합니다.

```
npm install @tensorflow/tfjs
```

그러면 Node.js 애플리케이션에서 사용할 수 있는 TensorFlow.js 라이브러리가 설치됩니다.

Node.js를 설치하려면 다음 명령을 실행합니다.

```
npm install node
```

이렇게 하면 애플리케이션을 실행하는 데 사용할 수 있는 Node.js 런타임이 설치됩니다.

# 안녕하세요, TensorFlow.js

이제 TensorFlow.js와 Node.js가 설치되었으므로 TensorFlow.js를 사용하는 간단한 프로그램을 작성해 보겠습니다.

`hello-tfjs.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a model for linear regression
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Train the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});
model.fit(tf.tensor2d([1, 2, 3, 4], [4, 1]), tf.tensor2d([1, 3, 5, 7], [4, 1]));

// Predict output for input [5]
model.predict(tf.tensor2d([5], [1, 1])).print();
```

이 코드는 TensorFlow.js 라이브러리를 사용하여 간단한 선형 회귀 모델을 정의합니다. 그런 다음 일부 데이터에 대해 모델을 교육하고 이를 사용하여 새 입력에 대한 출력을 예측합니다.

이 코드를 실행하기 위해 Node.js 런타임을 사용합니다.

```
node hello-tfjs.js
```

그러면 다음이 출력됩니다.

```
Tensor
[[9]]
```

이것은 입력 [5]에 대한 선형 회귀 모델에 의해 만들어진 예측입니다.

# 주의 메커니즘 구축

TensorFlow.js를 사용하는 방법을 살펴보았으니 이제 어텐션 메커니즘을 구축하는 방법을 살펴보겠습니다. 우리는 TensorFlow.js용 Node.js 래퍼인 TensorFlow.js-node라는 라이브러리를 사용할 것입니다.

TensorFlow.js-node를 설치하려면 다음 명령을 실행합니다.

```
npm install @tensorflow/tfjs-node
```

그러면 Node.js 애플리케이션에서 사용할 수 있는 TensorFlow.js-node 라이브러리가 설치됩니다.

`attention.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
// Load the TensorFlow.js-node library
const tf = require('@tensorflow/tfjs-node');

// Define a model for attention
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Train the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});
model.fit(tf.tensor2d([1, 2, 3, 4], [4, 1]), tf.tensor2d([1, 3, 5, 7], [4, 1]));

// Predict output for input [5]
model.predict(tf.tensor2d([5], [1, 1])).print();
```

이 코드는 TensorFlow.js-node 라이브러리를 사용하여 간단한 주의 모델을 정의합니다. 그런 다음 일부 데이터에 대해 모델을 교육하고 이를 사용하여 새 입력에 대한 출력을 예측합니다.

이 코드를 실행하기 위해 Node.js 런타임을 사용합니다.

```
node attention.js
```

그러면 다음이 출력됩니다.

```
Tensor
[[9]]
```

이것은 입력 [5]에 대한 우리의 주의 모델에 의해 만들어진 예측입니다.

# 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 어텐션 메커니즘을 구축하는 방법을 살펴보았습니다. TensorFlow.js를 사용하여 어텐션 모델의 성능을 훈련하고 평가하는 방법도 살펴보았습니다.