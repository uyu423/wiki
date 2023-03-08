---
title: 019: TensorFlow.js 및 Node.js를 사용한 텍스트 분류
description: 
published: true
date: 2023-02-02T11:19:05.702Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:19:04.013Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [019: Text Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/019-text-classification-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 텍스트 분류

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 텍스트 분류 모델을 빌드하는 방법을 알아봅니다. 텍스트 분류는 인간 언어 데이터를 분석하고 작업하는 프로세스인 자연어 처리의 일반적인 작업입니다.

웹사이트 Rotten Tomatoes의 영화 리뷰 데이터 세트를 사용할 것입니다. 데이터 세트에는 각 리뷰에 대한 텍스트와 리뷰가 긍정적인지 부정적인지를 나타내는 레이블이 포함되어 있습니다. 이 데이터 세트를 사용하여 새 리뷰를 읽고 긍정적인지 부정적인지 예측할 수 있는 모델을 교육합니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- 컴퓨터에 설치된 Node.js 및 npm
- 텍스트 편집기 또는 IDE
- JavaScript에 대한 기본 지식

## 시작하기

먼저 새 Node.js 프로젝트를 만들어야 합니다. 프로젝트의 새 디렉터리를 만들고 npm으로 초기화합니다.

```
mkdir text-classification
cd text-classification
npm init -y
```

그러면 프로젝트에 대한 package.json 파일이 생성됩니다. 다음으로 사용할 종속성을 설치해야 합니다. 우리는 JavaScript에서 기계 학습 작업을 위한 라이브러리인 TensorFlow.js와 인간 언어 데이터 작업에 유용한 몇 가지 기능을 제공하는 자연 라이브러리를 사용할 것입니다.

```
npm install --save @tensorflow/tfjs natural
```

종속성이 설치되었으므로 이제 코딩을 시작할 수 있습니다. 프로젝트 디렉터리에 index.js라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here
```

이렇게 하면 다음 섹션에서 사용할 TensorFlow.js 및 자연 라이브러리를 가져옵니다.

## 데이터 준비

모델을 교육하기 전에 데이터를 준비해야 합니다. 영화 리뷰 데이터 세트는 reviews.csv라는 파일에 있으며 [여기에서 다운로드](https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv)할 수 있습니다.

index.js에 다음 코드를 추가하여 데이터를 로드하고 준비합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});
```

이 코드가 무엇을 하는지 살펴보겠습니다.

- 첫 번째 줄은 URL에서 데이터 세트를 로드합니다. 이 데이터 세트는 CSV 형식이므로 tf.data.csv() 함수를 사용하여 로드합니다.
- 두 번째 줄은 데이터를 섞습니다. 이것은 모델이 리뷰 순서를 학습하는 것이 아니라 리뷰 자체를 학습하는 것을 원하기 때문에 중요합니다.
- 세 번째 줄은 데이터를 훈련 세트와 테스트 세트로 나눕니다. 학습 세트는 모델을 훈련하는 데 사용되고 테스트 세트는 모델을 평가하는 데 사용됩니다.
- 네 번째 줄은 레이블을 원-핫 인코딩으로 변환합니다. 이는 기계 학습에서 범주형 데이터를 나타내는 일반적인 방법입니다.
- 다섯 번째와 여섯 번째 줄은 데이터를 정규화합니다. 이 단계는 모델이 훈련 데이터에 과적합되지 않도록 하기 때문에 중요합니다.

## 모델 구축

이제 데이터가 준비되었으므로 모델을 빌드할 수 있습니다. 순환 신경망(RNN)의 일종인 BiLSTM(Bidirectional Long Short-Term Memory) 모델을 사용할 것입니다.

다음 코드를 index.js에 추가하여 모델을 빌드합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
});
```

이 코드는 다음을 수행합니다.

- 첫 번째 라인은 Sequential 모델을 사용하여 모델을 구축합니다. 레이어의 선형 스택으로 구성된 모델 유형입니다.
- 두 번째 줄은 임베딩 레이어를 추가합니다. 이 레이어는 입력 데이터를 벡터 표현으로 변환하는 데 사용됩니다.
- 세 번째 줄은 양방향 레이어를 추가합니다. 이 계층은 데이터를 양방향으로 처리하는 데 사용됩니다.
- 네 번째 라인은 LSTM(Long Short-Term Memory) 레이어를 추가합니다. 이 계층은 오랜 기간 동안 정보를 기억하는 데 사용됩니다.
- 다섯 번째 줄은 Dense 레이어를 추가합니다. 이 계층은 데이터를 기반으로 예측하는 데 사용됩니다.
- 여섯 번째 줄은 모델을 컴파일합니다. 이 단계에서는 훈련을 위해 모델을 구성합니다.
- 일곱 번째 줄은 모델을 훈련시킵니다. 이 단계를 완료하는 데 몇 분 정도 걸립니다.
- 여덟 번째 라인은 모델을 평가합니다. 이 단계는 모델의 정확도를 콘솔에 출력합니다.

## 예측하기

이제 학습된 모델이 있으므로 이를 사용하여 예측할 수 있습니다. index.js에 다음 코드를 추가하여 예측합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const natural = require('natural');

// TODO: Add code here

// Load the dataset
const csvUrl = 'https://storage.googleapis.com/tfjs-examples/movie-reviews/data.csv';
const { data, labels } = tf.data.csv(csvUrl);

// Shuffle the data
const shuffledData = data.shuffle();

// Split the data into training and test sets
const [trainData, testData] = shuffledData.split([0.8, 0.2]);

// Convert the labels to a one-hot encoding
const trainLabels = trainData.map((_, i) => labels[i]).oneHot(2);
const testLabels = testData.map((_, i) => labels[i]).oneHot(2);

// Normalize the data
const trainDataNormalized = trainData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

const testDataNormalized = testData.map(review => {
  // Convert the review to lowercase
  const lowered = review.toLowerCase();
  // Tokenize the review
  const tokens = natural.WordTokenizer().tokenize(lowered);
  // Remove stopwords
  const filtered = tokens.filter(token => !natural.stopwords.some(stopword => stopword === token));
  // Join the tokens back into a string
  const text = filtered.join(' ');
  // Return the normalized review
  return text;
});

// Build the model
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 1000,
  outputDim: 32,
  inputLength: 100
}));
model.add(tf.layers.bidirectional({
  layer: tf.layers.lstm({
    units: 32
  })
}));
model.add(tf.layers.dense({
  units: 2,
  activation: 'softmax'
}));
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'adam',
  metrics: ['accuracy']
});

// Train the model
model.fit(trainDataNormalized, trainLabels, {
  epochs: 5,
  validationData: [testDataNormalized, testLabels]
}).then(() => {
  // Evaluate the model
  const results = model.evaluate(testDataNormalized, testLabels);
  console.log(results);
  
  // Make a prediction
  const prediction = model.predict(['this movie was great']);
  console.log(prediction);
});
```

