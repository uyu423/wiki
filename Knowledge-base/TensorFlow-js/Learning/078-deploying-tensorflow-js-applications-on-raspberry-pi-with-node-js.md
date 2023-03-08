---
title: 078: Node.js를 사용하여 Raspberry Pi에 TensorFlow.js 애플리케이션 배포
description: 
published: true
date: 2023-02-03T01:04:40.515Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:04:38.864Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [078: Deploying TensorFlow.js Applications on Raspberry Pi with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/078-deploying-tensorflow-js-applications-on-raspberry-pi-with-node-js)
{.links-list}


## 소개

Raspberry Pi는 다양한 전자 프로젝트에 사용할 수 있는 신용 카드 크기의 컴퓨터입니다. 응용 범위가 넓어 교육, 산업, 연구 등 다양한 분야에서 사용할 수 있습니다.

Raspberry Pi의 가장 인기 있는 응용 프로그램 중 하나는 기계 학습을 위한 에지 장치로 사용하는 것입니다. TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

이 게시물에서는 TensorFlow.js용 Raspberry Pi를 설정하는 과정을 안내합니다. 또한 TensorFlow.js 애플리케이션을 Raspberry Pi에 배포하는 방법도 보여줍니다.

## 라즈베리파이 설정하기

가장 먼저 해야 할 일은 Raspberry Pi를 설정하는 것입니다. 이 링크의 지침을 따를 수 있습니다: https://www.raspberrypi.org/documentation/setup/

Raspberry Pi가 설정되면 Node.js를 설치해야 합니다. Node.js는 TensorFlow.js 애플리케이션을 실행하는 데 필요한 JavaScript 런타임입니다.

https://nodejs.org/en/download/package-manager/# installing-node-js-via-package-manager 링크의 지침에 따라 Raspberry Pi에 Node.js를 설치할 수 있습니다.

## TensorFlow.js 애플리케이션 배포

Node.js가 설치되면 이제 Raspberry Pi에 TensorFlow.js 애플리케이션을 배포할 수 있습니다.

TensorFlow.js 애플리케이션을 배포하는 방법에는 두 가지가 있습니다.

1. 웹 서버를 사용하여 애플리케이션을 제공합니다.
2. 명령줄 도구를 사용하여 애플리케이션을 배포합니다.

### 웹 서버 사용

첫 번째 방법은 웹 서버를 사용하여 애플리케이션을 제공하는 것입니다. 우리는 Node.js 웹 서버인 Express.js를 사용할 것입니다.

Express.js는 Node.js용 웹 애플리케이션 프레임워크입니다. 웹 애플리케이션 및 API를 구축하는 데 사용됩니다.

다음 명령을 실행하여 Express.js를 설치할 수 있습니다.

```
npm install express --save
```

Express.js가 설치되면 `app.js`라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello world!');
});

app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

이 코드는 `Hello world!` 문자열로 HTTP 요청에 응답하는 웹 서버를 생성합니다.

다음 명령을 실행하여 웹 서버를 시작할 수 있습니다.

```
node app.js
```

이제 http://localhost:3000에서 웹 서버에 액세스할 수 있습니다.

### 명령줄 도구 사용

두 번째 방법은 명령줄 도구를 사용하여 애플리케이션을 배포하는 것입니다. 우리는 TensorFlow.js CLI를 사용할 것입니다.

TensorFlow.js CLI는 TensorFlow.js 모델을 교육, 배포 및 작업하는 데 사용할 수 있는 명령줄 도구입니다.

다음 명령을 실행하여 TensorFlow.js CLI를 설치할 수 있습니다.

```
npm install -g @tensorflow/tfjs-node
```

TensorFlow.js CLI가 설치되면 이를 사용하여 TensorFlow.js 애플리케이션을 배포할 수 있습니다.

`app` 디렉토리에 TensorFlow.js 애플리케이션이 있다고 가정해 보겠습니다. 다음 명령을 실행하여 애플리케이션을 배포할 수 있습니다.

```
tfjs deploy --dir app
```

그러면 TensorFlow.js 애플리케이션을 제공하는 웹 서버가 시작됩니다. http://localhost:3000에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 게시물에서는 TensorFlow.js 애플리케이션을 Raspberry Pi에 배포하는 방법을 보여주었습니다. 또한 웹 서버를 사용하여 애플리케이션을 제공하는 방법도 보여 주었습니다.