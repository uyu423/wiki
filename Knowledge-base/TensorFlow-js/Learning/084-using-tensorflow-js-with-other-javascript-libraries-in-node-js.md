---
title: 084: Node.js에서 다른 JavaScript 라이브러리와 함께 TensorFlow.js 사용
description: 
published: true
date: 2023-02-03T02:37:09.683Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:37:08.077Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [084: Using TensorFlow.js with Other JavaScript Libraries in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/084-using-tensorflow-js-with-other-javascript-libraries-in-node-js)
{.links-list}


# Node.js의 다른 JavaScript 라이브러리와 함께 TensorFlow.js 사용

TensorFlow.js는 JavaScript에서 기계 학습을 위한 강력한 도구이며 다른 JavaScript 라이브러리와 잘 작동합니다. 이 게시물에서는 TensorFlow.js를 Node.js 및 Express와 함께 사용하는 방법을 보여드리겠습니다.

## 전제 조건

이 게시물을 따라하려면 몇 가지가 필요합니다.

- Node.js 및 npm 설치
- 텍스트 편집기 - Visual Studio Code를 권장합니다.
- JavaScript에 대한 기본 지식

## 시작하기

먼저 프로젝트를 위한 새 디렉토리를 생성해 보겠습니다.

```
mkdir tensorflowjs-node
cd tensorflowjs-node
```

다음으로 npm으로 프로젝트를 초기화합니다.

```
npm init -y
```

이제 프로젝트가 설정되었으므로 필요한 종속성을 설치할 수 있습니다. 다음 라이브러리를 사용할 것입니다.

- [TensorFlow.js](https://www.tensorflow.org/js)
- [익스프레스](https://expressjs.com/)
- [바디 파서](https://www.npmjs.com/package/body-parser)

다음 명령을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install --save @tensorflow/tfjs express body-parser
```

## 안녕하세요, TensorFlow.js!

종속성을 설치했으므로 이제 일부 코드 작성을 시작할 수 있습니다. `index.js`라는 파일을 생성하여 시작하겠습니다. 이 파일에서 "Hello, TensorFlow.js!"를 출력하는 간단한 스크립트를 작성합니다. 콘솔에:

```javascript
// index.js

const tf = require('@tensorflow/tfjs');

console.log('Hello, TensorFlow.js!');
```

Node.js로 이 스크립트를 실행하면 다음 출력이 표시됩니다.

```
$ node index.js
Hello, TensorFlow.js!
```

## Express와 함께 TensorFlow.js 사용

Node.js 스크립트에서 TensorFlow.js를 사용하는 방법을 살펴보았으니 이제 Express와 함께 사용하는 방법을 살펴보겠습니다. 이 예에서는 숫자 목록으로 `GET` 요청에 응답하는 간단한 서버를 만듭니다.

먼저 필요한 종속성을 요구해 보겠습니다.

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

다음으로 ` Express` 인스턴스를 생성하고 `body-parser`를 구성하여 JSON 본문을 구문 분석합니다.

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

이제 숫자 목록으로 `GET` 요청에 응답할 경로를 정의해 보겠습니다.

```javascript
// index.js

app.get('/numbers', (req, res) => {
  const numbers = [1, 2, 3, 4, 5];
  res.json(numbers);
});
```

마지막으로 포트 `3000`에서 서버를 시작합니다.

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

Node.js로 이 스크립트를 실행하면 다음 출력이 표시됩니다.

```
$ node index.js
Server is listening on port 3000
```

이제 `http://localhost:3000/numbers`에 `GET` 요청을 보낼 수 있으며 숫자 목록이 포함된 JSON 응답을 받게 됩니다.

## Express 및 body-parser와 함께 TensorFlow.js 사용

이전 섹션에서는 Express와 함께 TensorFlow.js를 사용하는 방법을 살펴보았습니다. 이 섹션에서는 예제를 확장하여 `body-parser`를 사용하여 JSON 본문을 구문 분석하는 방법을 보여줍니다.

먼저 필요한 종속성을 요구해 보겠습니다.

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

다음으로 ` Express` 인스턴스를 생성하고 `body-parser`를 구성하여 JSON 본문을 구문 분석합니다.

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

이제 요청 본문으로 `POST` 요청에 응답할 경로를 정의해 보겠습니다.

```javascript
// index.js

app.post('/body', (req, res) => {
  res.json(req.body);
});
```

마지막으로 포트 `3000`에서 서버를 시작합니다.

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

Node.js로 이 스크립트를 실행하면 다음 출력이 표시됩니다.

```
$ node index.js
Server is listening on port 3000
```

이제 JSON 본문과 함께 `http://localhost:3000/body`에 `POST` 요청을 보낼 수 있으며 요청 본문과 함께 JSON 응답을 받게 됩니다.

## Express 및 body-parser와 함께 TensorFlow.js 사용

이전 섹션에서는 Express 및 body-parser와 함께 TensorFlow.js를 사용하는 방법을 살펴보았습니다. 이 섹션에서는 예제를 확장하여 TensorFlow.js를 사용하여 요청 본문에 대한 추론을 수행하는 방법을 보여줍니다.

먼저 필요한 종속성을 요구해 보겠습니다.

```javascript
// index.js

const tf = require('@tensorflow/tfjs');
const express = require('express');
const bodyParser = require('body-parser');
```

다음으로 ` Express` 인스턴스를 생성하고 `body-parser`를 구성하여 JSON 본문을 구문 분석합니다.

```javascript
// index.js

const app = express();
app.use(bodyParser.json());
```

이제 요청 본문으로 `POST` 요청에 응답할 경로를 정의해 보겠습니다.

```javascript
// index.js

app.post('/inference', (req, res) => {
  const input = tf.tensor(req.body);
  const output = tf.add(input, 1);
  res.json(output.dataSync());
});
```

마지막으로 포트 `3000`에서 서버를 시작합니다.

```javascript
// index.js

app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

Node.js로 이 스크립트를 실행하면 다음 출력이 표시됩니다.

```
$ node index.js
Server is listening on port 3000
```

이제 JSON 본문과 함께 `http://localhost:3000/inference`에 `POST` 요청을 보낼 수 있으며 추론 결과와 함께 JSON 응답을 받게 됩니다.

## 마무리

이 게시물에서는 TensorFlow.js를 Node.js 및 Express와 함께 사용하는 방법을 살펴보았습니다. 또한 TensorFlow.js를 body-parser와 함께 사용하여 JSON 본문을 구문 분석하는 방법도 살펴보았습니다.

## 자원

- [TensorFlow.js](https://www.tensorflow.org/js)
- [익스프레스](https://expressjs.com/)
- [바디 파서](https://www.npmjs.com/package/body-parser)