---
title: Express.js로 REST API 구축
description: 
published: true
date: 2023-02-06T13:55:51.759Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:55:50.123Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building REST APIs with Express.js***English** document is available*](/en/Knowledge-base/Backend/building-rest-apis-with-express-js)
{.links-list}


# Express.js로 REST API 구축

Node.js로 REST API를 구축하려는 경우 널리 사용되는 Express.js 프레임워크를 사용하고 싶을 것입니다. 이 기사에서는 Express.js를 사용하여 기본 REST API를 빌드하는 방법을 보여줍니다.

## REST API란?

시작하기 전에 먼저 REST API가 무엇인지 간단히 살펴보겠습니다. REST(Representational State Transfer)는 웹 서비스를 구축하기 위한 아키텍처 스타일입니다. REST API는 일반적으로 URL로 식별되는 리소스에서 수행할 수 있는 일련의 작업을 정의합니다.

예를 들어 블로그가 있는 경우 모든 블로그 게시물을 나타내는 `/posts` 리소스가 있을 수 있으며 각 게시물에는 고유한 URL이 있습니다. 새 게시물을 만들려면 `/posts` 리소스에 `POST`해야 합니다. 특정 게시물을 보려면 게시물의 URL을 `GET`해야 합니다. 게시물을 업데이트하려면 게시물의 URL에 `PUT`하고 게시물을 삭제하려면 게시물의 URL을 `DELETE`합니다.

이는 가장 일반적인 작업 중 일부에 불과하지만 리소스에서 수행할 수 있는 작업이 더 많습니다.

## Express.js 설정

이제 REST API가 무엇인지 알았으니 Express.js 설정을 시작하겠습니다. 가장 먼저 해야 할 일은 Express.js 프레임워크를 설치하는 것입니다. NPM(노드 패키지 관리자)을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install express
```

Express.js가 설치되면 새 `app.js` 파일을 만들고 Express.js 모듈을 요구할 수 있습니다.

```javascript
const express = require('express');
const app = express();
```

다음으로 몇 가지 경로를 설정해야 합니다. 경로는 HTTP 메서드와 URL 패턴으로 정의됩니다. 이 예에서는 모든 게시물을 `GET`하는 경로와 새 게시물을 `POST`하는 경로를 만듭니다.

```javascript
app.get('/posts', (req, res) => {
  // Get all posts
});

app.post('/posts', (req, res) => {
  // Create a new post
});
```

또한 게시물의 `PUT` 및 `DELETE`에 대한 경로를 ID로 정의할 수 있습니다.

```javascript
app.put('/posts/:id', (req, res) => {
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  // Delete a post
});
```

`PUT` 및 `DELETE` 경로에서 업데이트하거나 삭제하려는 게시물의 ID를 나타내는 URL 매개변수 `:id`를 사용하고 있습니다. `req.params` 개체를 사용하여 경로 처리기 함수에서 이 ID에 액세스할 수 있습니다.

```javascript
app.put('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Delete a post
});
```

이제 경로를 정의했으므로 Express.js 서버를 시작해야 합니다. `app.listen` 메서드를 호출하고 포트 번호를 전달하여 이를 수행할 수 있습니다. 또한 `console.log` 문을 추가하여 서버가 실행 중인지 알 수 있습니다.

```javascript
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

## API 테스트

이제 서버가 가동되어 실행 중이므로 API를 테스트해 보겠습니다. Postman과 같은 도구를 사용하여 API에 HTTP 요청을 할 수 있습니다.

먼저 모든 게시물을 `GET`합시다. 아직 게시물을 추가하지 않았기 때문에 빈 배열이 응답으로 표시되어야 합니다.

![모든 게시물 가져오기](https://i.imgur.com/VmYbU7D.png)

다음으로 새 게시물을 `POST`해 봅시다. `Content-Type` 헤더를 `application/json`으로 설정하고 게시물의 `title` 및 `body`와 함께 JSON 본문을 전달해야 합니다.

![새 게시물 게시](https://i.imgur.com/WBY4KdI.png)

모든 게시물을 다시 'GET'하면 응답에서 새 게시물을 볼 수 있습니다.

![새 게시물이 포함된 모든 게시물 가져오기](https://i.imgur.com/YB7qAFs.png)

마지막으로 게시물에 대한 업데이트를 `PUT`하고 `DELETE`합시다. `Content-Type` 헤더를 `application/json`으로 다시 설정하고 URL에서 게시물의 `id`를 전달해야 합니다. 업데이트를 위해 게시물의 `제목`만 변경하겠습니다.

![게시물에 업데이트 넣기](https://i.imgur.com/YB7qAFs.png)

게시물을 다시 `GET`하면 업데이트된 `제목`이 표시됩니다.

![업데이트된 제목으로 게시물 가져오기](https://i.imgur.com/VmYbU7D.png)

이제 게시물을 `DELETE`합시다.

![게시물 삭제](https://i.imgur.com/VmYbU7D.png)

모든 게시물을 다시 `GET`하면 게시물이 삭제된 것을 볼 수 있습니다.

![게시물이 삭제된 모든 게시물 가져오기](https://i.imgur.com/VmYbU7D.png)

그리고 그게 다야! 이제 Express.js를 사용하여 기본 REST API를 성공적으로 빌드했습니다.

## 외부 리소스

- [REST API 튜토리얼](https://www.restapitutorial.com/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)