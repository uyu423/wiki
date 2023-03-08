---
title: Express.js 및 TypeScript로 CRUD 애플리케이션 개발
description: 
published: true
date: 2023-01-31T02:57:44.940Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:57:43.273Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Developing CRUD Applications with Express.js and TypeScript***English** version of this document is available*](/en/Knowledge-base/TypeScript/developing-crud-applications-with-express-js-and-typescript)
{.links-list}


# Express.js 및 TypeScript로 CRUD 애플리케이션 개발

가장 일반적인 유형의 웹 애플리케이션은 CRUD 애플리케이션입니다. CRUD는 생성, 읽기, 업데이트, 삭제를 의미합니다. CRUD 애플리케이션은 데이터를 관리하는 데 사용됩니다. 이 기사에서는 Express.js 및 TypeScript를 사용하여 CRUD 애플리케이션을 개발하는 방법에 대해 설명합니다.

## Express.js가 무엇인가요?

Express.js는 Node.js용 웹 애플리케이션 프레임워크입니다. 백엔드 개발에 사용됩니다. Express.js는 개발 프로세스를 훨씬 쉽게 만들어주는 일련의 기능을 제공합니다.

## 타입스크립트란?

TypeScript는 JavaScript의 상위 집합인 프로그래밍 언어입니다. 주로 대규모 응용 프로그램을 개발하는 데 사용됩니다. TypeScript는 유형이 지정된 언어이므로 특정 데이터 유형으로 변수를 선언할 수 있습니다. 이는 변수에 다른 데이터 유형의 값이 할당될 때 발생할 수 있는 오류를 방지하는 데 도움이 됩니다.

## CRUD 애플리케이션 개발

이 섹션에서는 Express.js 및 TypeScript를 사용하여 CRUD 애플리케이션을 개발합니다. 애플리케이션에 MongoDB 데이터베이스를 사용할 것입니다.

### 프로젝트 설정

먼저 프로젝트를 위한 새 디렉토리를 생성해야 합니다. 프로젝트 이름을 "crud-app"로 지정합니다.

```
mkdir crud-app
```

다음으로 npm을 사용하여 프로젝트를 초기화해야 합니다. "--typescript" 플래그를 사용하여 프로젝트를 TypeScript 프로젝트로 초기화합니다.

```
npm init --typescript
```

이렇게 하면 프로젝트 디렉토리에 "package.json" 파일이 생성됩니다. 이 파일에는 프로젝트에 필요한 종속성과 같은 프로젝트에 대한 정보가 포함되어 있습니다.

이제 프로젝트에 대한 종속성을 설치해야 합니다. "express" 및 "mongodb" 패키지를 사용할 것입니다.

```
npm install express mongodb
```

TypeScript 컴파일러도 설치해야 합니다. 이를 위해 "typescript" 패키지를 사용할 것입니다.

```
npm install typescript
```

마지막으로 "tsconfig.json" 파일을 만들어야 합니다. 이 파일에는 TypeScript 컴파일러에 대한 구성이 포함되어 있습니다. 이 파일에서 "target" 및 "outDir" 속성을 설정합니다. "target" 속성은 JavaScript 대상 버전을 지정합니다. "outDir" 속성은 컴파일된 JavaScript 파일이 출력될 디렉터리를 지정합니다.

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "dist"
    }
}
```

### 데이터베이스 생성

먼저 애플리케이션을 위한 데이터베이스를 생성해야 합니다. 데이터베이스 이름을 "crud_db"로 지정합니다.

다음으로 데이터베이스에 컬렉션을 만들어야 합니다. 컬렉션의 이름을 "사용자"로 지정합니다.

마지막으로 일부 데이터를 컬렉션에 삽입해야 합니다. 각 사용자에 대해 하나씩 두 개의 문서를 삽입합니다.

```json
{
    "_id": ObjectId("5f3f6a8ea864fa22a0b1d9f1"),
    "name": "John Doe",
    "age": 30,
    "email": "john.doe@example.com"
}
```

```json
{
    "_id": ObjectId("5f3f6a8ea864fa22a0b1d9f2"),
    "name": "Jane Doe",
    "age": 28,
    "email": "jane.doe@example.com"
}
```

### Express.js 서버 만들기

이제 서버용 TypeScript 파일을 만들어야 합니다. 이 파일의 이름은 "server.ts"입니다.

이 파일에서 먼저 "express" 모듈을 가져옵니다.

```javascript
import * as express from 'express';
```

다음으로 "express" 클래스의 인스턴스를 만듭니다.

```javascript
const app = express();
```

이제 경로를 설정해야 합니다. 각 CRUD 작업에 대해 하나씩 두 개의 경로를 생성합니다.

"만들기" 경로의 경우 "POST" 메서드를 사용합니다.

"읽기" 경로의 경우 "GET" 메서드를 사용합니다.

"업데이트" 경로의 경우 "PUT" 메서드를 사용합니다.

"삭제" 경로의 경우 "DELETE" 메서드를 사용합니다.

```javascript
app.post('/create', (req, res) => {
    // TODO: Implement the create route
});

