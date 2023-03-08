---
title: Node.js 및 NoSQL 데이터베이스: 실습 가이드
description: 
published: true
date: 2023-02-12T19:56:01.389Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:55:59.645Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js and NoSQL Databases: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-nosql-databases-a-hands-on-guide)
{.links-list}


# Node.js 및 NoSQL 데이터베이스: 실습 가이드

Node.js는 확장 가능한 네트워크 애플리케이션을 구축하는 데 사용할 수 있는 Chrome의 V8 엔진에 구축된 강력한 JavaScript 런타임입니다. NoSQL 데이터베이스는 유연성과 확장성으로 인해 점점 인기를 얻고 있으며 Node.js와 함께 사용하기에 적합합니다.

이 기사에서는 Node.js 및 NoSQL 데이터베이스 작업에 대한 실습 방식을 살펴보겠습니다. 각 기술의 기본 사항을 다룬 다음 MongoDB 데이터베이스에 데이터를 저장하는 간단한 CRUD 애플리케이션을 구축합니다.

## Node.js가 무엇인가요?

Node.js는 서버 측 애플리케이션 개발을 위한 오픈 소스 크로스 플랫폼 런타임 환경입니다. Node.js 애플리케이션은 JavaScript로 작성되며 OS X, Microsoft Windows 및 Linux의 Node.js 런타임 내에서 실행할 수 있습니다.

 Node.js는 이벤트 기반 아키텍처와 비차단 I/O API를 제공하여 가볍고 효율적입니다. Node.js 애플리케이션은 단일 CPU 코어를 사용하여 단일 스레드에서 실행할 수 있습니다.

## NoSQL이란?

NoSQL은 몇 가지 주요 방식에서 기존의 관계형 데이터베이스와 다른 데이터베이스 관리 시스템 클래스를 설명하는 데 사용되는 용어입니다.

NoSQL 데이터베이스는 많은 상용 서버에 분산될 수 있는 대량의 데이터를 처리하도록 설계되었기 때문에 관계형 데이터베이스보다 확장성이 뛰어난 경우가 많습니다. NoSQL 데이터베이스는 엄격한 스키마가 필요하지 않기 때문에 종종 관계형 데이터베이스보다 더 유연합니다.

## Node.js와 NoSQL

Node.js 및 NoSQL 데이터베이스는 모두 대량의 데이터를 처리하도록 설계되었으며 수평 확장이 가능하므로 자연스럽게 적합합니다. 또한 NoSQL 데이터베이스의 유연한 스키마는 JavaScript 개체에 더 자연스러운 형식으로 데이터를 저장할 수 있음을 의미합니다.

Node.js와 함께 사용하는 가장 인기 있는 NoSQL 데이터베이스 중 하나는 MongoDB입니다. MongoDB는 JSON과 유사한 문서에 데이터를 저장하는 문서 지향 데이터베이스입니다.

## 몽고DB 설정

