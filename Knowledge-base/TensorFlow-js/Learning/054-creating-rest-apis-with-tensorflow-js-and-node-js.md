---
title: 054: TensorFlow.js 및 Node.js로 REST API 만들기
description: 
published: true
date: 2023-02-02T19:36:27.228Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:36:25.588Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [054: Creating REST APIs with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/054-creating-rest-apis-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js로 REST API 만들기

## 소개

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 REST API를 만드는 방법을 보여줍니다. 필요한 종속성 설치, 프로젝트 설정 및 코드 작성을 포함하여 프로젝트를 시작하고 실행하는 데 필요한 모든 단계를 살펴보겠습니다.

이 게시물을 마치면 TensorFlow.js 및 Node.js를 사용하여 고유한 REST API를 만들 수 있습니다.

## 전제 조건

시작하기 전에 따라하기 위해 필요한 몇 가지 사항이 있습니다.

- 텍스트 편집기. [Visual Studio Code](https://code.visualstudio.com/)를 권장합니다.
- [Node.js](https://nodejs.org/en/)가 컴퓨터에 설치되었습니다.
- [npm](https://www.npmjs.com/)이 컴퓨터에 설치되었습니다.
- [TensorFlow.js](https://js.tensorflow.org/)가 컴퓨터에 설치되었습니다.

## 프로젝트 설정

사전 요구 사항을 설정했으면 프로젝트 설정을 시작할 준비가 된 것입니다.

먼저 프로젝트의 새 디렉토리를 만듭니다. 우리는 `tfjs-rest-api`라고 부를 것입니다.

다음으로 프로젝트 디렉토리에서 `npm init`를 실행하여 프로젝트를 초기화합니다. 그러면 프로젝트에 대한 `package.json` 파일이 생성됩니다.

이제 `package.json` 파일이 있으므로 프로젝트에 대한 종속성을 설치할 수 있습니다. 다음 명령을 실행하여 [Express](https://expressjs.com/), [ Body-Parser ](https://www.npmjs.com/package/body-parser) 및 [ TensorFlow.js ]( https://www.npmjs.com/package/@tensorflow/tfjs):

```
npm install express body-parser @tensorflow/tfjs --save
```

그러면 종속 항목이 설치되고 `package.json` 파일에 추가됩니다.

## 코드 작성

이제 프로젝트가 설정되었으므로 코드 작성을 시작할 준비가 되었습니다.

텍스트 편집기를 열고 프로젝트 디렉토리에 새 파일을 만듭니다. 우리는 `index.js`라고 부를 것입니다.

이 파일에서는 이전에 설치한 종속성을 요구하는 것으로 시작합니다.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const tf = require('@tensorflow/tfjs');
```

다음으로 Express 서버를 설정합니다.

```javascript
const app = express();
const port = 3000;

app.use(bodyParser.json());

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

이제 서버가 설정되었으므로 API 끝점 작성을 시작할 수 있습니다.

첫 번째 끝점은 간단한 메시지를 반환하는 `/`에 대한 `GET` 요청입니다.

```javascript
app.get('/', (req, res) => {
  res.send('Hello, world!');
});
```

두 번째 엔드포인트는 `/predict`에 대한 `POST` 요청으로 숫자 배열을 받아 해당 숫자를 기반으로 예측을 반환합니다.

```javascript
app.post('/predict', (req, res) => {
  const input = tf.tensor2d([req.body.numbers], [1, req.body.numbers.length]);
  const output = model.predict(input);
  res.send(output.dataSync());
});
```

이 엔드포인트에서는 사전 학습된 [TensorFlow.js](https://js.tensorflow.org/) 모델을 사용하여 예측합니다. 이 모델은 [여기](https://storage.googleapis.com/tfjs-models/tfjs/mnist_model/model.json)에서 찾을 수 있습니다.

## API 테스트

이제 API 끝점을 설정했으므로 테스트할 준비가 되었습니다.

'GET' 엔드포인트를 테스트하려면 [Postman](https://www.getpostman.com/)과 같은 도구를 사용할 수 있습니다.

`POST` 엔드포인트를 테스트하려면 다음 명령을 사용할 수 있습니다.

```
curl -X POST -H "Content-Type: application/json" -d '{"numbers": [1, 2, 3, 4, 5]}' http://localhost:3000/predict
```

이것은 `[6]`의 예측을 반환해야 합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 REST API를 만드는 방법을 보여주었습니다. 필요한 종속성 설치, 프로젝트 설정 및 코드 작성을 포함하여 프로젝트를 시작하고 실행하는 데 필요한 모든 단계를 다루었습니다.

이 게시물이 끝나면 TensorFlow.js 및 Node.js를 사용하여 고유한 REST API를 만들 수 있어야 합니다.