---
title: 027: TensorFlow.js 및 Node.js를 사용한 이상 감지
description: 
published: true
date: 2023-02-02T13:17:49.025Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:17:47.449Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [027: Anomaly Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/027-anomaly-detection-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 이상 탐지

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이상 감지 모델을 빌드하는 방법을 살펴보겠습니다. 우리는 지난 140년 동안 매일 측정한 온도 데이터 세트를 사용하여 훈련 세트와 테스트 세트로 나눌 것입니다.

TensorFlow.js 라이브러리를 사용하여 모델을 구축하고 훈련할 것입니다. TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

TensorFlow.js의 Sequential 모델 API를 사용할 것입니다. 순차 모델은 레이어의 선형 스택으로 구성된 일종의 신경망입니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- 텍스트 편집기. [Visual Studio Code](https://code.visualstudio.com/)를 추천합니다.
- [Node.js](https://nodejs.org/en/)가 컴퓨터에 설치되었습니다.
- 자바스크립트에 대한 기본적인 이해.

## 데이터 얻기

첫 번째 단계는 데이터를 가져오는 것입니다. 우리는 지난 140년 동안의 일일 온도 판독값 데이터 세트를 사용할 것입니다. 데이터 세트는 [여기](https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data)에서 사용할 수 있습니다.

데이터 세트를 다운로드하고 압축을 풉니다. 이제 `GlobalLandTemperaturesByCountry`라는 폴더가 있어야 합니다.

## 데이터 준비

다음 단계는 데이터를 준비하는 것입니다. 데이터 세트를 교육 및 테스트 세트로 분할해야 합니다. 또한 데이터를 정규화해야 합니다. 즉, 데이터가 0과 1 사이가 되도록 스케일링해야 합니다.

이를 돕기 위해 [`normalize-dataset`](https://www.npmjs.com/package/normalize-dataset) 패키지를 사용할 것입니다. 다음 명령을 실행하여 설치하십시오.

```
npm install --save normalize-dataset
```

`prepare-data.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const fs = require('fs');
const path = require('path');
const normalizeDataset = require('normalize-dataset');

const dataPath = path.join(__dirname, 'GlobalLandTemperaturesByCountry.csv');
const data = fs.readFileSync(dataPath, 'utf8');

// Split the data into training and testing sets
const [train, test] = normalizeDataset.splitDataset(data, 0.8);

// Save the training and testing sets to files
fs.writeFileSync(path.join(__dirname, 'train.csv'), train);
fs.writeFileSync(path.join(__dirname, 'test.csv'), test);
```

다음 명령을 실행하여 코드를 실행합니다.

```
node prepare-data.js
```

이제 프로젝트에 `train.csv` 및 `test.csv`라는 두 개의 새 파일이 있어야 합니다. 모델을 훈련하고 테스트하는 데 사용할 훈련 및 테스트 세트입니다.

## 모델 구축

이제 데이터가 있으므로 모델 구축을 시작할 수 있습니다. TensorFlow.js의 Sequential 모델 API를 사용할 것입니다. 순차 모델은 레이어의 선형 스택으로 구성된 일종의 신경망입니다.

`model.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Create a sequential model
const model = tf.sequential();

// Add a single hidden layer
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

// Add an output layer
model.add(tf.layers.dense({ units: 1, activation: 'sigmoid' }));

// Compile the model
model.compile({
  loss: 'binaryCrossentropy',
  optimizer: 'adam'
});

module.exports = model;
```

위의 코드에서 하나의 숨겨진 레이어와 하나의 출력 레이어가 있는 순차 모델을 만들었습니다. 또한 `binaryCrossentropy` 손실 함수와 `adam` 옵티마이저를 사용하여 모델을 컴파일했습니다.

## 모델 교육

이제 모델이 있으므로 모델을 훈련해야 합니다. 이전에 준비한 학습 세트를 모델에 제공하여 이를 수행합니다.

`train.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the training set from a file
const trainPath = path.join(__dirname, 'train.csv');
const trainData = tf.data.csv(trainPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Train the model
model.fitDataset(trainData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

위의 코드에서는 파일에서 훈련 세트를 읽고 `fitDataset` 함수에 전달했습니다. 이 함수는 10 epoch 동안 모델을 훈련합니다. Epoch는 전체 훈련 세트에 대한 하나의 반복입니다.

또한 각 에포크 후 손실을 기록하도록 `onEpochEnd` 콜백을 구성했습니다. 손실은 모델이 얼마나 잘 수행되고 있는지를 측정한 것입니다. 우리는 가능한 한 손실이 적기를 원합니다.

## 모델 테스트

이제 모델을 교육했으므로 테스트해야 합니다. 이전에 준비한 테스트 세트를 모델에 제공하여 이를 수행합니다.

`test.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const fs = require('fs');
const path = require('path');

const model = require('./model');

// Read the testing set from a file
const testPath = path.join(__dirname, 'test.csv');
const testData = tf.data.csv(testPath, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});

// Evaluate the model
model.evaluateDataset(testData).then(results => {
  console.log(`Loss: ${results.loss}`);
});
```

위의 코드에서는 파일에서 테스트 세트를 읽고 `evaluateDataset` 함수에 전달했습니다. 이 함수는 모델을 평가하고 손실을 반환합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이상 감지 모델을 빌드하는 방법을 살펴보았습니다. 우리는 데이터를 준비하고, 모델을 구축하고, 모델을 교육하고 테스트했습니다.