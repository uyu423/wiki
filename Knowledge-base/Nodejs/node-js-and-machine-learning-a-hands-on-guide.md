---
title: Node.js 및 기계 학습: 실습 가이드
description: 
published: true
date: 2023-02-25T02:32:50.720Z
tags: 
editor: markdown
dateCreated: 2023-02-25T02:32:43.189Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js and Machine Learning: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-machine-learning-a-hands-on-guide)
{.links-list}


# Node.js와 기계 학습: 실습 가이드

기계 학습은 컴퓨터에게 데이터를 제공하여 스스로 결정을 내리도록 가르치는 과정입니다. 이것은 문제를 해결하기 위해 따를 수 있는 일련의 규칙인 알고리즘을 생성함으로써 수행됩니다. Node.js는 서버에서 JavaScript를 실행할 수 있는 JavaScript 런타임 환경입니다. 또한 서버 측 애플리케이션 개발에도 사용됩니다.

이 기사에서는 기계 학습에 Node.js를 사용하는 방법을 살펴보겠습니다. 인기 있는 기계 학습 라이브러리인 TensorFlow.js를 사용할 것입니다. TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

## 환경 설정

기계 학습에 Node.js를 사용하기 전에 개발 환경을 설정해야 합니다. 우리는 Node.js 런타임 환경과 npm 패키지 관리자를 사용할 것입니다.

### Node.js

[Node.js 웹사이트](https://nodejs.org/en/)에서 안정적인 최신 Node.js 릴리스를 다운로드하세요. 다운로드가 완료되면 설치 프로그램을 실행합니다.

### npm

npm은 JavaScript용 패키지 관리자입니다. 패키지를 설치, 업데이트 및 제거하는 데 사용됩니다. npm은 Node.js와 함께 번들로 제공되므로 별도로 설치할 필요가 없습니다.

## 헬로월드

이제 Node.js와 npm이 설치되었으므로 첫 번째 Node.js 프로그램을 만들어 보겠습니다. `hello.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
console.log("Hello, world!");
```

프로그램을 실행하려면 명령 프롬프트 또는 터미널을 열고 다음 명령을 실행합니다.

```
node hello.js
```

다음 출력이 표시되어야 합니다.

```
Hello, world!
```

## TensorFlow.js

이제 개발 환경이 설정되었으므로 TensorFlow.js를 설치할 수 있습니다. TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

TensorFlow.js를 설치하려면 명령 프롬프트 또는 터미널을 열고 다음 명령을 실행합니다.

```
npm install @tensorflow/tfjs
```

이렇게 하면 TensorFlow.js와 모든 종속 항목이 설치됩니다.

## 모델 교육

이제 TensorFlow.js가 설치되었으므로 간단한 기계 학습 모델을 교육해 보겠습니다. 우리는 [ Iris Dataset ](https://en.wikipedia.org/wiki/Iris_flower_data_set)을 사용할 것입니다. Iris Dataset은 Iris 꽃의 150개 레코드 세트입니다. 각 레코드에는 다음 속성이 포함됩니다.

* 꽃받침 길이
* 꽃받침 폭
* 꽃잎 길이
* 꽃잎 폭
* 종

[ K-Nearest Neighbors ](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) 알고리즘을 사용하여 모델을 훈련할 것입니다. K-Nearest Neighbors는 분류 및 회귀에 사용할 수 있는 간단한 알고리즘입니다.

`knn.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');
// Load the Iris Dataset
const irisDataset = require('./iris.json');
// Load the K-Means algorithm
const kMeans = require('@tensorflow/tfjs-kmeans');
 
// Convert the dataset to a Tensor
const dataset = tf.tensor2d(irisDataset.map(item => [
  item.sepal_length,
  item.sepal_width,
  item.petal_length,
  item.petal_width,
]));
 
// Train the model
kMeans.train({
  dataset,
  numClusters: 3,
  iterations: 10,
  distanceFunction: 'euclidean',
}).then(model => {
  // Use the model to predict the class of a new record
  const prediction = model.predict(tf.tensor2d([
    [5.1, 3.5, 1.4, 0.2],
  ]));
  // Print the predicted class for the new record
  prediction.print();
});
```

위의 코드에서 먼저 TensorFlow.js, Iris Dataset 및 K-Means 알고리즘을 로드했습니다. 그런 다음 데이터 세트를 Tensor로 변환했습니다. 다음으로 K-Means 알고리즘을 사용하여 모델을 교육했습니다. 마지막으로 모델을 사용하여 새 레코드의 클래스를 예측했습니다.

프로그램을 실행하려면 명령 프롬프트 또는 터미널을 열고 다음 명령을 실행합니다.

```
node knn.js
```

다음 출력이 표시되어야 합니다.

```
Tensor
[[0]]
```

출력은 새 레코드가 클래스 0에 속함을 나타냅니다. 클래스 0은 Iris setosa 종에 해당합니다.

## 모델 배포

기계 학습 모델을 교육했으므로 이제 이를 웹 애플리케이션으로 배포해 보겠습니다. [ Express.js ](https://expressjs.com/) 웹 프레임워크를 사용하여 웹 애플리케이션을 만들 것입니다.

다음 명령을 실행하여 Express.js 프레임워크를 설치합니다.

```
npm install express
```

`app.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
// Load the Express.js framework
const express = require('express');
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');
// Load the K-Means algorithm
const kMeans = require('@tensorflow/tfjs-kmeans');
 
// Create a new Express.js application
const app = express();
 
// Train the model
kMeans.train({
  dataset,
  numClusters: 3,
  iterations: 10,
  distanceFunction: 'euclidean',
}).then(model => {
  // Define a route that returns the predictions
  app.get('/predict', (req, res) => {
    // Use the model to predict the class of a new record
    const prediction = model.predict(tf.tensor2d([
      [req.query.sepal_length, req.query.sepal_width, req.query.petal_length, req.query.petal_width],
    ]));
    // Return the predictions as a JSON object
    res.json(prediction.dataSync());
  });
 
  // Start the Express.js server
  app.listen(3000, () => console.log('Server started on port 3000'));
});
```

위의 코드에서 먼저 Express.js, TensorFlow.js 및 K-Means 알고리즘을 로드했습니다. 그런 다음 K-Means 알고리즘을 사용하여 모델을 교육했습니다. 다음으로 예측을 반환하는 경로를 정의했습니다. 마지막으로 Express.js 서버를 시작했습니다.

프로그램을 실행하려면 명령 프롬프트 또는 터미널을 열고 다음 명령을 실행합니다.

```
node app.js
```

다음 출력이 표시되어야 합니다.

```
Server started on port 3000
```

웹 브라우저를 열고 http://localhost:3000/predict?sepal_length=5.1&sepal_width=3.5&petal_length=1.4&petal_width=0.2로 이동합니다. 다음 출력이 표시되어야 합니다.

```
[0]
```

출력은 새 레코드가 클래스 0에 속함을 나타냅니다. 클래스 0은 Iris setosa 종에 해당합니다.

## 결론

이 기사에서는 기계 학습에 Node.js를 사용하는 방법을 살펴보았습니다. 우리는 인기 있는 기계 학습 라이브러리인 TensorFlow.js를 사용했습니다. TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.