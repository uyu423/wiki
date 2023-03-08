---
title: 059: Using Nest.js with IndexedDB
description: 
published: true
date: 2023-02-15T22:32:38.601Z
tags: 
editor: markdown
dateCreated: 2023-02-15T22:32:31.007Z
---

- [059: Uso de Nest.js con IndexedDB***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/059-using-nest-js-with-indexeddb)
{.links-list}
- [059：将 Nest.js 与 IndexedDB 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/059-using-nest-js-with-indexeddb)
{.links-list}
- [059: Nest.js를 IndexedDB와 함께 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/059-using-nest-js-with-indexeddb)
{.links-list}


# Using Nest.js with IndexedDB

In this post, we'll take a look at how to use [Nest.js](https://nestjs.com/) with [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API), a JavaScript-based database.

We'll start by creating a simple Nest.js application that will connect to an IndexedDB database. Then, we'll add some code to insert data into the database and query the data.

## Creating a Nest.js Application

First, we need to create a Nest.js application. We can do this using the [Nest CLI](https://docs.nestjs.com/cli/overview).

```
$ nest new nest-indexeddb
```

This will create a new Nest.js application in a directory called `nest-indexeddb`.

## Connecting to the Database

Next, we need to connect to the IndexedDB database. We can do this using the [`idb`](https://www.npmjs.com/package/idb) npm package.

First, we need to install the `idb` package:

```
$ npm install idb
```

Then, we can create a new file called `database.service.ts` in the `src/` directory with the following contents:

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

In this file, we are creating a new service called `DatabaseService` which will be responsible for connecting to the database. We are using the `openDB` function from the `idb` package to open the database. We are also passing in a `schema` object which defines the structure of the database. In this case, we are creating a new object store called `todos` which will contain data about todos.

## Inserting Data into the Database

Now that we have a service for connecting to the database, we can use it to insert data into the database.

First, we need to create a new file called `todo.model.ts` in the `src/` directory with the following contents:

```typescript
export class Todo {
  id: number;
  title: string;
  completed: boolean;
}
```

This file contains a model for a todo. It has three fields: `id`, `title`, and `completed`.

Next, we need to create a new file called `todo.service.ts` in the `src/` directory with the following contents:

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

In this file, we are creating a new service called `TodoService` which will be responsible for insert data into the database. We are injecting the `DatabaseService` so that we can use it to get a connection to the database.

The `createTodo` method takes a `Todo` object as a parameter and inserts it into the database. First, it gets a connection to the database. Then, it starts a new transaction. Transactions are used to ensure that data is inserted into the database atomically. In other words, either all of the data is inserted, or none of it is.

After starting the transaction, the code gets a reference to the `todos` object store. Then, it calls the `put` method on the store, passing in the `todo` object. This will insert the `todo` object into the database.

Finally, the code calls the `complete` method on the transaction. This will commit the transaction, and the data will be inserted into the database.

## Querying Data from the Database

Now that we can insert data into the database, let's take a look at how to query data from the database.

We can query data from the database using the `get` method on an object store. The `get` method takes a key as a parameter and returns the value associated with that key.

For example, let's say we have a todo with an `id` of `1`. We can query that todo from the database like this:

```typescript
const todo = await store.get(1);
```

We can also use the `getAll` method to get all of the values from an object store. For example, we can get all of the todos from the database like this:

```typescript
const todos = await store.getAll();
```

We can also use the `getAllKeys` method to get all of the keys from an object store. For example, we can get all of the keys from the `todos` object store like this:

```typescript
const keys = await store.getAllKeys();
```

## Deleting Data from the Database

We can delete data from the database using the `delete` method on an object store. The `delete` method takes a key as a parameter and deletes the value associated with that key.

For example, let's say we have a todo with an `id` of `1`. We can delete that todo from the database like this:

```typescript
await store.delete(1);
```

## Conclusion

In this post, we've seen how to use Nest.js with IndexedDB. We've seen how to connect to the database, insert data into the database, query data from the database, and delete data from the database.