---
title: Node.js 및 Express로 RESTful API 구축
description: 
published: true
date: 2023-02-07T02:19:10.984Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:19:09.181Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building RESTful APIs with Node.js and Express***English** document is available*](/en/Knowledge-base/Nodejs/building-restful-apis-with-node-js-and-express)
{.links-list}


# Node.js 및 Express로 RESTful API 구축

Node.js는 서버 측 애플리케이션을 구축하기 위한 강력한 플랫폼입니다. 이 기사에서는 Node.js 및 Express를 사용하여 RESTful API를 빌드하는 방법을 보여줍니다.

## REST API란?

REST API는 GET, PUT, POST 및 DELETE 데이터에 대한 HTTP 요청을 사용하는 애플리케이션 프로그래밍 인터페이스입니다. REST API는 서버에서 리소스에 액세스하는 데 사용할 수 있으므로 웹 또는 모바일 애플리케이션용 백엔드를 구축하기 위한 완벽한 도구입니다.

## 익스프레스를 사용하는 이유

Express는 Node.js에서 웹 애플리케이션을 구축하기 위한 인기 있는 프레임워크입니다. 가볍고 사용하기 쉬우므로 RESTful API를 구축하는 데 적합합니다.

## Node.js 및 Express로 REST API 만들기

이제 REST API가 무엇인지, 왜 Express를 사용하여 API를 만들어야 하는지 알았으니 시작하겠습니다!

우리는 사용자가 할 일 목록을 관리할 수 있는 간단한 REST API를 만들 것입니다. API에는 다음 엔드포인트가 있습니다.

- `GET /todos`: 모든 할 일 목록 가져오기
- `POST /todos`: 새로운 할 일 만들기
- `PUT /todos/:id`: 할 일 업데이트
- `DELETE /todos/:id`: 할 일 삭제

### Node.js 프로젝트 설정

새 Node.js 프로젝트를 설정하여 시작하겠습니다. [Express 생성기](https://expressjs.com/en/starter/generator.html)를 사용하여 프로젝트를 생성합니다.

먼저 Express 생성기를 전역으로 설치합니다.

```
npm install -g express-generator
```

다음으로 Express 생성기를 사용하여 새 프로젝트를 만듭니다.

```
express todo-api
```

이렇게 하면 시작하는 데 필요한 기본 파일과 디렉토리가 있는 `todo-api`라는 새 디렉토리가 생성됩니다.

다음으로 새 프로젝트 디렉터리로 변경하고 종속 항목을 설치합니다.

```
cd todo-api
npm install
```

이제 종속 항목이 설치되었으므로 개발 서버를 시작할 수 있습니다.

```
npm start
```

다음 출력이 표시되어야 합니다.

```
> todo-api@0.0.0 start /Users/<user>/<path>/todo-api
> node ./bin/www

```

이제 http://localhost:3000에서 애플리케이션에 액세스할 수 있습니다.

### To-Do 모델 정의

우리의 API는 할 일을 데이터베이스에 저장합니다. 데이터베이스에는 [MongoDB](https://www.mongodb.com/)를 사용하고 데이터베이스 라이브러리에는 [Mongoose](https://mongoosejs.com/)를 사용합니다.

먼저 몽구스를 설치합니다.

```
npm install mongoose --save
```

다음으로 `./models/Todo.js`에 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
const mongoose = require('mongoose');

const todoSchema = new mongoose.Schema({
  name: String,
  completed: Boolean
});

const Todo = mongoose.model('Todo', todoSchema);

module.exports = Todo;
```

이 코드는 `name`과 `completed`라는 두 개의 필드가 있는 `Todo` 모델을 정의합니다.

### 데이터베이스에 연결

이제 모델을 정의했으므로 데이터베이스에 연결해야 합니다. `./bin/www` 파일에서 이 작업을 수행합니다.

`./bin/www`를 열고 다음 코드를 추가합니다.

```javascript
#!/usr/bin/env node

/**
 * Module dependencies.
 */

const app = require('../app');
const debug = require('debug')('todo-api:server');
const http = require('http');

/**
 * Get port from environment and store in Express.
 */

const port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

/**
 * Create HTTP server.
 */

const server = http.createServer(app);

/**
 * Connect to MongoDB
 */

const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/todo-api');

/**
 * Listen on provided port, on all network interfaces.
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

/**
 * Normalize a port into a number, string, or false.
 */

function normalizePort(val) {
  const port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}

/**
 * Event listener for HTTP server "error" event.
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  const bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

/**
 * Event listener for HTTP server "listening" event.
 */

function onListening() {
  const addr = server.address();
  const bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}
```

이 코드는 다음을 수행합니다.

- Mongoose를 사용하여 MongoDB 데이터베이스에 연결
- 지정된 포트에서 Express 서버를 시작합니다.

### API 경로 정의

이제 모델과 데이터베이스가 설정되었으므로 API 경로 정의를 시작할 수 있습니다.

`GET /todos` 경로를 정의하는 것으로 시작하겠습니다. 이 경로는 데이터베이스의 모든 할 일 목록을 반환합니다.

`./routes/index.js`를 열고 다음 코드를 추가합니다.

```javascript
const express = require('express');
const router = express.Router();

const Todo = require('../models/Todo');

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});

/* GET all todos. */
router.get('/todos', function(req, res, next) {
  Todo.find({}, function(err, todos) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todos);
    }
  });
});