이 코드는 다음을 수행합니다.

- 첫 번째 줄은 URL에서 데이터 세트를 로드합니다. 이 데이터 세트는 CSV 형식이므로 tf.data.csv() 함수를 사용하여 로드합니다.
- 두 번째 줄은 데이터를 섞습니다. 이것은 모델이 리뷰 순서를 학습하는 것이 아니라 리뷰 자체를 학습하는 것을 원하기 때문에 중요합니다.
- 세 번째 줄은 데이터를 훈련 세트와 테스트 세트로 나눕니다. 학습 세트는 모델을 훈련하는 데 사용되고 테스트 세트는 모델을 평가하는 데 사용됩니다.
- 네 번째 줄은 레이블을 원-핫 인코딩으로 변환합니다. 이는 기계 학습에서 범주형 데이터를 나타내는 일반적인 방법입니다.
- 다섯 번째와 여섯 번째 줄은 데이터를 정규화합니다. 이 단계는 모델이 훈련 데이터에 과적합되지 않도록 하기 때문에 중요합니다.
- 일곱 번째 라인은 Sequential 모델을 사용하여 모델을 구축합니다. 레이어의 선형 스택으로 구성된 모델 유형입니다.
- 여덟 번째 줄은 임베딩 레이어를 추가합니다. 이 레이어는 입력 데이터를 벡터 표현으로 변환하는 데 사용됩니다.
- 아홉 번째 줄은 양방향 레이어를 추가합니다. 이 계층은 데이터를 양방향으로 처리하는 데 사용됩니다.
- 10번째 줄은 LSTM(Long Short-Term Memory) 레이어를 추가합니다. 이 계층은 오랜 기간 동안 정보를 기억하는 데 사용됩니다.
- 11번째 줄은 Dense 레이어를 추가합니다. 이 계층은 데이터를 기반으로 예측하는 데 사용됩니다.
- 12번째 줄은 모델을 컴파일합니다. 이 단계에서는 훈련을 위해 모델을 구성합니다.
- 13번째 줄은 모델을 학습시킵니다. 이 단계를 완료하는 데 몇 분 정도 걸립니다.
- 14번째 줄은 모델을 평가합니다. 이 단계는 모델의 정확도를 콘솔에 출력합니다.
- 15번째 줄은 예측을 합니다. 이 단계는 예측을 콘솔에 인쇄합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 텍스트 분류 모델을 빌드하는 방법을 배웠습니다. 먼저 데이터를 로드하고 준비한 다음 모델을 구축하고 교육했습니다. 마지막으로 모델을 사용하여 예측했습니다.

텍스트 분류는 자연어 처리의 일반적인 작업이며 이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 텍스트 분류 모델을 빌드하는 방법을 보여줍니다.