---
title: Node.js로 RESTful API를 구축하는 방법
description: 
published: true
date: 2023-03-02T10:32:26.176Z
tags: 
editor: markdown
dateCreated: 2023-03-02T10:32:18.818Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a RESTful API with Node.js***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-restful-api-with-node-js)
{.links-list}


Node.js는 다양성과 확장성으로 인해 개발자들 사이에서 가장 인기 있는 기술 중 하나입니다. 고성능 서버 측 애플리케이션을 구축하는 프로세스를 단순화합니다. RESTful API는 단순성, 유연성 및 확장성 때문에 웹 서비스를 구축하는 데 선호되는 방법이 되었습니다. 이 기사에서는 Node.js로 RESTful API를 구축하는 과정을 안내합니다.

## RESTful API란 무엇인가요?

RESTful API는 GET, POST, PUT 및 DELETE와 같은 HTTP 메서드를 사용하여 웹 서비스를 구축하기 위한 아키텍처 스타일입니다. 이해하고 구현하기 쉬운 가볍고 유연한 아키텍처입니다. RESTful API는 URI(Uniform Resource Identifier)를 사용하여 리소스를 나타내고 리소스 표시 형식(예: JSON 또는 XML)을 사용하여 데이터를 전송합니다.

## 전제 조건

RESTful API 구축을 시작하기 전에 시스템에 다음을 설치해야 합니다.

- Node.js(v10.16.3 이상)
- NPM(v6.9.0 이상)
- Visual Studio Code 또는 Sublime Text와 같은 IDE 또는 텍스트 편집기

## 1단계: 프로젝트 설정

새 Node.js 프로젝트를 만들려면 터미널이나 명령 프롬프트를 열고 프로젝트를 만들 디렉터리로 이동한 후 다음 명령을 실행합니다.

```bash
mkdir my-rest-api
cd my-rest-api
npm init
```

이렇게 하면 새 Node.js 프로젝트가 생성되고 루트 디렉터리에 package.json 파일이 초기화됩니다.

## 2단계: 종속 항목 설치

RESTful API를 구축하려면 여러 종속 항목을 설치해야 합니다. 터미널에서 다음 명령을 실행하여 설치합니다.

```bash
npm install express body-parser cors --save
```

- **익스프레스** - 웹 애플리케이션 구축을 위한 일련의 기능을 제공하는 널리 사용되는 Node.js 웹 프레임워크입니다.
- **body-parser** - JSON 또는 URL 인코딩과 같은 요청 본문을 구문 분석하기 위한 미들웨어입니다.
- **cors** - API에서 교차 출처 리소스 공유(CORS)를 활성화하기 위한 미들웨어입니다.

## 3단계: 서버 생성

프로젝트의 루트 디렉터리에 `server.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');

const app = express();

app.use(cors());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

이 코드는 새로운 `express` 애플리케이션을 생성하고 `CORS`를 활성화하며 요청 본문을 구문 분석하기 위한 미들웨어를 추가합니다. 또한 서버에서 사용할 포트를 `3000` 또는 환경 변수 `PORT`에 지정된 포트로 설정합니다.

## 4단계: 경로 만들기

경로는 API의 끝점을 정의하는 데 사용됩니다. 이 단계에서는 `GET` 요청을 처리하기 위한 새 경로를 만듭니다.

프로젝트의 루트 디렉터리에 `routes.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('Hello, World!');
});

module.exports = router;
```

이 코드는 새로운 `express` 라우터를 생성하고 루트 끝점 `/`에 대한 `GET` 요청을 처리하기 위한 경로를 정의합니다. 이 끝점에 `GET` 요청이 이루어지면 서버는 `Hello, World!` 응답을 보냅니다.

## 5단계: 경로 마운트

`routes.js`에서 생성한 경로를 사용하려면 서버에 마운트해야 합니다.

`server.js` 파일에 다음 코드를 추가합니다.

```javascript
const routes = require('./routes');

app.use('/', routes);
```

이 코드는 `routes.js` 파일을 가져오고 경로를 루트 엔드포인트 `/`에 마운트합니다. 루트 엔드포인트에 대한 요청이 이루어지면 서버는 `routes.js`에 정의된 경로를 사용합니다.

## 6단계: API 테스트

API를 테스트하려면 터미널에서 다음 명령을 실행하여 서버를 시작하십시오.

```bash
node server.js
```

웹 브라우저를 열고 `http://localhost:3000`으로 이동합니다. 브라우저에 'Hello, World!' 메시지가 표시되어야 합니다.

축하해요! Node.js로 RESTful API를 성공적으로 구축했습니다.

## 결론

Node.js로 RESTful API를 구축하는 것은 간단하고 간단합니다. `express` 프레임워크와 해당 미들웨어 라이브러리 덕분에 HTTP 요청을 쉽게 처리하고 경로를 정의하고 응답을 보낼 수 있습니다. 이 문서에 설명된 단계를 따르면 이제 Node.js로 자신만의 RESTful API를 만들 수 있습니다.

## 외부 리소스

- [Express.js 공식 홈페이지](https://expressjs.com/)
- [RESTful API 설계 - 모범 사례](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)
- [NodeJS 및 ExpressJS로 간단한 RESTful API 구축](https://blog.logrocket.com/building-a-simple-restful-api-with-nodejs-and-expressjs/)