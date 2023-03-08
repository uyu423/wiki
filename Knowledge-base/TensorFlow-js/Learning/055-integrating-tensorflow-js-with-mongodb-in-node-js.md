---
title: 055: TensorFlow.js와 Node.js의 MongoDB 통합
description: 
published: true
date: 2023-02-02T19:43:49.243Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:43:44.590Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [055: Integrating TensorFlow.js with MongoDB in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/055-integrating-tensorflow-js-with-mongodb-in-node-js)
{.links-list}


# 05: Node.js에서 MongoDB와 TensorFlow.js 통합

이 게시물에서는 TensorFlow.js를 Node.js에서 MongoDB와 통합하는 방법을 알아봅니다. 다음 주제를 다룹니다.

- TensorFlow.js가 무엇인가요?
- 몽고DB란?
- TensorFlow.js 및 MongoDB 설치 방법
- TensorFlow.js를 MongoDB와 통합하는 방법

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. Google에서 개발했으며 Apache 2.0 오픈 소스 라이선스에 따라 출시되었습니다.

TensorFlow.js는 다음과 같은 다양한 방법으로 사용할 수 있습니다.

- 브라우저에서 JavaScript 사용
- Node.js에서 JavaScript 사용
- React Native 앱에서
- Docker 컨테이너에서

## 몽고DB란?

MongoDB는 강력한 문서 지향 데이터베이스 시스템입니다. MongoDB, Inc.에서 개발했으며 GNU Affero General Public License에 따라 출시되었습니다.

MongoDB는 다음과 같은 다양한 방법으로 사용할 수 있습니다.

- 전통적인 데이터베이스 시스템으로
- NoSQL 데이터베이스로
- 문서 지향 데이터베이스로
- 그래프 데이터베이스로

## TensorFlow.js 및 MongoDB 설치 방법

TensorFlow.js를 MongoDB와 통합하기 전에 TensorFlow.js와 MongoDB를 모두 설치해야 합니다.

### TensorFlow.js 설치하기

TensorFlow.js를 설치하는 방법에는 두 가지가 있습니다.

- 스크립트 태그 사용
- 패키지 관리자 사용

#### 스크립트 태그 사용

스크립트 태그를 사용하여 HTML 파일에 TensorFlow.js 라이브러리를 포함할 수 있습니다.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

#### 패키지 관리자 사용

npm 또는 yarn과 같은 패키지 관리자를 사용하는 경우 다음 명령을 사용하여 TensorFlow.js를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

### 몽고DB 설치하기

MongoDB를 설치하는 방법에는 두 가지가 있습니다.

- 스크립트 사용
- 패키지 관리자 사용

#### 스크립트 사용

스크립트를 사용하여 MongoDB를 설치할 수 있습니다. 스크립트가 MongoDB를 다운로드하고 설치합니다.

```
curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-4.2.2.tgz
tar -zxvf mongodb-osx-x86_64-4.2.2.tgz
mkdir -p mongodb
cp -R -n mongodb-osx-x86_64-4.2.2/ mongodb
```

#### 패키지 관리자 사용

Homebrew와 같은 패키지 관리자를 사용하는 경우 다음 명령을 사용하여 MongoDB를 설치할 수 있습니다.

```
brew install mongodb
```

## TensorFlow.js를 MongoDB와 통합하는 방법

이제 TensorFlow.js와 MongoDB가 설치되었으므로 통합을 시작할 수 있습니다.

이렇게 하려면 다음을 수행해야 합니다.

- MongoDB Node.js 드라이버 설치
- MongoDB 데이터베이스에 연결
- 스키마 생성
- 모델 교육
- 모델 배포

### MongoDB Node.js 드라이버 설치

가장 먼저 해야 할 일은 MongoDB Node.js 드라이버를 설치하는 것입니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install mongodb
```

### MongoDB 데이터베이스에 연결

다음으로 MongoDB 데이터베이스에 연결해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';

MongoClient.connect(url, { useNewUrlParser: true }, (err, client) => {
  if (err) throw err;

  const db = client.db('test');

  console.log('Connected to MongoDB');
});
```

### 스키마 생성

이제 MongoDB 데이터베이스에 연결되었으므로 스키마를 생성해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const schema = new mongoose.Schema({
  name: String,
  age: Number,
  gender: String
});
```

### 모델 교육

이제 스키마가 있으므로 모델을 교육할 수 있습니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

model.compile({ loss: 'meanSquaredError', optimizer: 'sgd' });

const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

model.fit(xs, ys, { epochs: 10 }).then(() => {
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

### 모델 배포

마지막으로 모델을 배포해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.use(express.static('public'));

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

app.listen(port, () => console.log(`Listening on port ${port}`));
```

## 결론

이 게시물에서는 TensorFlow.js를 Node.js에서 MongoDB와 통합하는 방법을 배웠습니다. 우리는 다음 주제를 다루었습니다.

- TensorFlow.js가 무엇인가요?
- 몽고DB란?
- TensorFlow.js 및 MongoDB 설치 방법
- TensorFlow.js를 MongoDB와 통합하는 방법

질문이나 의견이 있으시면 언제든지 아래에 남겨주세요.