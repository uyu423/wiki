---
title: TypeScript と MongoDB を使用したデータの管理
description: 
published: true
date: 2023-02-01T02:36:46.809Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:36:42.941Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Managing Data with TypeScript and MongoDB***English** version of this document is available*](/en/Knowledge-base/TypeScript/managing-data-with-typescript-and-mongodb)
{.links-list}


#TypeScriptとMongoDBによるデータ管理

JavaScriptの開発者であれば、TypeScriptの利点に精通しています。 TypeScript は、通常の JavaScript でコンパイルされる型付き JavaScript の親セットであり、型の安全性や簡単なコード保守などの利点を提供します。

この記事では、広く使用されているNoSQLデータベースであるMongoDBでTypeScriptを使用する方法について説明します。プロジェクトを設定する方法、型が安全なクエリを作成する方法、型の安全性をさらに強化するために、MongoDB Node.jsドライバの `TypedData`クラスを使用する方法を見てみましょう。

## TypeScriptプロジェクトの設定

開始するには、TypeScriptプロジェクトを設定する必要があります。まず、コンパイルを必要とせずにTypeScriptファイルを直接実行するために `ts-node`パッケージを使用します。

まず、プロジェクトの新しいディレクトリを作成し、 `npm`で初期化します。

```bash
mkdir ts-mongodb && cd ts-mongodb
npm init -y
```

次に、 `mongodb`、 `@types/mongodb`、および `ts-node`パッケージをインストールします。

```bash
npm install mongodb @types/mongodb ts-node
```

これで `.ts` ファイルを作成して `ts-node` として実行できるようになりました。

```bash
touch index.ts
ts-node index.ts
```

## モンゴルDBに接続する

クエリを実行する前に、MongoDBデータベースへの接続を確立する必要があります。 MongoDB Node.jsドライバは `MongoClient.connect()`メソッドを使って簡単に作成します。

データベース接続ロジックを保持する新しいファイル `src/db.ts` を作成することから始めましょう。このファイルでは、静的 `connect()` メソッドを使用して新しい `Db` クラスを作成します。

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

`connect()` メソッドは `Db` インスタンスで解決される Promise を返します。このインスタンスを使用して、データベースに対してクエリを実行できます。

## スキーマの定義

クエリを作成する前に、データのスキーマを定義する必要があります。 MongoDBではスキーマは必要ありませんが、型安全のためにスキーマを定義することをお勧めします。 `src/schema.ts` ファイルでスキーマを定義します。

```typescript
export interface User {
  _id: string
  name: string
  age: number
  email: string
}
```

## 型安全問合せの作成

これでスキーマがあるので、安全な形式のクエリを書くことができます。 `src/queries.ts`ファイルを生成することから始めましょう：

```typescript
import { Db, User } from './db'

export async function getUsers(): Promise<User[]> {
  const db = await Db.connect()
  return db.collection('users').find().toArray()
}
```

ここでは、`User`オブジェクトの配列として識別されるPromiseを返す`getUsers（）`関数を定義しました。 `users`コレクションからすべての文書を取得するには`find（）`メソッドを使用し、結果のカーソルを配列に変換するために`toArray（）`メソッドを使用します。

## MongoDB Node.jsドライバの `TypedData`クラスを使用する

MongoDB Node.jsドライバは、データを扱うときにはるかに安全な型を提供する`TypedData`クラスを提供します。これを使用するには、まずインポートする必要があります。

```typescript
import { Db, User, TypedData } from './db'
```

その後、データベースからデータをインポートするときにそれを使用してデータを型変換できます。

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

ここでは `TypedData.cast()` メソッドを使って `data` 配列の各ドキュメントを `User` インタフェースに型変換しました。

## データの挿入

MongoDBにデータを挿入するのは、クエリするのと同じくらい簡単です。 `insertOne()` メソッドを使って単一の文書を挿入するか、 `insertMany()` メソッドを使って複数の文書を挿入することができます。

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

##データ更新

MongoDBでは、データの更新は `updateOne()` と `updateMany()` メソッドで行われます。これらのメソッドはフィルタオブジェクトと更新オブジェクトを使用します。フィルタオブジェクトは、更新する必要がある文書を一致させるために使用され、更新オブジェクトは更新する必要があるフィールドとそのフィールドの新しい値を指定するために使用されます。

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

## データ削除

MongoDBでは、データの削除は `deleteOne()` と `deleteMany()` メソッドで行われます。これらのメソッドは、削除する必要がある文書を一致させるために使用されるフィルタオブジェクトを使用します。

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

##仕上げ

この記事では、MongoDBでTypeScriptを使用する方法について説明しました。私たちはプロジェクトを設定する方法、型に安全なクエリを書く方法、そしてもっと安全な型のためにMongoDB Node.jsドライバの `TypedData`クラスを使用する方法を見ました。