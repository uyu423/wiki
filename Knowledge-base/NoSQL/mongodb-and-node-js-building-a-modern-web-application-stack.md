---
title: MongoDB 및 Node.js: 최신 웹 애플리케이션 스택 구축
description: 
published: true
date: 2023-03-04T13:32:45.751Z
tags: 
editor: markdown
dateCreated: 2023-03-04T13:32:44.338Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB and Node.js: Building a Modern Web Application Stack***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-and-node-js-building-a-modern-web-application-stack)
{.links-list}


MongoDB 및 Node.js: 최신 웹 애플리케이션 스택 구축

최신 웹 애플리케이션은 데이터베이스, 프런트 엔드 프레임워크 및 백엔드 언어와 같은 다양한 기술을 사용하여 구축됩니다. 이 기사에서는 MongoDB 및 Node.js를 사용하여 최신 웹 애플리케이션 스택을 구축하는 방법을 살펴봅니다.

## 몽고DB란?

MongoDB는 BSON(Binary JSON)이라는 유연한 반구조화된 문서 형식으로 데이터를 저장하는 오픈 소스 NoSQL 문서 기반 데이터베이스입니다. MongoDB는 수평 확장이 가능하도록 설계되어 고가용성과 자동 샤딩을 제공합니다. 유연성, 확장성 및 사용 용이성으로 인해 최신 웹 애플리케이션에서 널리 사용됩니다.

## Node.js가 무엇인가요?

Node.js는 브라우저 외부에서 JavaScript 코드를 실행하는 오픈 소스 크로스 플랫폼 JavaScript 런타임 환경입니다. Node.js는 Chrome의 V8 JavaScript 엔진을 기반으로 하며 가볍고 효율적이며 확장 가능한 웹 애플리케이션 구축에 이상적인 이벤트 중심의 비차단 I/O 모델을 제공합니다.

## 왜 MongoDB와 Node.js인가?

MongoDB와 Node.js는 유연성과 확장성으로 인해 최신 웹 애플리케이션을 구축하는 데 널리 사용되는 조합입니다. 대량의 데이터를 처리하고 빠른 실시간 데이터 액세스를 제공할 수 있습니다. 또한 두 기술 모두 동일한 프로그래밍 언어인 JavaScript를 공유하므로 클라이언트와 서버 측 모두에서 실행할 수 있는 코드를 쉽게 작성할 수 있습니다.

## MongoDB 및 Node.js로 최신 웹 애플리케이션 스택 구축

MongoDB 및 Node.js로 최신 웹 애플리케이션 스택을 구축하려면 애플리케이션의 문제를 분리하는 아키텍처를 만들어야 합니다. Node.js 및 MongoDB를 사용하여 백엔드 API를 만들고 React 또는 Angular와 같은 최신 JavaScript 프레임워크를 사용하여 프런트엔드를 만듭니다.

### 몽고DB 설정

MongoDB를 설정하려면 MongoDB 서버와 MongoDB Node.js 드라이버를 설치해야 합니다. 이 드라이버를 사용하면 Node.js가 MongoDB 서버에 연결하고 상호 작용할 수 있습니다.

먼저 로컬 머신이나 MongoDB Atlas와 같은 클라우드 기반 서비스에 MongoDB 서버를 설치해야 합니다. 서버를 설치한 후 npm(Node Package Manager)을 사용하여 MongoDB Node.js 드라이버를 설치할 수 있습니다.

```javascript
npm install mongodb
```

드라이버를 설치하고 나면 드라이버에서 제공하는 MongoClient 개체를 사용하여 MongoDB 서버에 연결할 수 있습니다.

```javascript
const { MongoClient } = require('mongodb');

const uri = 'mongodb+srv://<username>:<password>@<cluster-address>/test?retryWrites=true&w=majority';

const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

client.connect((err) => {
  if (err) throw err;

  const collection = client.db('test').collection('devices');

  // perform actions on the collection object
  client.close();
});
```

이제 컬렉션 개체를 사용하여 MongoDB 서버에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 수행할 수 있습니다.

### Node.js로 백엔드 API 구축

