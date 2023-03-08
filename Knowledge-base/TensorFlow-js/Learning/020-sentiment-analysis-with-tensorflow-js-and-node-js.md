---
title: 020: TensorFlow.js 및 Node.js를 사용한 감정 분석
description: 
published: true
date: 2023-02-02T11:36:30.927Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:36:29.267Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [020: Sentiment Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/020-sentiment-analysis-with-tensorflow-js-and-node-js)
{.links-list}


# 020: TensorFlow.js 및 Node.js를 사용한 감성 분석

## 소개

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 감정 분석을 수행하는 방법을 다룰 것입니다. 감정 분석은 글이 긍정적인지, 부정적인지 또는 중립적인지를 계산적으로 결정하는 프로세스입니다. 종종 소셜 미디어에 대한 여론을 측정하는 데 사용되며 다양한 다른 응용 프로그램이 있습니다.

우리는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리인 TensorFlow.js 라이브러리를 사용할 것입니다. TensorFlow.js는 감정 분석에 사용할 Node.js 환경에서 사용할 수 있습니다.

## 시작하기

시작하기 전에 설정해야 할 몇 가지 사항이 있습니다. 먼저 컴퓨터에 Node.js가 설치되어 있어야 합니다. [Node.js 웹사이트](https://nodejs.org/en/)에서 다운로드할 수 있습니다.

Node.js를 설치했으면 TensorFlow.js 라이브러리를 설치해야 합니다. 다음 명령으로 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 감정 분석 프로그램을 위한 새 파일을 만들어야 합니다. 우리는 그것을 `sentiment.js`라고 부를 것입니다. 즐겨 사용하는 텍스트 편집기로 이 작업을 수행할 수 있습니다.

## TensorFlow.js 환경 초기화

`sentiment.js` 파일에서 가장 먼저 해야 할 일은 TensorFlow.js 환경을 초기화하는 것입니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');
```

이렇게 하면 TensorFlow.js 라이브러리가 프로그램에 로드되어 사용할 수 있습니다.

## 데이터세트 로드

이제 TensorFlow.js 환경이 설정되었으므로 감정 분석 모델을 교육하는 데 사용할 데이터 세트를 로드해야 합니다. [IMDB 영화 리뷰 데이터 세트](https://ai.stanford.edu/~amaas/data/sentiment/)를 사용할 것입니다. 이 데이터 세트에는 각각 0(부정적) 또는 1(긍정적) 레이블이 있는 50,000개의 영화 리뷰가 포함되어 있습니다.

다음 코드를 사용하여 이 데이터 세트를 프로그램에 로드할 수 있습니다.

```javascript
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/imdb_reviews.csv');
```

이렇게 하면 데이터세트가 `dataset` 변수에 로드됩니다.

## 데이터세트 전처리

훈련을 위해 데이터 세트를 사용하기 전에 사전 처리가 필요합니다. 여기에는 데이터 세트를 교육 및 테스트 세트로 분할하고 텍스트 데이터를 숫자 벡터로 변환하는 작업이 포함됩니다.

다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const [train, test] = dataset.split(0.8);

const vectorizer = new tf.layers.Embedding(10000, 16);

const trainX = train.map(example => vectorizer.apply(example.text));
const testX = test.map(example => vectorizer.apply(example.text));
const trainY = train.map(example => example.label);
const testY = test.map(example => example.label);
```

이 코드는 데이터 세트를 교육 및 테스트 세트로 분할한 다음 텍스트 데이터를 벡터화합니다. 벡터화된 데이터는 훈련 세트와 테스트 세트의 `trainX` 및 `testX` 변수에 각각 저장됩니다. 학습 및 테스트 세트의 레이블은 각각 `trainY` 및 `testY` 변수에 저장됩니다.

## 모델 구축

이제 데이터 세트를 사전 처리했으므로 감정 분석에 사용할 모델을 빌드할 수 있습니다. 하나의 숨겨진 레이어가 있는 간단한 신경망을 사용할 것입니다.

다음 코드를 사용하여 모델을 빌드할 수 있습니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 16, activation: 'relu', inputShape: [16] }));
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));
model.compile({ loss: 'binaryCrossentropy', optimizer: 'adam' });
```

이 코드는 새로운 `sequential` 모델을 생성한 다음 히든 레이어와 출력 레이어를 모델에 추가합니다. 숨겨진 계층에는 16개의 단위가 있고 출력 계층에는 1개의 단위가 있습니다. 모델은 `binaryCrossentropy` 손실 함수와 `adam` 옵티마이저로 컴파일됩니다.

## 모델 훈련

이제 모델을 구축했으므로 데이터 세트에서 학습할 수 있습니다. 10 epoch 동안 학습할 것입니다. 즉, 모델이 학습 데이터를 10번 보게 됩니다.

다음 코드를 사용하여 모델을 학습할 수 있습니다.

```javascript
model.fit(trainX, trainY, { epochs: 10 })
  .then(() => {
    // evaluate the model on the test set
  });
```

이 코드는 학습 세트에서 모델을 학습한 다음 테스트 세트에서 평가합니다.

## 모델 평가

모델이 훈련되면 테스트 세트에서 성능을 평가할 수 있습니다. 이를 위해 `model.evaluate()` 메소드를 사용할 것입니다.

다음 코드를 사용하여 모델을 평가할 수 있습니다.

```javascript
model.evaluate(testX, testY)
  .then(results => {
    // log the results
  });
```

이 코드는 테스트 세트에서 모델을 평가하고 결과를 출력합니다.

## 예측하기

이제 학습된 모델이 있으므로 이를 사용하여 새 데이터를 예측할 수 있습니다. 이를 위해 `model.predict()` 메서드를 사용합니다.

다음 코드를 사용하여 예측할 수 있습니다.

```javascript
const prediction = model.predict(tf.tensor2d([[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]]));
prediction.print();
```

이 코드는 `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]` 데이터에 대한 예측을 수행합니다. `print()` 메서드는 예측을 콘솔에 인쇄합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 감정 분석을 수행하는 방법을 다루었습니다. 데이터 세트를 로드 및 전처리하고, 모델을 구축하고, 모델을 훈련하고, 모델을 사용하여 예측하는 방법을 다루었습니다.