---
title: Node.js 및 MongoDB: 데이터 지속성에 대한 실습 가이드
description: 
published: true
date: 2023-01-31T06:43:49.316Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:43:45.846Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Node.js and MongoDB: A Hands-On Guide to Data Persistence***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-mongodb-a-hands-on-guide-to-data-persistence)
{.links-list}



# Node.js 및 MongoDB: 데이터 지속성에 대한 실습 가이드

이 기사에서는 Node.js와 MongoDB를 사용하여 데이터를 유지하는 방법을 살펴보겠습니다. MongoDB 데이터베이스 설정, 데이터베이스와 상호 작용하는 Node.js 애플리케이션 만들기, CRUD 작업을 사용하여 데이터 조작에 대한 기본 사항을 다룹니다. 이 기사를 마치면 Node.js와 MongoDB를 사용하여 확장 가능한 데이터 기반 애플리케이션을 만드는 방법을 확실하게 이해할 수 있습니다.

## 몽고DB 설정

MongoDB는 강력한 문서 지향 데이터베이스 시스템입니다. 모든 크기와 복잡성의 데이터로 쉽게 작업할 수 있도록 하는 풍부한 쿼리 언어와 인덱싱 기능이 있습니다.

MongoDB를 시작하려면 먼저 [MongoDB 커뮤니티 서버를 설치](https://www.mongodb.com/download-center/community)해야 합니다. MongoDB는 Windows, macOS 및 Linux에서 사용할 수 있습니다.

MongoDB가 설치되면 `mongod` 명령으로 MongoDB 데몬을 시작할 수 있습니다. 이렇게 하면 MongoDB 서버가 시작되고 데이터베이스 파일을 저장할 `data` 디렉토리가 생성됩니다.

다음으로 MongoDB 서버에 대한 구성 파일을 만들어야 합니다. 이 파일은 일반적으로 `mongod.conf`라는 이름을 가지며 MongoDB가 설치된 `bin` 디렉토리에 있습니다. 다음은 시작하는 데 사용할 수 있는 기본 구성 파일입니다.

```
storage:
  dbPath: /data/db
  journal:
    enabled: true
```

이 파일은 MongoDB에게 데이터베이스 파일(이 경우 `/data/db` 디렉토리)을 저장할 위치를 알려주고 데이터베이스에 대한 충돌 복구를 제공하는 기능인 저널링을 활성화합니다.

이제 MongoDB 서버가 실행 중이므로 `mongo` 셸을 사용하여 연결할 수 있습니다. 이렇게 하면 데이터베이스와 상호 작용하기 위한 JavaScript 인터페이스가 제공됩니다.

## Node.js 애플리케이션 만들기

이제 MongoDB를 실행하고 있으므로 데이터베이스와 상호 작용할 수 있는 Node.js 애플리케이션을 만들어 보겠습니다. 프로젝트의 기본 디렉토리 구조를 만드는 것부터 시작하겠습니다.

```
node-mongo
├── config
│   └── mongodb.js
├── controllers
│   └── books.js
├── models
│   └── book.js
├── routes
│   └── books.js
└── app.js
```

구성 파일은 `config` 디렉토리에, 컨트롤러 파일은 `controllers` 디렉토리에, 모델 파일은 `models` 디렉토리에, 경로 파일은 `routes` 디렉토리에 둘 것입니다.

`app.js` 파일은 애플리케이션의 진입점이 될 것입니다. 여기에서 애플리케이션을 구성하고 미들웨어를 설정합니다.

먼저 `config/mongodb.js` 파일을 생성합니다. 이 파일에는 MongoDB 구성이 포함됩니다.

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/node-mongo', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  console.log('Connected to MongoDB');
});

module.exports = db;
```

이 파일에서는 `mongoose` 라이브러리를 사용하여 MongoDB 데이터베이스에 연결합니다. 또한 데이터베이스 연결을 참조하기 위해 `db` 변수를 설정하고 있습니다. 이 `db` 변수는 이 모듈이 필요한 모든 파일에서 사용할 수 있습니다.

다음으로 `models/book.js` 파일을 생성해 보겠습니다. 이 파일에는 책 모델이 포함됩니다.

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const bookSchema = new Schema({
  title: String,
  author: String,
  year: Number,
  genre: String
});

const Book = mongoose.model('Book', bookSchema);

module.exports = Book;
```

이 모델은 데이터베이스에서 책 문서의 구조를 정의합니다. 스키마에서 모델을 생성하기 위해 `mongoose.model()` 메서드를 사용하고 있습니다. 이 모델은 데이터베이스에서 문서를 만드는 데 사용됩니다.

