---
title: 059：将 Nest.js 与 IndexedDB 结合使用
description: 
published: true
date: 2023-02-15T22:32:32.650Z
tags: 
editor: markdown
dateCreated: 2023-02-15T22:32:31.001Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [059: Using Nest.js with IndexedDB***English** document is available*](/en/Knowledge-base/Nest-js/Learning/059-using-nest-js-with-indexeddb)
{.links-list}


# 将 Nest.js 与 IndexedDB 结合使用

在这篇文章中，我们将看看如何将 [Nest.js](https://nestjs.com/) 与 [IndexedDB](https://developer.mozilla.org/en-US/docs/ Web/API/IndexedDB_API)，一个基于 JavaScript 的数据库。

我们将从创建一个连接到 IndexedDB 数据库的简单 Nest.js 应用程序开始。然后，我们将添加一些代码以将数据插入数据库并查询数据。

## 创建一个 Nest.js 应用程序

首先，我们需要创建一个 Nest.js 应用程序。我们可以使用 [Nest CLI](https://docs.nestjs.com/cli/overview) 执行此操作。

```
$ nest new nest-indexeddb
```

这将在名为“nest-indexeddb”的目录中创建一个新的 Nest.js 应用程序。

## 连接到数据库

接下来，我们需要连接到 IndexedDB 数据库。我们可以使用 [`idb`](https://www.npmjs.com/package/idb) npm 包来做到这一点。

首先，我们需要安装 `idb` 包：

```
$ npm install idb
```

然后，我们可以在 `src/` 目录中创建一个名为 `database.service.ts` 的新文件，内容如下：

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

在这个文件中，我们正在创建一个名为“DatabaseService”的新服务，它将负责连接到数据库。我们正在使用 `idb` 包中的 `openDB` 函数来打开数据库。我们还传递了一个定义数据库结构的“schema”对象。在这种情况下，我们正在创建一个名为“todos”的新对象存储，它将包含有关待办事项的数据。

## 向数据库中插入数据

现在我们有了一个连接数据库的服务，我们可以用它来向数据库中插入数据。

首先，我们需要在 `src/` 目录中创建一个名为 `todo.model.ts` 的新文件，内容如下：

```typescript
export class Todo {
  id: number;
  title: string;
  completed: boolean;
}
```

此文件包含待办事项的模型。它具有三个字段：`id`、`title` 和 `completed`。

接下来，我们需要在 `src/` 目录中创建一个名为 `todo.service.ts` 的新文件，内容如下：

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

在这个文件中，我们正在创建一个名为“TodoService”的新服务，它将负责将数据插入数据库。我们正在注入“DatabaseService”，以便我们可以使用它来获得与数据库的连接。

`createTodo` 方法将一个 `Todo` 对象作为参数并将其插入到数据库中。首先，它获得到数据库的连接。然后，它开始一个新的事务。事务用于确保数据以原子方式插入到数据库中。换句话说，要么插入所有数据，要么一个都不插入。

开始事务后，代码获取对“todos”对象存储的引用。然后，它调用商店的“put”方法，传入“todo”对象。这会将 `todo` 对象插入到数据库中。

最后，代码调用交易的 `complete` 方法。这将提交事务，并且数据将被插入到数据库中。

## 从数据库中查询数据

现在我们可以向数据库中插入数据了，让我们来看看如何从数据库中查询数据。

我们可以使用对象存储上的 get 方法从数据库中查询数据。 `get` 方法将键作为参数并返回与该键关联的值。

例如，假设我们有一个 id 为 1 的待办事项。我们可以像这样从数据库中查询待办事项：

```typescript
const todo = await store.get(1);
```

我们还可以使用 getAll 方法从对象存储中获取所有值。例如，我们可以像这样从数据库中获取所有的待办事项：

```typescript
const todos = await store.getAll();
```

我们还可以使用 getAllKeys 方法从对象存储中获取所有键。例如，我们可以像这样从 `todos` 对象存储中获取所有键：

```typescript
const keys = await store.getAllKeys();
```

## 从数据库中删除数据

我们可以使用对象存储上的 delete 方法从数据库中删除数据。 `delete` 方法将键作为参数并删除与该键关联的值。

例如，假设我们有一个 id 为 1 的待办事项。我们可以像这样从数据库中删除那个待办事项：

```typescript
await store.delete(1);
```

## 结论

在本文中，我们了解了如何将 Nest.js 与 IndexedDB 结合使用。我们已经了解了如何连接到数据库、向数据库中插入数据、从数据库中查询数据以及从数据库中删除数据。