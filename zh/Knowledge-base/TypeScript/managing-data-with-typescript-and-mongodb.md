---
title: 使用 TypeScript 和 MongoDB 管理数据
description: 
published: true
date: 2023-02-01T02:36:46.809Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:36:42.948Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Managing Data with TypeScript and MongoDB***English** version of this document is available*](/en/Knowledge-base/TypeScript/managing-data-with-typescript-and-mongodb)
{.links-list}


# 使用 TypeScript 和 MongoDB 管理数据

作为 JavaScript 开发人员，您可能熟悉 TypeScript 的好处。 TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript，提供类型安全和更轻松的代码维护等优势。

在本文中，我们将探讨如何将 TypeScript 与流行的 NoSQL 数据库 MongoDB 结合使用。我们将了解如何设置项目、如何编写类型安全的查询以及如何使用 MongoDB Node.js 驱动程序的“TypedData”类来实现更高的类型安全性。

## 设置 TypeScript 项目

首先，我们需要设置一个 TypeScript 项目。我们将使用 ts-node 包直接运行 TypeScript 文件，无需先编译它们。

首先，为您的项目创建一个新目录并使用 `npm` 初始化它：

```bash
mkdir ts-mongodb && cd ts-mongodb
npm init -y
```

接下来，安装 `mongodb`、`@types/mongodb` 和 `ts-node` 包：

```bash
npm install mongodb @types/mongodb ts-node
```

现在我们可以创建一个 .ts 文件并使用 ts-node 运行它：

```bash
touch index.ts
ts-node index.ts
```

## 连接到 MongoDB

在我们可以运行任何查询之前，我们需要建立到我们的 MongoDB 数据库的连接。 MongoDB Node.js 驱动程序使用 `MongoClient.connect()` 方法使这一切变得简单。

我们将首先创建一个新文件 `src/db.ts` 来存放我们的数据库连接逻辑。在这个文件中，我们将使用静态 connect() 方法创建一个新的 Db 类：

```typescript
import { MongoClient } from 'mongodb'

export class Db {
  static async connect() {
    const client = await MongoClient.connect(
      'mongodb://localhost:27017',
      { useNewUrlParser: true }
    )
    return client.db('ts-mongodb')
  }
}
```

`connect()` 方法返回一个解析为 `Db` 实例的 Promise。我们可以使用此实例对我们的数据库运行查询。

## 定义模式

在我们可以编写任何查询之前，我们需要为我们的数据定义一个模式。在 MongoDB 中，模式不是必需的，但为了类型安全，无论如何定义一个模式是个好主意。我们将在 `src/schema.ts` 文件中定义我们的模式：

```typescript
export interface User {
  _id: string
  name: string
  age: number
  email: string
}
```

## 编写类型安全的查询

现在我们有了一个模式，我们可以编写一些类型安全的查询。我们将从创建一个 `src/queries.ts` 文件开始：

```typescript
import { Db, User } from './db'

export async function getUsers(): Promise<User[]> {
  const db = await Db.connect()
  return db.collection('users').find().toArray()
}
```

在这里，我们定义了一个 getUsers() 函数，它返回一个解析为 User 对象数组的 Promise。我们使用 `find()` 方法从 `users` 集合中获取所有文档，并使用 `toArray()` 方法将生成的游标转换为数组。

## 使用 MongoDB Node.js 驱动程序的 `TypedData` 类

MongoDB Node.js 驱动程序提供了一个“TypedData”类，该类在处理数据时提供了更高的类型安全性。要使用它，我们首先需要导入它：

```typescript
import { Db, User, TypedData } from './db'
```

然后，当我们从数据库中获取数据时，我们可以使用它来对数据进行类型转换：

```typescript
export async function getUsers(): Promise<User[]> {
  const db = await Db.connect()
  const data = await db
    .collection<User>('users')
    .find()
    .toArray()
  return data.map(d => TypedData.cast<User>(d))
}
```

在这里，我们使用了 TypedData.cast() 方法将 data 数组中的每个文档类型转换为 User 界面。

## 插入数据

向 MongoDB 中插入数据与查询数据一样简单。我们可以使用 insertOne() 方法插入单个文档，或者使用 insertMany() 方法插入多个文档：

```typescript
export async function insertUser(user: User): Promise<void> {
  const db = await Db.connect()
  await db.collection('users').insertOne(user)
}

export async function insertUsers(users: User[]): Promise<void> {
  const db = await Db.connect()
  await db.collection('users').insertMany(users)
}
```

## 更新数据

更新 MongoDB 中的数据是通过 `updateOne()` 和 `updateMany()` 方法完成的。这些方法采用过滤器对象和更新对象。 filter 对象用于匹配应该更新的文档，update 对象用于指定应该更新的字段以及这些字段的新值：

```typescript
export async function updateUser(
  filter: object,
  update: object
): Promise<void> {
  const db = await Db.connect()
  await db.collection('users').updateOne(filter, update)
}

export async function updateUsers(
  filter: object,
  update: object
): Promise<void> {
  const db = await Db.connect()
  await db.collection('users').updateMany(filter, update)
}
```

## 删除数据

在 MongoDB 中删除数据是使用 deleteOne() 和 deleteMany() 方法完成的。这些方法采用一个过滤器对象，用于匹配应删除的文档：

```typescript
export async function deleteUser(filter: object): Promise<void> {
  const db = await Db.connect()
  await db.collection('users').deleteOne(filter)
}

export async function deleteUsers(filter: object): Promise<void> {
  const db = await Db.connect()
  await db.collection('users').deleteMany(filter)
}
```

## 包起来

在本文中，我们探讨了如何将 TypeScript 与 MongoDB 结合使用。我们了解了如何设置项目、如何编写类型安全的查询以及如何使用 MongoDB Node.js 驱动程序的“TypedData”类来提高类型安全性。