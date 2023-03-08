---
title: Node.js 및 Express로 RESTful API 구축
description: 
published: true
date: 2023-03-05T22:32:34.111Z
tags: 
editor: markdown
dateCreated: 2023-03-05T22:32:32.711Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building RESTful APIs with Node.js and Express***English** document is available*](/en/Knowledge-base/Common/building-restful-apis-with-node-js-and-express)
{.links-list}

Node.js 및 Express로 RESTful API 구축

RESTful API는 웹 애플리케이션 개발의 필수 요소가 되었습니다. 웹 애플리케이션에 대한 수요가 증가함에 따라 확장 가능하고 모듈식이며 안전한 API를 구축해야 하는 필요성이 필수적이 되었습니다. Node.js 및 Express는 RESTful API를 구축하기 위한 가장 인기 있는 선택 중 하나입니다. Node.js는 오픈 소스 서버 환경인 반면 Express는 API를 쉽게 구축할 수 있게 해주는 널리 사용되는 Node.js 웹 프레임워크입니다. 이 기사에서는 Node.js 및 Express를 사용하여 RESTful API를 빌드하는 방법을 살펴봅니다.

## RESTful API란 무엇인가요?

REST는 Representational State Transfer의 약자입니다. 분산 시스템을 설계하는 데 사용되는 소프트웨어 아키텍처 스타일입니다. RESTful API는 REST 아키텍처 스타일을 따르는 API입니다. GET, POST, PUT 및 DELETE와 같은 HTTP 메서드를 통해 액세스할 수 있는 리소스 모음입니다.

## Node.js 및 Express 시작하기

Node.js 및 Express로 RESTful API 구축을 시작하기 전에 개발 환경을 설정해야 합니다. 시작하는 단계는 다음과 같습니다.

1. Node.js 설치: 공식 웹사이트에서 Node.js를 다운로드하여 설치합니다.

2. 새 Node.js 프로젝트 만들기: 터미널을 열고 프로젝트의 새 디렉터리를 만듭니다. 프로젝트 디렉터리로 이동하여 다음 명령을 실행합니다.

```
$ npm init
```

이렇게 하면 프로젝트 디렉토리에 `package.json` 파일이 생성됩니다.

3. Express 설치: 다음 명령을 실행하여 Express를 설치합니다.

```
$ npm install express
```

## 간단한 RESTful API 구축

이제 개발 환경을 설정했으므로 간단한 RESTful API를 빌드해 보겠습니다. 사용자를 만들고, 읽고, 업데이트하고, 삭제할 수 있는 API를 만들 것입니다.

### 서버 생성

먼저 들어오는 요청을 수신 대기하는 서버를 만듭니다. 프로젝트 디렉터리에 `server.js`라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const app = express();

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

여기서는 Express 모듈을 가져오고 새 Express 애플리케이션을 만들었습니다. 또한 포트 3000에서 들어오는 요청을 수신하도록 서버를 설정했습니다.

### 끝점 만들기

이제 API용 엔드포인트를 생성해 보겠습니다. 사용자 생성, 읽기, 업데이트 및 삭제를 위한 엔드포인트를 생성합니다.

```javascript
const users = [];

// Create a user
app.post('/users', (req, res) => {
  const user = req.body;
  users.push(user);
  res.send('User has been added to the database');
});

// Read all users
app.get('/users', (req, res) => {
  res.send(users);
});

// Read a single user
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  const user = users.find(user => user.id === userId);
  res.send(user);
});

// Update a user
app.put('/users/:id', (req, res) => {
  const userId = req.params.id;
  const updatedUser = req.body;
  const index = users.findIndex(user => user.id === userId);
  users[index] = updatedUser;
  res.send('User has been updated');
});

// Delete a user
app.delete('/users/:id', (req, res) => {
  const userId = req.params.id;
  const index = users.findIndex(user => user.id === userId);
  users.splice(index, 1);
  res.send('User has been deleted');
});
```

여기에서 사용자 생성, 읽기, 업데이트 및 삭제를 위한 끝점을 만들었습니다. `app.post()` 메소드는 사용자를 생성하는 데 사용되며 `app.get()` 메소드는 모든 사용자와 단일 사용자를 읽는 데 사용되며 `app.put()` 메소드는 사용자를 업데이트하는 데 사용됩니다. 사용자이며 `app.delete()` 메서드는 사용자를 삭제하는 데 사용됩니다.

### API 테스트

이제 끝점을 만들었으므로 API를 테스트해 보겠습니다. 다음 명령을 실행하여 서버를 시작합니다.

```
$ node server.js
```

Postman과 같은 도구를 사용하여 API를 테스트합니다. 사용자 데이터가 포함된 JSON 페이로드와 함께 `http://localhost:3000/users`에 POST 요청을 보냅니다. GET, PUT 및 DELETE 요청을 사용하여 사용자를 읽고, 업데이트하고, 삭제합니다.

## 결론

이 기사에서는 Node.js 및 Express를 사용하여 RESTful API를 빌드하는 방법을 살펴보았습니다. 우리는 개발 환경을 설정하는 방법과 사용자를 만들고, 읽고, 업데이트하고, 삭제할 수 있는 간단한 API를 만드는 방법을 배웠습니다. Node.js 및 Express로 RESTful API를 구축하면 확장 가능하고 모듈식이며 안전한 웹 애플리케이션을 구축하기 위한 강력한 도구가 될 수 있습니다.

## 외부 리소스

- [Node.js 공식 홈페이지](https://nodejs.org/en/)
- [익스프레스 공식 홈페이지](https://expressjs.com/)
- TutorialsPoint의 [Node.js 및 Express를 사용한 RESTful API 자습서](https://www.tutorialspoint.com/nodejs/nodejs_restful_api.htm)
- Scotch.io의 [Node 및 Express 4를 사용하여 RESTful API 구축](https://scotch.io/tutorials/build-a-restful-api-using-node-and-express-4).