MongoDB는 MongoDB 웹 사이트(https://www.mongodb.com/)에서 다운로드할 수 있습니다. MongoDB가 설치되면 npm에서 mongodb-server 패키지를 설치해야 합니다.

```
$ npm install mongodb-server
```

## MongoDB 데이터베이스 생성

MongoDB는 관계형 데이터베이스의 테이블과 유사한 컬렉션에 데이터를 저장합니다. 데이터베이스는 여러 컬렉션을 포함할 수 있습니다.

새 데이터베이스를 만들려면 MongoDB 클라이언트를 사용하여 mongodb 서버에 연결한 다음 createDatabase() 메서드를 사용합니다.

```javascript
var MongoClient = require('mongodb').MongoClient;

MongoClient.connect('mongodb://localhost:27017/mydatabase', function(err, db) {
   if(err) throw err;

   db.createDatabase('mydatabase', function(err, result) {
      if(err) throw err;
      console.log('Database created!');
   });
});
```

## MongoDB 데이터베이스에 데이터 삽입

데이터는 insert() 메서드를 사용하여 MongoDB 데이터베이스에 삽입됩니다. insert() 메서드는 개체를 매개 변수로 사용하여 컬렉션에 삽입합니다.

다음 예제에서는 "users" 컬렉션에 문서를 삽입합니다.

```javascript
db.collection('users').insert({
   name: 'John Doe',
   age: 40
}, function(err, result) {
   if(err) throw err;
   console.log('Document inserted!');
});
```

## MongoDB 데이터베이스 쿼리

데이터는 find() 메서드를 사용하여 MongoDB 데이터베이스에서 쿼리됩니다. find() 메서드는 쿼리 개체를 매개 변수로 사용하고 쿼리와 일치하는 모든 문서를 반환합니다.

다음 예제에서는 40년 된 모든 문서에 대해 "users" 컬렉션을 쿼리합니다.

```javascript
db.collection('users').find({
   age: 40
}).toArray(function(err, docs) {
   if(err) throw err;
   console.log(docs);
});
```

## MongoDB 데이터베이스에서 데이터 업데이트

데이터는 update() 메서드를 사용하여 MongoDB 데이터베이스에서 업데이트됩니다. update() 메서드는 쿼리 개체와 업데이트 개체를 매개 변수로 사용합니다. 업데이트 개체에는 업데이트해야 하는 필드와 새 값이 포함되어 있습니다.

다음 예에서는 _id가 1인 사용자 이름을 "Jane Doe"로 업데이트합니다.

```javascript
db.collection('users').update({
   _id: 1
}, {
   $set: {
      name: 'Jane Doe'
   }
}, function(err, result) {
   if(err) throw err;
   console.log('Document updated!');
});
```

## MongoDB 데이터베이스에서 데이터 삭제

데이터는 remove() 메서드를 사용하여 MongoDB 데이터베이스에서 삭제됩니다. remove() 메서드는 쿼리 개체를 매개 변수로 사용하고 쿼리와 일치하는 모든 문서를 삭제합니다.

다음 예에서는 _id가 1인 사용자를 삭제합니다.

```javascript
db.collection('users').remove({
   _id: 1
}, function(err, result) {
   if(err) throw err;
   console.log('Document deleted!');
});
```

## Node.js와 MongoDB로 CRUD 애플리케이션 구축

이제 Node.js와 MongoDB의 기본 사항을 다루었으므로 간단한 CRUD 애플리케이션을 빌드하여 배운 내용을 실습해 보겠습니다.

애플리케이션을 통해 사용자는 MongoDB 데이터베이스에서 문서를 생성, 읽기, 업데이트 및 삭제할 수 있습니다.

### 프로젝트 설정

프로젝트의 새 디렉터리를 만들고 npm으로 초기화합니다.

```
$ mkdir nodejs-mongodb-crud
$ cd nodejs-mongodb-crud
$ npm init
```

npm에서 다음 종속 항목을 설치합니다.

```
$ npm install express body-parser mongodb
```

### 서버 생성

server.js라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
var express = require('express');
var bodyParser = require('body-parser');
var MongoClient = require('mongodb').MongoClient;

var app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

var db;

MongoClient.connect('mongodb://localhost:27017/crud', function(err, database) {
   if(err) throw err;
   db = database;
   app.listen(3000, function() {
      console.log('Listening on port 3000');
   });
});
```

위의 코드는 Express 서버를 생성하고 JSON 및 URL 인코딩 데이터를 구문 분석하도록 body-parser 미들웨어를 구성합니다. 또한 MongoDB 데이터베이스에 연결하고 데이터베이스 개체를 db 변수에 저장합니다. 마지막으로 포트 3000에서 서버를 시작합니다.

### 경로 만들기

route.js라는 새 파일을 만들고 다음 코드를 추가합니다.

```javascript
module.exports = function(app, db) {
   app.post('/users', function(req, res) {
      db.collection('users').insert(req.body, function(err, result) {
         if (err) { 
            res.send({ 'error': 'An error has occurred' }); 
         } else {
            res.send(result.ops[0]);
         }
      });
   });
};
```

위의 코드는 문서를 "users" 컬렉션에 삽입하는 POST /users 경로를 정의합니다. 문서는 요청 본문에서 가져옵니다. 삽입에 성공하면 새 문서가 응답으로 반환됩니다.

다음 코드를 server.js 파일 끝에 추가하여 경로를 로드합니다.

```javascript
require('./routes')(app, db);
```

### 애플리케이션 테스트

MongoDB 서버와 Node.js 서버를 시작합니다.

```
$ mongod
$ node server.js
```

/users 경로에 POST 요청을 전송하여 애플리케이션을 테스트합니다. 이를 위해 curl 또는 Postman을 사용할 수 있습니다.

```
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "John Doe", "age": 40}' http://localhost:3000/users
```

다음 응답이 표시되어야 합니다.

```json
{"name": "John Doe", "age": 40, "_id": "58c0eb9e4a6e4a1c9c5e4a82"}
```

데이터베이스를 쿼리하여 문서가 삽입되었는지 확인할 수도 있습니다.

```
$ mongo
> use crud
> db.users.find()
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
```

### 경로 업데이트

다음 코드를 사용하여 route.js 파일을 업데이트합니다.

```javascript
app.get('/users', function(req, res) {
   db.collection('users').find().toArray(function(err, docs) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(docs);
      }
   });
});

app.get('/users/:id', function(req, res) {
   var id = req.params.id;
   db.collection('users').findOne({ '_id': new ObjectID(id) }, function(err, doc) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(doc);
      }
   });
});

app.put('/users/:id', function(req, res) {
   var id = req.params.id;
   var user = req.body;
   db.collection('users').update({ '_id': new ObjectID(id) }, user, function(err, result) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(user);
      }
   });
});

app.delete('/users/:id', function(req, res) {
   var id = req.params.id;
   db.collection('users').remove({ '_id': new ObjectID(id) }, function(err, result) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(req.body);
      }
   });
});
```

위의 코드는 다음 경로를 정의합니다.

* GET /users - "users" 컬렉션의 모든 문서를 반환합니다.
* GET /users/:id - 지정된 ID를 가진 문서를 반환합니다.
* PUT /users/:id - 지정된 ID로 문서를 업데이트합니다.
* DELETE /users/:id - 지정된 ID를 가진 문서를 삭제합니다.

### 경로 테스트

다음 요청을 서버에 전송하여 경로를 테스트하십시오.

```
$ curl http://localhost:3000/users
$ curl http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X PUT -H "Content-Type: application/json" -d '{"name": "Jane Doe", "age": 30}' http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X DELETE http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
```

다음 응답이 표시되어야 합니다.

```json
[{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}]
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
{"name": "Jane Doe", "age": 30}
{"name": "Jane Doe", "age": 30}
```

## 결론

이 기사에서는 Node.js 및 NoSQL 데이터베이스 작업에 대한 실습 접근 방식을 취했습니다. 각 기술의 기본 사항을 다룬 다음 MongoDB 데이터베이스에 데이터를 저장하는 간단한 CRUD 애플리케이션을 구축했습니다.

Node.js, MongoDB 또는 NoSQL 데이터베이스에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

* [Node.js](https://nodejs.org/)
* [몽고DB](https://www.mongodb.com/)
* [NoSQL](https://en.wikipedia.org/wiki/NoSQL)