module.exports = router;
```

이 코드는 데이터베이스에서 모든 할일을 가져오기 위해 `Todo.find()` 메서드를 사용하는 `GET /todos` 경로를 정의합니다.

쿼리가 성공하면 JSON 응답에 `todos` 배열이 반환됩니다. 오류가 있는 경우 오류 메시지와 함께 '500 내부 서버 오류'가 반환됩니다.

다음으로 `POST /todos` 경로를 정의해 보겠습니다. 이 경로는 새로운 할 일을 만드는 데 사용됩니다.

`./routes/index.js`에 다음 코드를 추가합니다.

```javascript
/* POST new todo. */
router.post('/todos', function(req, res, next) {
  const todo = new Todo(req.body);
  todo.save(function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

이 코드는 `req.body` 개체에서 새 `Todo`를 생성하는 `POST /todos` 경로를 정의합니다. 'save()' 메서드는 할 일을 데이터베이스에 저장하는 데 사용됩니다.

저장에 성공하면 JSON 응답에 새 할 일이 반환됩니다. 오류가 있는 경우 오류 메시지와 함께 '500 내부 서버 오류'가 반환됩니다.

다음으로 `PUT /todos/:id` 경로를 정의해 보겠습니다. 이 경로는 기존 할 일을 업데이트하는 데 사용됩니다.

`./routes/index.js`에 다음 코드를 추가합니다.

```javascript
/* PUT update todo. */
router.put('/todos/:id', function(req, res, next) {
  const id = req.params.id;
  const todo = req.body;
  Todo.findByIdAndUpdate(id, todo, function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

이 코드는 URL에 지정된 `id`로 할 일을 업데이트하기 위해 `findByIdAndUpdate()` 메서드를 사용하는 `PUT /todos/:id` 경로를 정의합니다. `todo` 개체는 `req.body`의 데이터로 업데이트됩니다.

업데이트가 성공하면 업데이트된 할 일이 JSON 응답으로 반환됩니다. 오류가 있는 경우 오류 메시지와 함께 '500 내부 서버 오류'가 반환됩니다.

마지막으로 `DELETE /todos/:id` 경로를 정의해 보겠습니다. 이 경로는 기존 할 일을 삭제하는 데 사용됩니다.

`./routes/index.js`에 다음 코드를 추가합니다.

```javascript
/* DELETE todo. */
router.delete('/todos/:id', function(req, res, next) {
  const id = req.params.id;
  Todo.findByIdAndRemove(id, function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

이 코드는 URL에 지정된 `id`로 할 일을 삭제하기 위해 `findByIdAndRemove()` 메서드를 사용하는 `DELETE /todos/:id` 경로를 정의합니다.

삭제에 성공하면 삭제된 할 일이 JSON 응답으로 반환됩니다. 오류가 있는 경우 오류 메시지와 함께 '500 내부 서버 오류'가 반환됩니다.

### API 테스트

이제 API 경로를 정의했으므로 테스트해 보겠습니다. [Postman](https://www.getpostman.com/)을 사용하여 API를 테스트합니다.

먼저 개발 서버를 시작합니다.

```
npm start
```

그런 다음 Postman을 열고 새 요청을 만듭니다.

`GET /todos` 경로의 경우 다음 설정을 사용합니다.

- 방법: GET
- URL: http://localhost:3000/todos

![할 일 받기](https://i.imgur.com/wLwvWxH.png)

`POST /todos` 경로의 경우 다음 설정을 사용합니다.

- 방법: POST
- URL: http://localhost:3000/todos
- 몸:
  - 유형: JSON(어플리케이션/json)
  - 날것의:
    ```json
    {
      "name": "테스트 할 일",
      "완료": 거짓
    }
    ```

![할 일 만들기](https://i.imgur.com/VkzMxK0.png)

`PUT /todos/:id` 경로의 경우 다음 설정을 사용합니다.

- 방법: PUT
- URL: http://localhost:3000/todos/{id}
- 몸:
  - 유형: JSON(어플리케이션/json)
  - 날것의:
    ```json
    {
      "name": "업데이트된 할 일",
      "완료": 참
    }
    ```

![할 일 업데이트](https://i.imgur.com/pBKgVnS.png)

`DELETE /todos/:id` 경로의 경우 다음 설정을 사용합니다.

- 방법: DELETE
- URL: http://localhost:3000/todos/{id}

![할 일 삭제](https://i.imgur.com/wEwJWdl.png)

## 마무리

이 기사에서는 Node.js 및 Express를 사용하여 RESTful API를 빌드하는 방법을 보여주었습니다. 우리는 `Todo` 모델을 정의하고 `GET`, `POST`, `PUT` 및 `DELETE` 요청에 대한 경로를 생성했습니다. 또한 Postman을 사용하여 API를 테스트했습니다.

Node.js 및 Express를 사용하여 REST API를 빌드하는 방법을 살펴보았으므로 이제 이 지식을 사용하여 고유한 API를 빌드할 수 있습니다.

## 자원

- [REST API란?](https://www.mulesoft.com/resources/api/what-rest-api)
- [익스프레스](https://expressjs.com/)
- [Node.js](https://nodejs.org/en/)
- [몽고DB](https://www.mongodb.com/)
- [몽구스](https://mongoosejs.com/)
- [우체부](https://www.getpostman.com/)