백엔드 API를 구축하려면 프런트엔드에서 사용할 RESTful 엔드포인트를 노출하는 Node.js 애플리케이션을 생성해야 합니다. Express 프레임워크를 사용하여 API와 MongoDB Node.js 드라이버를 생성하여 데이터베이스와 상호 작용할 것입니다.

먼저 프로젝트 폴더를 생성하고 npm으로 초기화해야 합니다.

```javascript
mkdir myapp
cd myapp
npm init
```

다음으로 필요한 종속 항목을 설치해야 합니다.

```javascript
npm install express mongodb body-parser
```

이제 API 끝점을 정의하고 MongoDB 서버에 연결할 server.js 파일을 만들 수 있습니다.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const { MongoClient } = require('mongodb');

const app = express();
const port = process.env.PORT || 3000;

const uri = 'mongodb+srv://<username>:<password>@<cluster-address>/test?retryWrites=true&w=majority';

const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

app.use(bodyParser.json());

app.get('/devices', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');

    collection.find().toArray((err, result) => {
      if (err) throw err;

      res.send(result);
    });
  });
});

app.post('/devices', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');

    collection.insertOne(req.body, (err, result) => {
      if (err) throw err;

      res.send(result.ops);
    });
  });
});

app.put('/devices/:id', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');
    const id = req.params.id;

    collection.updateOne({ _id: id }, { $set: req.body }, (err, result) => {
      if (err) throw err;

      res.send(result);
    });
  });
});

app.delete('/devices/:id', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');
    const id = req.params.id;

    collection.deleteOne({ _id: id }, (err, result) => {
      if (err) throw err;

      res.send(result);
    });
  });
});

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

이제 Postman과 같은 도구를 사용하여 서버를 시작하고 API 끝점을 테스트할 수 있습니다.

```javascript
npm start
```

### React로 프런트엔드 구축

프런트엔드를 구축하기 위해 사용자 인터페이스 구축에 널리 사용되는 JavaScript 라이브러리인 React를 사용할 것입니다. React를 사용하면 재사용 가능한 UI 구성 요소를 만들고 예측 가능한 방식으로 애플리케이션의 상태를 관리할 수 있습니다.

먼저 create-react-app 도구를 사용하여 React 프로젝트를 생성해야 합니다.

```javascript
npx create-react-app my-app
cd my-app
npm start
```

다음으로 백엔드 API에서 가져온 장치 목록을 표시하는 장치 구성 요소를 만들 수 있습니다.

```javascript
import React, { useState, useEffect } from 'react';

function Devices() {
  const [devices, setDevices] = useState([]);

  useEffect(() => {
    fetch('/devices')
      .then(response => response.json())
      .then(data => setDevices(data));
  }, []);

  return (
    <ul>
      {devices.map(device => (
        <li key={device._id}>{device.name}</li>
      ))}
    </ul>
  );
}

export default Devices;
```

이제 앱 구성 요소에서 장치 구성 요소를 사용할 수 있습니다.

```javascript
import React from 'react';
import Devices from './Devices';

function App() {
  return (
    <div>
      <h1>Devices</h1>
      <Devices />
    </div>
  );
}

export default App;
```

이제 프런트엔드를 시작하고 브라우저에서 애플리케이션을 테스트할 수 있습니다.

```javascript
npm start
```

## 결론

이 기사에서는 MongoDB 및 Node.js를 사용하여 최신 웹 애플리케이션 스택을 구축하는 방법을 살펴보았습니다. MongoDB를 설정하고 MongoDB Node.js 드라이버를 사용하여 연결하는 방법을 배웠습니다. 또한 Node.js와 Express를 사용하여 백엔드 API를 구축하고 React를 사용하여 프런트엔드를 구축했습니다.

이 스택은 유연성, 확장성 및 사용 편의성을 제공하므로 최신 웹 애플리케이션 구축에 탁월한 선택입니다.

## 외부 리소스

- [MongoDB 문서](https://docs.mongodb.com/)
- [Node.js 문서](https://nodejs.org/en/docs/)
- [Express 문서](https://expressjs.com/en/api.html)
- [React 문서](https://reactjs.org/docs/)