이제 모델을 정의했으므로 컨트롤러를 생성해 보겠습니다. 컨트롤러에는 CRUD 작업에 대한 논리가 포함됩니다. `controllers/books.js` 파일을 생성하여 시작하겠습니다.

```javascript
const Book = require('../models/book');

exports.getBooks = (req, res, next) => {
  Book.find((err, books) => {
    if (err) return next(err);
    res.json(books);
  });
};

exports.getBook = (req, res, next) => {
  Book.findById(req.params.id, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.createBook = (req, res, next) => {
  const book = new Book(req.body);
  book.save((err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.updateBook = (req, res, next) => {
  Book.findByIdAndUpdate(req.params.id, req.body, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.deleteBook = (req, res, next) => {
  Book.findByIdAndRemove(req.params.id, req.body, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};
```

이 컨트롤러는 CRUD 작업의 논리를 정의합니다. 데이터베이스에서 모든 책을 가져오는 `getBooks` 메소드, ID로 단일 책을 가져오는 `getBook` 메소드, 새 책을 만드는 `createBook` 메소드, 기존 책을 업데이트하는 `updateBook` 메소드, 책을 삭제하는 `deleteBook` 메소드.

이제 컨트롤러를 정의했으므로 경로를 생성해 보겠습니다. `routes/books.js` 파일을 생성하는 것으로 시작하겠습니다:

```javascript
const express = require('express');
const router = express.Router();
const booksCtrl = require('../controllers/books');

router.get('/books', booksCtrl.getBooks);
router.get('/books/:id', booksCtrl.getBook);
router.post('/books', booksCtrl.createBook);
router.put('/books/:id', booksCtrl.updateBook);
router.delete('/books/:id', booksCtrl.deleteBook);

module.exports = router;
```

이 파일에서는 `express.Router` 클래스를 사용하여 책 API용 라우터를 만듭니다. 그런 다음 CRUD 작업에 대한 경로를 정의하고 이를 적절한 컨트롤러 메서드에 매핑합니다.

마지막으로 `app.js` 파일을 정의합니다. 이것은 우리 애플리케이션의 진입점입니다.

```javascript
const express = require('express');
const app = express();
const booksRouter = require('./routes/books');
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/node-mongo');

app.use(express.json());
app.use('/api/v1/books', booksRouter);

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

이 파일에서는 애플리케이션에 필요한 종속성이 필요합니다. 그런 다음 `express.json()` 미들웨어를 사용하여 JSON 요청을 구문 분석합니다.

다음으로 `express.Router` 클래스를 사용하여 책 API용 라우터를 만듭니다. 그런 다음 `booksRouter`를 `/api/v1/books` 경로에 매핑합니다.

마지막으로 애플리케이션이 포트 3000에서 수신 대기하도록 합니다.

## CRUD 작업

이제 애플리케이션을 설정했으므로 CRUD 작업을 수행하는 방법을 살펴보겠습니다.

### 책 만들기

책을 만들기 위해 책 데이터를 포함하는 JSON 본문과 함께 `/api/v1/books` 끝점에 POST 요청을 보냅니다.

```javascript
{
	"title": "The Great Gatsby",
	"author": "F. Scott Fitzgerald",
	"year": 1925,
	"genre": "Novel"
}
```

### 책 검색

책을 검색하기 위해 `/api/v1/books/:id` 엔드포인트에 GET 요청을 보냅니다. 여기서 `:id`는 검색하려는 책의 ID입니다.

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

### 책 업데이트

책을 업데이트하려면 업데이트된 책 데이터가 포함된 JSON 본문과 함께 PUT 요청을 `/api/v1/books/:id` 엔드포인트로 보냅니다. 업데이트가 필요한 필드만 요청 본문에 포함하면 됩니다.

```javascript
{
	"title": "The Great Gatsby",
	"author": "F. Scott Fitzgerald",
	"year": 1926,
	"genre": "Novel"
}
```

### 책 삭제

책을 삭제하려면 `/api/v1/books/:id` 엔드포인트에 DELETE 요청을 보냅니다. 여기서 `:id`는 삭제할 책의 ID입니다.

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

## 결론

이 기사에서는 Node.js와 MongoDB를 사용하여 확장 가능한 데이터 기반 애플리케이션을 만드는 방법을 살펴보았습니다. MongoDB 설정, 데이터베이스와 상호 작용하는 Node.js 애플리케이션 생성, CRUD 작업을 사용하여 데이터 조작에 대한 기본 사항을 다뤘습니다.