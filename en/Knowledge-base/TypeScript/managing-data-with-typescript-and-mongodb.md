---
title: Managing Data with TypeScript and MongoDB
description: 
published: true
date: 2023-02-01T02:36:44.880Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:36:42.940Z
---

- [TypeScript 및 MongoDB로 데이터 관리***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/managing-data-with-typescript-and-mongodb)
{.links-list}
- [TypeScript と MongoDB を使用したデータの管理***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/managing-data-with-typescript-and-mongodb)
{.links-list}
- [使用 TypeScript 和 MongoDB 管理数据***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/managing-data-with-typescript-and-mongodb)
{.links-list}


# Managing Data with TypeScript and MongoDB

As a JavaScript developer, you're likely familiar with the benefits of TypeScript. TypeScript is a typed superset of JavaScript that compiles to plain JavaScript, offering benefits like type safety and easier code maintenance.

In this article, we'll explore how to use TypeScript with MongoDB, a popular NoSQL database. We'll look at how to set up a project, how to write type-safe queries, and how to use the MongoDB Node.js driver's `TypedData` class for even more type safety.

## Setting up a TypeScript Project

To get started, we'll need to set up a TypeScript project. We'll use the `ts-node` package to run TypeScript files directly, without the need to compile them first.

First, create a new directory for your project and initialize it with `npm`:

```bash
mkdir ts-mongodb && cd ts-mongodb
npm init -y
```

Next, install the `mongodb`, `@types/mongodb`, and `ts-node` packages:

```bash
npm install mongodb @types/mongodb ts-node
```

Now we can create a `.ts` file and run it with `ts-node`:

```bash
touch index.ts
ts-node index.ts
```

## Connecting to MongoDB

Before we can run any queries, we need to establish a connection to our MongoDB database. The MongoDB Node.js driver makes this easy with the `MongoClient.connect()` method.

We'll start by creating a new file, `src/db.ts`, to house our database connection logic. In this file, we'll create a new `Db` class with a static `connect()` method:

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

The `connect()` method returns a Promise that resolves to a `Db` instance. We can use this instance to run queries against our database.

## Defining a Schema

Before we can write any queries, we need to define a schema for our data. In MongoDB, a schema is not required, but it's a good idea to define one anyway for the sake of type safety. We'll define our schema in a `src/schema.ts` file:

```typescript
export interface User {
  _id: string
  name: string
  age: number
  email: string
}
```

## Writing Type-Safe Queries

Now that we have a schema, we can write some type-safe queries. We'll start by creating a `src/queries.ts` file:

```typescript
import { Db, User } from './db'

export async function getUsers(): Promise<User[]> {
  const db = await Db.connect()
  return db.collection('users').find().toArray()
}
```

Here, we've defined a `getUsers()` function that returns a Promise that resolves to an array of `User` objects. We use the `find()` method to get all documents from the `users` collection, and the `toArray()` method to convert the resulting cursor to an array.

## Using the MongoDB Node.js Driver's `TypedData` Class

The MongoDB Node.js driver provides a `TypedData` class that offers even more type safety when working with data. To use it, we first need to import it:

```typescript
import { Db, User, TypedData } from './db'
```

Then, we can use it to type-cast our data when we fetch it from the database:

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

Here, we've used the `TypedData.cast()` method to type-cast each document in the `data` array to the `User` interface.

## Inserting Data

Inserting data into MongoDB is just as easy as querying it. We can use the `insertOne()` method to insert a single document, or the `insertMany()` method to insert multiple documents:

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

## Updating Data

Updating data in MongoDB is done with the `updateOne()` and `updateMany()` methods. These methods take a filter object and an update object. The filter object is used to match the documents that should be updated, and the update object is used to specify the fields that should be updated and the new values for those fields:

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

## Deleting Data

Deleting data in MongoDB is done with the `deleteOne()` and `deleteMany()` methods. These methods take a filter object that is used to match the documents that should be deleted:

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

## Wrapping Up

In this article, we've explored how to use TypeScript with MongoDB. We've looked at how to set up a project, how to write type-safe queries, and how to use the MongoDB Node.js driver's `TypedData` class for even more type safety.