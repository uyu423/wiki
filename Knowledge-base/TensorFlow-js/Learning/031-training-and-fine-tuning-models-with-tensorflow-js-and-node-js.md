---
title: 031: TensorFlow.js 및 Node.js로 모델 훈련 및 미세 조정
description: 
published: true
date: 2023-02-02T14:17:56.928Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:17:55.368Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [031: Training and Fine-Tuning Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/031-training-and-fine-tuning-models-with-tensorflow-js-and-node-js)
{.links-list}


# 031: TensorFlow.js 및 Node.js로 모델 훈련 및 미세 조정

TensorFlow.js는 브라우저에서 기계 학습 모델을 생성하고 교육할 수 있는 수치 계산을 위한 오픈 소스 라이브러리입니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다. 이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 기계 학습 모델을 훈련하고 미세 조정하는 방법을 보여줍니다.

## TensorFlow.js 설치

TensorFlow.js를 설치하려면 Node.js 및 npm(Node.js 패키지 관리자)이 설치되어 있어야 합니다. 터미널에서 다음 명령을 실행하여 Node.js가 설치되어 있는지 확인할 수 있습니다.

```
node -v
```

Node.js가 설치되어 있지 않으면 [여기](https://nodejs.org/en/)에서 다운로드할 수 있습니다.

Node.js와 npm이 설치되면 다음 명령을 사용하여 TensorFlow.js를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

## 모델 교육

이제 TensorFlow.js가 설치되었으므로 자체 기계 학습 모델 학습을 시작할 수 있습니다. 이 섹션에서는 간단한 선형 회귀 모델을 교육하는 방법을 보여줍니다.

먼저 훈련 데이터를 만들어 봅시다. 내장된 tf.tensor2d() 함수를 사용하여 10개의 행과 1개의 열이 있는 2D 텐서(배열의 배열)를 생성합니다. 평균이 0이고 표준 편차가 1인 정규 분포의 난수로 텐서를 채울 것입니다.

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4], [6, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7], [6, 1]);
```

다음으로 모델을 정의합니다. tf.sequential() 함수를 사용하여 레이어의 선형 스택인 순차 모델을 만듭니다. 그런 다음 tf.layers.dense() 함수를 사용하여 밀도가 높은 레이어를 모델에 추가합니다. Dense 레이어는 완전 연결 레이어로, 이전 레이어의 모든 노드가 dense 레이어의 모든 노드에 연결되어 있음을 의미합니다. 고밀도 레이어에 1개의 출력 노드가 있고 입력 모양이 [1]이라고 지정합니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

이제 모델을 정의했으므로 컴파일해야 합니다. 모델을 컴파일하면 교육용 모델이 구성됩니다. tf.train.sgd() 함수를 사용하여 확률적 경사 하강 최적화 프로그램을 만듭니다. 옵티마이저는 학습 중에 손실 함수를 최소화하는 데 사용됩니다. 또한 평균 제곱 오차에 대해 최적화하도록 지정할 것입니다.

```javascript
model.compile({optimizer: tf.train.sgd(0.1), loss: 'meanSquaredError'});
```

이제 모델이 컴파일되었으므로 학습을 시작할 수 있습니다. model.fit() 함수를 사용하여 모델을 훈련합니다. 학습 데이터(xs 및 ys), 에포크 수(100) 및 배치 크기(1)를 지정합니다. Epoch는 모델이 학습 데이터를 통과하는 횟수입니다. 배치 크기는 모델의 가중치를 업데이트하기 전에 모델이 사용할 교육 예제의 수입니다.

```javascript
model.fit(xs, ys, {epochs: 100, batchSize: 1});
```

## 예측하기

이제 모델이 학습되었으므로 모델을 사용하여 예측할 수 있습니다. model.predict() 함수를 사용하여 예측합니다. 값이 3인 1D 텐서를 전달합니다. 모델은 값이 9인 1D 텐서를 출력합니다.

```javascript
model.predict(tf.tensor2d([3], [1, 1])).print();
```

## 모델 미세 조정

학습된 모델이 있으면 성능을 개선하기 위해 모델을 미세 조정해야 할 수 있습니다. 이 섹션에서는 사전 학습된 모델을 미세 조정하는 방법을 보여줍니다.

미리 학습된 모델을 로드하는 것으로 시작하겠습니다. tf.loadLayersModel() 함수를 사용하여 모델을 로드합니다. 모델의 URL을 지정해야 합니다. 선행 학습된 모델 목록은 [여기](https://github.com/tensorflow/tfjs-models/tree/master/models)에서 찾을 수 있습니다.

```javascript
const model = tf.loadLayersModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

이제 모델을 로드했으므로 컴파일해야 합니다. 이전과 동일한 compile() 함수를 사용합니다. 그러나 이번에는 분류 정확도를 위해 최적화하도록 지정할 것입니다.

```javascript
model.compile({optimizer: tf.train.sgd(0.0001), loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

이제 모델 학습을 시작할 수 있습니다. fit() 함수를 다시 사용하겠습니다. 그러나 이번에는 에포크 수(5)와 유효성 검사 데이터(xs 및 ys)를 지정합니다. 유효성 검사 데이터는 각 에포크 후 모델을 평가하는 데 사용됩니다.

```javascript
model.fit(xs, ys, {epochs: 5, validationData: [xs, ys]});
```

모델을 학습한 후 모델을 사용하여 예측할 수 있습니다. 우리는 predict() 함수를 다시 사용할 것입니다. 이번에는 강아지 이미지를 전달하겠습니다. 모델은 각 클래스에 대해 하나씩 확률 배열을 출력합니다. 가장 높은 확률은 모델이 이미지가 속하는 것으로 예측하는 클래스입니다.

```javascript
model.predict(tf.tensor2d([image], [1, 224, 224, 3])).print();
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 기계 학습 모델을 훈련하고 미세 조정하는 방법을 보여주었습니다.