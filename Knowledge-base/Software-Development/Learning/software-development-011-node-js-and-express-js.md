---
title: 소프트웨어 개발 011: Node.js 및 Express.js
description: 
published: true
date: 2023-02-16T11:55:36.485Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:55:34.909Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Software Development 011: Node.js and Express.js***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-011-node-js-and-express-js)
{.links-list}


# 소프트웨어 개발 011: Node.js 및 Express.js

이 게시물에서는 소프트웨어 개발에 널리 사용되는 두 가지 도구인 Node.js와 Express.js를 살펴보겠습니다.

Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있는 JavaScript 런타임 환경입니다. 따라서 서버 측 애플리케이션 개발에 이상적입니다.

Express.js는 Node.js용 웹 애플리케이션 프레임워크입니다. 웹 애플리케이션 구축을 위한 일련의 도구를 제공합니다.

## Node.js

Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있는 JavaScript 런타임 환경입니다. 따라서 서버 측 애플리케이션 개발에 이상적입니다.

Node.js는 Google Chrome에서 사용되는 V8 JavaScript 엔진을 기반으로 합니다. 또한 Node.js에는 다양한 작업에 사용할 수 있는 오픈 소스 라이브러리의 대규모 생태계가 있습니다.

### Node.js 설치하기

Node.js 설치는 간단한 과정입니다. [Node.js 웹사이트](https://nodejs.org/en/)에서 Node.js 설치 프로그램을 다운로드할 수 있습니다.

설치 프로그램이 다운로드되면 실행하고 지침을 따릅니다. Node.js가 컴퓨터에 설치됩니다.

### Node.js 실행하기

Node.js가 설치되면 Node.js 런타임을 사용하여 JavaScript 코드를 실행할 수 있습니다.

JavaScript 파일을 실행하려면 다음 명령을 사용하십시오.

```
node {filename}
```

예를 들어 `hello.js`라는 파일을 실행하려면 다음 명령을 사용합니다.

```
node hello.js
```

Node.js는 `hello.js` 파일의 코드를 실행하고 결과를 콘솔에 출력합니다.

## 익스프레스.js

Express.js는 Node.js용 웹 애플리케이션 프레임워크입니다. 웹 애플리케이션 구축을 위한 일련의 도구를 제공합니다.

Express.js는 웹 애플리케이션 구축에 널리 사용되는 선택입니다. 사용하기 쉽고 대규모 사용자 커뮤니티가 있습니다.

### 헬로월드

간단한 "Hello, World!" Express.js를 사용하는 애플리케이션.

`hello.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Hello, World! app is listening on port 3000');
});
```

이 코드는 "Hello, World!"로 HTTP `GET` 요청에 응답하는 Express.js 애플리케이션을 생성합니다. 메시지.

`app.listen()` 메서드는 포트 3000에서 Express.js 애플리케이션을 시작합니다.

애플리케이션을 실행하려면 다음 명령을 사용하십시오.

```
node hello.js
```

이제 http://localhost:3000에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 게시물에서는 Node.js와 Express.js를 살펴보았습니다. Node.js를 설치하고 Node.js 런타임을 사용하여 JavaScript 코드를 실행하는 방법을 살펴보았습니다. 또한 Express.js를 사용하여 간단한 웹 애플리케이션을 만드는 방법도 살펴보았습니다.