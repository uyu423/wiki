---
title: 가벼운 NoSQL 데이터베이스를 위해 NeDB와 함께 TypeScript 사용
description: 
published: true
date: 2023-02-09T18:56:28.343Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:56:26.566Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript with NeDB for Lightweight NoSQL Database***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-nedb-for-lightweight-nosql-database)
{.links-list}


# 가벼운 NoSQL 데이터베이스를 위해 NeDB와 함께 TypeScript 사용

## 소개

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다. TypeScript는 Node.js 런타임 환경에서 사용할 수 있는 많은 언어 중 하나입니다.

NeDB는 Node.js와 브라우저 모두에서 사용할 수 있는 가벼운 NoSQL 데이터베이스입니다. MongoDB API를 지원하므로 기존 MongoDB 라이브러리 및 도구와 함께 쉽게 사용할 수 있습니다.

이 기사에서는 NeDB에서 TypeScript를 사용하는 방법을 보여줍니다. NeDB 데이터베이스에 데이터를 저장하는 간단한 할일 애플리케이션을 만들 것입니다.

## TypeScript 프로젝트 설정

먼저 TypeScript 프로젝트를 생성해야 합니다. [TypeScript Node Starter](https://github.com/Microsoft/TypeScript-Node-Starter) 프로젝트 템플릿을 사용하겠습니다.

```
$ git clone https://github.com/Microsoft/TypeScript-Node-Starter.git todo-app
$ cd todo-app
$ npm install
```

다음으로 NeDB 유형을 설치해야 합니다.

```
$ npm install --save-dev @types/nedb
```

## To-Do 모델 만들기

To-Do 모델을 만드는 것부터 시작하겠습니다. 다음 코드를 사용하여 `src` 디렉토리에 `todo.ts`라는 새 파일을 만듭니다.

```typescript
export class ToDo {
  _id: string;
  title: string;
  completed: boolean;
  date: Date;

  constructor(title: string) {
    this.title = title;
    this.completed = false;
    this.date = new Date();
  }
}
```

이 모델에는 `_id`, `title`, `completed` 및 `date`의 네 가지 필드가 있습니다. `_id` 필드는 기본 키이며 NeDB에서 생성됩니다. `제목` 필드는 할 일 항목의 제목입니다. 'completed' 필드는 할 일 항목이 완료되었는지 여부를 나타내는 부울입니다. '날짜' 필드는 할 일 항목이 생성된 날짜입니다.

## 할일 서비스 만들기

다음으로 To-Do 서비스를 생성합니다. 이 서비스는 To-Do 항목에 대한 CRUD 작업을 담당합니다. 다음 코드를 사용하여 `src` 디렉토리에 `todoService.ts`라는 새 파일을 만듭니다.

```typescript
import { Datastore } from 'nedb';
import { ToDo } from './todo';

export class ToDoService {
  private db: Datastore;

  constructor(db: Datastore) {
    this.db = db;
  }

  public async getAll(): Promise<ToDo[]> {
    return new Promise<ToDo[]>((resolve, reject) => {
      this.db.find({}, (err, docs: ToDo[]) => {
        if (err) {
          return reject(err);
        }
        resolve(docs);
      });
    });
  }

  public async getById(id: string): Promise<ToDo | null> {
    return new Promise<ToDo | null>((resolve, reject) => {
      this.db.findOne({ _id: id }, (err, doc: ToDo) => {
        if (err) {
          return reject(err);
        }
        resolve(doc);
      });
    });
  }

  public async create(todo: ToDo): Promise<string> {
    return new Promise<string>((resolve, reject) => {
      this.db.insert(todo, (err, doc: ToDo) => {
        if (err) {
          return reject(err);
        }
        resolve(doc._id);
      });
    });
  }

  public async update(todo: ToDo): Promise<number> {
    return new Promise<number>((resolve, reject) => {
      this.db.update({ _id: todo._id }, todo, {}, (err, numUpdated: number) => {
        if (err) {
          return reject(err);
        }
        resolve(numUpdated);
      });
    });
  }

  public async delete(id: string): Promise<number> {
    return new Promise<number>((resolve, reject) => {
      this.db.remove({ _id: id }, {}, (err, numRemoved: number) => {
        if (err) {
          return reject(err);
        }
        resolve(numRemoved);
      });
    });
  }
}
```

이 서비스에는 `getAll`, `getById`, `create`, `update` 및 `delete`의 5가지 메서드가 있습니다. 이러한 메서드는 할 일 항목에 대한 CRUD 작업에 매핑됩니다.

'getAll' 및 'getById' 메서드는 각각 할 일 항목 배열 또는 단일 할 일 항목으로 확인되는 '약속'을 반환합니다.

`create`, `update` 및 `delete` 메소드는 생성된 To-Do 항목의 `_id`, 업데이트된 To-Do 항목의 수 또는 To-Do의 수로 해석되는 `Promise`를 반환합니다. 항목을 각각 삭제했습니다.

## 할일 컨트롤러 만들기

다음으로 To-Do 컨트롤러를 만듭니다. 이 컨트롤러는 HTTP 요청 처리를 담당합니다. 다음 코드를 사용하여 `src` 디렉토리에 `todoController.ts`라는 새 파일을 만듭니다.

```typescript
import { Request, Response } from 'express';
import { ToDoService } from './todoService';
import { ToDo } from './todo';

export class ToDoController {
  private todoService: ToDoService;

  constructor(todoService: ToDoService) {
    this.todoService = todoService;
  }

  public async getAll(req: Request, res: Response) {
    try {
      const todos = await this.todoService.getAll();
      res.json(todos);
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async getById(req: Request, res: Response) {
    const id = req.params.id;
    try {
      const todo = await this.todoService.getById(id);
      if (todo) {
        res.json(todo);
      } else {
        res.sendStatus(404);
      }
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async create(req: Request, res: Response) {
    const todo = req.body as ToDo;
    try {
      const id = await this.todoService.create(todo);
      res.json({ id: id });
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async update(req: Request, res: Response) {
    const todo = req.body as ToDo;
    if (!todo._id) {
      return res.status(400).send('To-Do item must have an _id');
    }
    try {
      const numUpdated = await this.todoService.update(todo);
      res.json({ numUpdated: numUpdated });
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async delete(req: Request, res: Response) {
    const id = req.params.id;
    try {
      const numDeleted = await this.todoService.delete(id);
      res.json({ numDeleted: numDeleted });
    } catch (err) {
      res.status(500).send(err);
    }
  }
}
```

이 컨트롤러에는 `getAll`, `getById`, `create`, `update` 및 `delete`의 다섯 가지 메서드가 있습니다. 이러한 메서드는 각각 HTTP 메서드 `GET`, `GET`/`:id`, `POST`, `PUT` 및 `DELETE`에 매핑됩니다.

`getAll` 및 `getById` 메서드는 각각 할일 항목의 배열 또는 단일 할일 항목을 반환합니다.

`create`, `update` 및 `delete` 메소드는 각각 생성된 할일 항목의 `_id`, 업데이트된 할일 항목 수 또는 삭제된 할일 항목 수를 반환합니다.

## 익스프레스 서버 생성

다음으로 [Express](https://expressjs.com/) 서버를 생성합니다. Express는 Node.js용 웹 애플리케이션 프레임워크입니다.

다음 코드를 사용하여 `src` 디렉토리에 `server.ts`라는 새 파일을 만듭니다.

```typescript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import { ToDoController } from './todoController';
import { Datastore } from 'nedb';

const app = express();
const PORT = 3000;

const db = new Datastore('todo.db');
db.loadDatabase();

const todoService = new ToDoService(db);
const todoController = new ToDoController(todoService);

app.use(bodyParser.json());

app.get('/todos', todoController.getAll);
app.get('/todos/:id', todoController.getById);
app.post('/todos', todoController.create);
app.put('/todos', todoController.update);
app.delete('/todos/:id', todoController.delete);

app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
```

이 서버는 `todo.db`라는 NeDB 데이터베이스를 생성하고 로드합니다. 그런 다음 To-Do 서비스와 To-Do 컨트롤러를 생성합니다.

서버는 [body-parser](https://www.npmjs.com/package/body-parser) 미들웨어를 사용하여 JSON 본문을 구문 분석하도록 Express를 구성합니다.

서버는 To-Do 컨트롤러의 메서드에 대한 경로를 정의합니다. `app.get` 경로는 `GET` 메서드에 매핑됩니다. `app.get`/`:id` 경로는 경로 매개변수를 사용하여 `GET` 메서드에 매핑됩니다. `app.post` 경로는 `POST` 메서드에 매핑됩니다. `app.put` 경로는 `PUT` 메서드에 매핑됩니다. `app.delete` 경로는 `DELETE` 메서드에 매핑됩니다.

마지막으로 서버는 포트 3000에서 수신을 시작합니다.

## To-Do API 테스트

[cURL](https://curl.haxx.se/)을 사용하여 To-Do API를 테스트할 수 있습니다.

먼저 서버를 시작합니다.

```
$ npm start

> todo-app@1.0.0 start /Users/username/projects/todo-app
> ts-node src/server.ts

Server listening on port 3000
```

다음으로 cURL을 사용하여 To-Do 항목을 만듭니다.

```
$ curl -X POST -H "Content-Type: application/json" -d '{"title": "Buy milk"}' http://localhost:3000/todos
```

이 cURL 명령은 JSON 본문과 함께 `/todos` 엔드포인트에 `POST` 요청을 보냅니다. JSON 본문에는 제목이 `우유 구입`인 할 일 항목이 포함되어 있습니다.

다음과 같은 응답을 받아야 합니다.

```json
{"id": "5e1d280b04a7a22a68e0e7cd"}
```

이것은 우리가 생성한 To-Do 항목의 `_id`입니다. 이 `_id`를 사용하여 To-Do 항목을 검색할 수 있습니다.

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

다음과 같은 응답을 받아야 합니다.

```json
{"_id":"5e1d280b04a7a22a68e0e7cd","title":"Buy milk","completed":false,"date":"2020-01-08T05:34:51.596Z"}
```

이것은 우리가 만든 To-Do 항목입니다. `completed` 필드가 `false`이고 `date` 필드가 항목을 생성한 날짜임을 알 수 있습니다.

다음으로 To-Do 항목을 업데이트합니다.

```
$ curl -X PUT -H "Content-Type: application/json" -d '{"_id": "5e1d280b04a7a22a68e0e7cd", "title": "Buy eggs", "completed": true}' http://localhost:3000/todos
```

이 cURL 명령은 JSON 본문과 함께 `/todos` 엔드포인트에 `PUT` 요청을 보냅니다. JSON 본문에는 업데이트된 To-Do 항목이 포함되어 있습니다. 제목을 'Buy eggs'로 변경하고 'completed' 필드를 'true'로 설정했습니다.

다음과 같은 응답을 받아야 합니다.

```json
{"numUpdated": 1}
```

업데이트된 To-Do 항목의 수입니다. 업데이트된 To-Do 항목을 검색하여 업데이트되었는지 확인할 수 있습니다.

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

다음과 같은 응답을 받아야 합니다.

```json
{"_id":"5e1d280b04a7a22a68e0e7cd","title":"Buy eggs","completed":true,"date":"2020-01-08T05:34:51.596Z"}
```

마지막으로 To-Do 항목을 삭제합니다.

```
$ curl -X DELETE http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

이 cURL 명령은 `/todos/:id` 엔드포인트에 `DELETE` 요청을 보냅니다. 삭제할 To-Do 항목의 `_id`를 경로 매개변수로 전달하고 있습니다.

다음과 같은 응답을 받아야 합니다.

```json
{"numDeleted": 1}
```

삭제된 To-Do 항목의 수입니다. 항목을 검색하여 항목이 삭제되었는지 확인할 수 있습니다.

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

To-Do 항목이 더 이상 존재하지 않기 때문에 '404 Not Found' 오류가 발생해야 합니다.

## 결론

이 기사에서는 NeDB와 함께 TypeScript를 사용하는 방법을 보여주었습니다. 우리는 NeDB 데이터베이스에 데이터를 저장하는 간단한 To-Do API를 만들었습니다. 또한 cURL을 사용하여 API를 테스트하는 방법도 보여 주었습니다.