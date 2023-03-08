---
title: 068: Node.js의 데이터베이스와 TensorFlow.js 통합
description: 
published: true
date: 2023-02-02T22:43:43.548Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:43:38.864Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [068: Integrating TensorFlow.js with Databases in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/068-integrating-tensorflow-js-with-databases-in-node-js)
{.links-list}


# 068: TensorFlow.js와 Node.js의 데이터베이스 통합

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. 이 게시물에서는 Node.js의 데이터베이스에서 TensorFlow.js를 사용하는 방법을 보여드리겠습니다.

## 환경 설정

시작하기 전에 환경을 설정해야 합니다. Node.js와 TensorFlow.js Node.js API를 설치해야 합니다.

[Node.js 웹사이트](https://nodejs.org/en/)에서 Node.js를 설치할 수 있습니다.

Node.js가 설치되면 다음 명령을 사용하여 TensorFlow.js Node.js API를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

## 데이터베이스에 연결

이제 환경이 설정되었으므로 데이터베이스 작업을 시작할 수 있습니다.

[sqlite3](https://www.npmjs.com/package/sqlite3) Node.js 모듈을 사용하여 SQLite 데이터베이스에 연결하겠습니다. SQLite는 별도의 서버가 필요하지 않은 경량 데이터베이스입니다.

먼저 sqlite3 모듈을 설치해야 합니다.

```
npm install sqlite3
```

다음으로 다음 내용으로 `database.js`라는 파일을 만듭니다.

```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  db.each('SELECT * FROM items', (err, row) => {
    console.log(row.name + ': ' + row.value);
  });
});

db.close();
```

이 파일에서 우리는 `database.sqlite3`이라는 SQLite 데이터베이스에 연결하고 있습니다. 그런 다음 `items`라는 테이블을 만들고 일부 데이터를 삽입합니다.

마지막으로 데이터베이스에서 데이터를 쿼리하고 콘솔에 인쇄합니다.

이 파일을 실행하려면 다음 명령을 사용할 수 있습니다.

```
node database.js
```

## TensorFlow.js를 데이터베이스와 함께 사용하기

데이터베이스에 연결하는 방법을 살펴보았으니 이제 데이터베이스와 함께 TensorFlow.js를 사용하는 방법을 살펴보겠습니다.

이전 섹션과 동일한 `database.js` 파일을 사용합니다. 몇 줄의 코드를 추가하여 데이터베이스에서 TensorFlow.js `tf.data.Dataset`으로 데이터를 로드합니다.

```javascript
const sqlite3 = require('sqlite3').verbose();
const tf = require('@tensorflow/tfjs-node');

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  const dataset = tf.data.Dataset.fromSqlQuery('SELECT * FROM items', db, (err, row) => {
    return {
      name: row.name,
      value: row.value
    };
  });

  // print the data
  dataset.forEachAsync(item => {
    console.log(item.name + ': ' + item.value);
  });
});

db.close();
```

이 파일에서는 `tf.data.Dataset.fromSqlQuery()` 함수를 사용하여 데이터베이스에서 `tf.data.Dataset`으로 데이터를 로드합니다. 그런 다음 데이터를 콘솔에 인쇄합니다.

이 파일을 실행하려면 다음 명령을 사용할 수 있습니다.

```
node database.js
```

## 요약

이 게시물에서는 Node.js에서 데이터베이스와 함께 TensorFlow.js를 사용하는 방법을 살펴보았습니다. 데이터베이스에 연결하는 방법과 TensorFlow.js를 사용하여 데이터베이스에서 데이터를 로드하는 방법을 살펴보았습니다.