app.get('/read/:id', (req, res) => {
    // TODO: Implement the read route
});

app.put('/update/:id', (req, res) => {
    // TODO: Implement the update route
});

app.delete('/delete/:id', (req, res) => {
    // TODO: Implement the delete route
});
```

마지막으로 서버를 시작해야 합니다. "listen" 방법을 사용하여 서버를 시작합니다. "포트" 속성을 "3000"으로 설정합니다.

```javascript
app.listen(3000, () => {
    console.log('Server is listening on port 3000');
});
```

### CRUD 작업 구현

이 섹션에서는 애플리케이션에 대한 CRUD 작업을 구현합니다.

#### 사용자 생성

"만들기" 경로의 경우 요청 본문에서 새 사용자에 대한 데이터를 가져와야 합니다.

다음으로 데이터를 "users" 컬렉션에 삽입합니다.

마지막으로 고객에게 응답을 보냅니다.

```javascript
app.post('/create', async (req, res) => {
    const user = req.body;
    const result = await users.insertOne(user);
    res.send(result);
});
```

#### 사용자 읽기

"읽기" 경로의 경우 요청에서 "id" 매개변수를 가져와야 합니다.

다음으로 일치하는 "id"가 있는 문서의 "users" 컬렉션을 쿼리합니다.

마지막으로 고객에게 응답을 보냅니다.

```javascript
app.get('/read/:id', async (req, res) => {
    const id = req.params.id;
    const result = await users.findOne({ "_id": ObjectId(id) });
    res.send(result);
});
```

#### 사용자 업데이트

"업데이트" 경로의 경우 요청에서 "id" 매개변수를 가져와야 합니다.

다음으로 요청 본문에서 업데이트된 사용자에 대한 데이터를 가져옵니다.

그런 다음 일치하는 "id"가 있는 문서의 "users" 컬렉션을 쿼리합니다.

마지막으로 문서를 업데이트하고 고객에게 응답을 보냅니다.

```javascript
app.put('/update/:id', async (req, res) => {
    const id = req.params.id;
    const user = req.body;
    const result = await users.findOneAndUpdate(
        { "_id": ObjectId(id) },
        { $set: user },
        { returnOriginal: false }
    );
    res.send(result);
});
```

#### 사용자 삭제

"삭제" 경로의 경우 요청에서 "id" 매개변수를 가져와야 합니다.

다음으로 일치하는 "id"가 있는 문서의 "users" 컬렉션을 쿼리합니다.

그런 다음 문서를 삭제하고 고객에게 응답을 보냅니다.

```javascript
app.delete('/delete/:id', async (req, res) => {
    const id = req.params.id;
    const result = await users.findOneAndDelete({ "_id": ObjectId(id) });
    res.send(result);
});
```

## 애플리케이션 테스트

이제 CRUD 작업을 구현했으므로 애플리케이션을 테스트해야 합니다.

TypeScript 코드를 컴파일하는 것으로 시작하겠습니다.

```
tsc
```

이렇게 하면 "dist" 디렉토리에 서버용 JavaScript 파일이 생성됩니다.

다음으로 서버를 시작해야 합니다.

```
node dist/server.js
```

이제 CRUD 작업을 테스트하기 위해 서버에 요청을 보낼 수 있습니다.

#### 사용자 생성

"만들기" 경로를 테스트하기 위해 "curl" 명령을 사용합니다.

```
curl -X POST http://localhost:3000/create -d '{"name":"John Doe","age":30,"email":"john.doe@example.com"}' -H "Content-Type: application/json"
```

이렇게 하면 새 사용자에 대한 데이터와 함께 "생성" 경로에 "POST" 요청이 전송됩니다.

#### 사용자 읽기

"읽기" 경로를 테스트하기 위해 "curl" 명령을 사용합니다.

```
curl http://localhost:3000/read/5f3f6a8ea864fa22a0b1d9f1
```

이렇게 하면 "id" 매개변수가 읽고자 하는 사용자의 "id"로 설정된 "읽기" 경로로 "GET" 요청을 보냅니다.

#### 사용자 업데이트

"업데이트" 경로를 테스트하기 위해 "curl" 명령을 사용합니다.

```
curl -X PUT http://localhost:3000/update/5f3f6a8ea864fa22a0b1d9f1 -d '{"name":"John Doe","age":31,"email":"john.doe@example.com"}' -H "Content-Type: application/json"
```

그러면 "id" 매개변수가 업데이트하려는 사용자의 "id"로 설정된 "update" 경로로 "PUT" 요청이 전송됩니다.

#### 사용자 삭제

"삭제" 경로를 테스트하기 위해 "curl" 명령을 사용합니다.

```
curl -X DELETE http://localhost:3000/delete/5f3f6a8ea864fa22a0b1d9f1
```

삭제하려는 사용자의 "id"로 설정된 "id" 매개변수를 사용하여 "삭제" 경로에 "DELETE" 요청을 보냅니다.