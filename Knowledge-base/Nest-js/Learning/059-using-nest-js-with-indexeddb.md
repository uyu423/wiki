---
title: 059: Nest.js를 IndexedDB와 함께 사용하기
description: 
published: true
date: 2023-02-15T22:32:32.746Z
tags: 
editor: markdown
dateCreated: 2023-02-15T22:32:31.003Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [059: Using Nest.js with IndexedDB***English** document is available*](/en/Knowledge-base/Nest-js/Learning/059-using-nest-js-with-indexeddb)
{.links-list}


# IndexedDB와 함께 Nest.js 사용

이 게시물에서는 [Nest.js](https://nestjs.com/)를 [IndexedDB](https://developer.mozilla.org/en-US/docs/)와 함께 사용하는 방법을 살펴보겠습니다. Web/API/IndexedDB_API), JavaScript 기반 데이터베이스.

IndexedDB 데이터베이스에 연결할 간단한 Nest.js 애플리케이션을 만드는 것으로 시작하겠습니다. 그런 다음 데이터베이스에 데이터를 삽입하고 데이터를 쿼리하는 코드를 추가합니다.

## Nest.js 애플리케이션 만들기

먼저 Nest.js 애플리케이션을 만들어야 합니다. [Nest CLI](https://docs.nestjs.com/cli/overview)를 사용하여 이 작업을 수행할 수 있습니다.

```
$ nest new nest-indexeddb
```

이렇게 하면 `nest-indexeddb`라는 디렉토리에 새로운 Nest.js 애플리케이션이 생성됩니다.

## 데이터베이스에 연결

다음으로 IndexedDB 데이터베이스에 연결해야 합니다. [`idb`](https://www.npmjs.com/package/idb) npm 패키지를 사용하여 이를 수행할 수 있습니다.

먼저 `idb` 패키지를 설치해야 합니다.

```
$ npm install idb
```

그런 다음 `src/` 디렉토리에 다음 내용으로 `database.service.ts`라는 새 파일을 만들 수 있습니다.

```typescript
import { Injectable } from '@nestjs/common';
import { openDB, DBSchema } from 'idb';

@Injectable()
export class DatabaseService {
  private dbPromise: Promise<IDBDatabase>;

  constructor() {
    this.dbPromise = openDB<DBSchema>('nest-indexeddb', 1, {
      upgrade(db) {
        db.createObjectStore('todos', {
          keyPath: 'id',
        });
      },
    });
  }

  getDb(): Promise<IDBDatabase> {
    return this.dbPromise;
  }
}
```

이 파일에서 데이터베이스 연결을 담당할 `DatabaseService`라는 새 서비스를 만듭니다. 데이터베이스를 열기 위해 `idb` 패키지의 `openDB` 기능을 사용하고 있습니다. 또한 데이터베이스의 구조를 정의하는 `schema` 개체를 전달하고 있습니다. 이 경우 todos에 대한 데이터를 포함할 `todos`라는 새 개체 저장소를 만듭니다.

## 데이터베이스에 데이터 삽입

이제 데이터베이스에 연결하기 위한 서비스가 있으므로 이를 사용하여 데이터베이스에 데이터를 삽입할 수 있습니다.

먼저 `src/` 디렉토리에 다음 내용으로 `todo.model.ts`라는 새 파일을 생성해야 합니다.

```typescript
export class Todo {
  id: number;
  title: string;
  completed: boolean;
}
```

이 파일에는 할 일에 대한 모델이 포함되어 있습니다. 여기에는 `id`, `title` 및 `completed`의 세 가지 필드가 있습니다.

다음으로 `src/` 디렉토리에 다음 내용으로 `todo.service.ts`라는 새 파일을 만들어야 합니다.

```typescript
import { Injectable } from '@nestjs/common';
import { DatabaseService } from './database.service';
import { Todo } from './todo.model';

@Injectable()
export class TodoService {
  constructor(private databaseService: DatabaseService) {}

  async createTodo(todo: Todo): Promise<void> {
    const db = await this.databaseService.getDb();
    const tx = db.transaction('todos', 'readwrite');
    const store = tx.objectStore('todos');
    store.put(todo);
    await tx.complete;
  }
}
```

이 파일에서 데이터베이스에 데이터 삽입을 담당할 'TodoService'라는 새 서비스를 만듭니다. 데이터베이스에 연결하는 데 사용할 수 있도록 `DatabaseService`를 주입하고 있습니다.

`createTodo` 메서드는 `Todo` 개체를 매개변수로 사용하여 데이터베이스에 삽입합니다. 먼저 데이터베이스에 연결합니다. 그런 다음 새 트랜잭션을 시작합니다. 트랜잭션은 데이터가 원자적으로 데이터베이스에 삽입되도록 하는 데 사용됩니다. 즉, 모든 데이터가 삽입되거나 전혀 삽입되지 않습니다.

트랜잭션을 시작한 후 코드는 `todos` 개체 저장소에 대한 참조를 가져옵니다. 그런 다음 스토어에서 `todo` 객체를 전달하는 `put` 메서드를 호출합니다. 이렇게 하면 `todo` 개체가 데이터베이스에 삽입됩니다.

마지막으로 코드는 트랜잭션에서 `complete` 메서드를 호출합니다. 이렇게 하면 트랜잭션이 커밋되고 데이터가 데이터베이스에 삽입됩니다.

## 데이터베이스에서 데이터 쿼리

이제 데이터베이스에 데이터를 삽입할 수 있으므로 데이터베이스에서 데이터를 쿼리하는 방법을 살펴보겠습니다.

개체 저장소에서 `get` 메서드를 사용하여 데이터베이스에서 데이터를 쿼리할 수 있습니다. `get` 메서드는 키를 매개변수로 사용하고 해당 키와 관련된 값을 반환합니다.

예를 들어 `id`가 `1`인 todo가 있다고 가정해 보겠습니다. 다음과 같이 데이터베이스에서 할 일을 쿼리할 수 있습니다.

```typescript
const todo = await store.get(1);
```

객체 저장소에서 모든 값을 가져오기 위해 `getAll` 메서드를 사용할 수도 있습니다. 예를 들어 다음과 같이 데이터베이스에서 모든 작업을 가져올 수 있습니다.

```typescript
const todos = await store.getAll();
```

객체 저장소에서 모든 키를 가져오기 위해 `getAllKeys` 메서드를 사용할 수도 있습니다. 예를 들어 다음과 같이 `todos` 객체 저장소에서 모든 키를 가져올 수 있습니다.

```typescript
const keys = await store.getAllKeys();
```

## 데이터베이스에서 데이터 삭제

개체 저장소에서 `delete` 메서드를 사용하여 데이터베이스에서 데이터를 삭제할 수 있습니다. `delete` 메소드는 키를 매개변수로 사용하고 해당 키와 연관된 값을 삭제합니다.

예를 들어 `id`가 `1`인 todo가 있다고 가정해 보겠습니다. 다음과 같이 데이터베이스에서 해당 todo를 삭제할 수 있습니다.

```typescript
await store.delete(1);
```

## 결론

이 게시물에서는 IndexedDB와 함께 Nest.js를 사용하는 방법을 살펴보았습니다. 데이터베이스에 연결하고, 데이터베이스에 데이터를 삽입하고, 데이터베이스에서 데이터를 쿼리하고, 데이터베이스에서 데이터를 삭제하는 방법을 살펴보았습니다.