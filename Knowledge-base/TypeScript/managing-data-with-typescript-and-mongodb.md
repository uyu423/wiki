---
title: TypeScript 및 MongoDB로 데이터 관리
description: 
published: true
date: 2023-02-01T02:36:46.809Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:36:42.939Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Managing Data with TypeScript and MongoDB***English** version of this document is available*](/en/Knowledge-base/TypeScript/managing-data-with-typescript-and-mongodb)
{.links-list}


# TypeScript와 MongoDB로 데이터 관리하기

JavaScript 개발자라면 TypeScript의 이점에 대해 잘 알고 있을 것입니다. TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript의 상위 집합으로, 유형 안전성 및 더 쉬운 코드 유지 관리와 같은 이점을 제공합니다.

이 기사에서는 널리 사용되는 NoSQL 데이터베이스인 MongoDB에서 TypeScript를 사용하는 방법을 살펴봅니다. 프로젝트를 설정하는 방법, 유형이 안전한 쿼리를 작성하는 방법, 유형 안전성을 더욱 강화하기 위해 MongoDB Node.js 드라이버의 `TypedData` 클래스를 사용하는 방법을 살펴보겠습니다.

## TypeScript 프로젝트 설정

시작하려면 TypeScript 프로젝트를 설정해야 합니다. 먼저 컴파일할 필요 없이 TypeScript 파일을 직접 실행하기 위해 `ts-node` 패키지를 사용할 것입니다.

먼저 프로젝트의 새 디렉터리를 만들고 `npm`으로 초기화합니다.

```bash
mkdir ts-mongodb && cd ts-mongodb
npm init -y
```

다음으로 `mongodb`, `@types/mongodb` 및 `ts-node` 패키지를 설치합니다.

```bash
npm install mongodb @types/mongodb ts-node
```

이제 `.ts` 파일을 만들고 `ts-node`로 실행할 수 있습니다.

```bash
touch index.ts
ts-node index.ts
```

## 몽고DB에 연결하기

쿼리를 실행하기 전에 MongoDB 데이터베이스에 대한 연결을 설정해야 합니다. MongoDB Node.js 드라이버는 `MongoClient.connect()` 메서드를 사용하여 이를 쉽게 만듭니다.

데이터베이스 연결 논리를 보관할 새 파일 `src/db.ts`를 생성하여 시작하겠습니다. 이 파일에서 정적 `connect()` 메서드를 사용하여 새 `Db` 클래스를 만듭니다.

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

`connect()` 메서드는 `Db` 인스턴스로 확인되는 Promise를 반환합니다. 이 인스턴스를 사용하여 데이터베이스에 대한 쿼리를 실행할 수 있습니다.

## 스키마 정의

쿼리를 작성하기 전에 데이터에 대한 스키마를 정의해야 합니다. MongoDB에서는 스키마가 필요하지 않지만 형식 안전을 위해 스키마를 정의하는 것이 좋습니다. `src/schema.ts` 파일에서 스키마를 정의합니다:

```typescript
export interface User {
  _id: string
  name: string
  age: number
  email: string
}
```

## 형식 안전 쿼리 작성

이제 스키마가 있으므로 형식이 안전한 쿼리를 작성할 수 있습니다. `src/queries.ts` 파일을 생성하는 것으로 시작하겠습니다:

```typescript
import { Db, User } from './db'

export async function getUsers(): Promise<User[]> {
  const db = await Db.connect()
  return db.collection('users').find().toArray()
}
```

여기에서 `User` 개체의 배열로 확인되는 Promise를 반환하는 `getUsers()` 함수를 정의했습니다. `users` 컬렉션에서 모든 문서를 가져오기 위해 `find()` 메소드를 사용하고 결과 커서를 배열로 변환하기 위해 `toArray()` 메소드를 사용합니다.

## MongoDB Node.js 드라이버의 `TypedData` 클래스 사용

MongoDB Node.js 드라이버는 데이터로 작업할 때 훨씬 더 안전한 유형을 제공하는 `TypedData` 클래스를 제공합니다. 이를 사용하려면 먼저 가져와야 합니다.

```typescript
import { Db, User, TypedData } from './db'
```

그런 다음 데이터베이스에서 데이터를 가져올 때 이를 사용하여 데이터를 유형 변환할 수 있습니다.

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

여기서는 `TypedData.cast()` 메서드를 사용하여 `data` 배열의 각 문서를 `User` 인터페이스로 유형 변환했습니다.

## 데이터 삽입

MongoDB에 데이터를 삽입하는 것은 쿼리하는 것만큼 쉽습니다. `insertOne()` 메서드를 사용하여 단일 문서를 삽입하거나 `insertMany()` 메서드를 사용하여 여러 문서를 삽입할 수 있습니다.

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

## 데이터 업데이트

MongoDB에서 데이터 업데이트는 `updateOne()` 및 `updateMany()` 메서드로 수행됩니다. 이러한 메서드는 필터 개체와 업데이트 개체를 사용합니다. 필터 개체는 업데이트해야 하는 문서를 일치시키는 데 사용되며 업데이트 개체는 업데이트해야 하는 필드와 해당 필드의 새 값을 지정하는 데 사용됩니다.

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

## 데이터 삭제

MongoDB에서 데이터 삭제는 `deleteOne()` 및 `deleteMany()` 메서드로 수행됩니다. 이러한 메서드는 삭제해야 하는 문서를 일치시키는 데 사용되는 필터 개체를 사용합니다.

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

## 마무리

이 기사에서는 MongoDB에서 TypeScript를 사용하는 방법을 살펴보았습니다. 우리는 프로젝트를 설정하는 방법, 유형에 안전한 쿼리를 작성하는 방법, 훨씬 더 안전한 유형을 위해 MongoDB Node.js 드라이버의 `TypedData` 클래스를 사용하는 방법을 살펴보았습니다.