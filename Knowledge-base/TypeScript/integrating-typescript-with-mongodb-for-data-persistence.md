---
title: 데이터 지속성을 위해 TypeScript를 MongoDB와 통합
description: 
published: true
date: 2023-03-12T09:32:52.679Z
tags: 
editor: markdown
dateCreated: 2023-03-12T09:32:52.679Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with MongoDB for Data Persistence***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-mongodb-for-data-persistence)
{.links-list}

# 데이터 지속성을 위해 TypeScript를 MongoDB와 통합

오늘날과 같이 급변하는 디지털 세계에서는 효율적이고 신뢰할 수 있는 데이터 관리가 필수적입니다. MongoDB는 개발자에게 데이터 저장 및 검색을 위한 유연하고 확장 가능한 솔루션을 제공하는 널리 사용되는 NoSQL 데이터베이스입니다. 반면에 TypeScript는 정적 타이핑 및 클래스와 같은 추가 기능을 제공하여 확장 가능하고 유지 관리 가능한 애플리케이션을 더 쉽게 구축할 수 있는 JavaScript의 상위 집합입니다. 이 기사에서는 데이터 지속성을 위해 TypeScript를 MongoDB와 통합하는 방법에 대해 자세히 설명합니다.

## MongoDB 데이터베이스 설정

먼저 MongoDB 데이터베이스를 설정해야 합니다. MongoDB를 설치하고 로컬에서 실행하거나 MongoDB Atlas와 같은 클라우드 기반 솔루션을 사용하여 이를 수행할 수 있습니다. MongoDB 데이터베이스를 설정했으면 MongoDB Node.js 드라이버와 같은 MongoDB 클라이언트를 사용하여 연결할 수 있습니다.

```javascript
import { MongoClient } from 'mongodb';

const uri = 'mongodb+srv://<username>:<password>@<cluster>.mongodb.net/test?retryWrites=true&w=majority';
const client = new MongoClient(uri);

await client.connect();
const database = client.db('<database-name>');
const collection = database.collection('<collection-name>');
```

이제 `collection` 개체를 사용하여 MongoDB 데이터베이스와 상호 작용할 수 있습니다.

## 데이터 모델을 위한 TypeScript 인터페이스 만들기

데이터를 MongoDB 데이터베이스에 유지하기 전에 데이터 모델을 정의하는 TypeScript 인터페이스를 생성해야 합니다. 이 인터페이스는 데이터가 올바른 유형이고 필요한 속성을 가지고 있는지 확인합니다. 간단한 `User` 모델을 위한 인터페이스를 만들어 봅시다.

```typescript
interface User {
  _id: string;
  name: string;
  email: string;
  age: number;
  createdAt: Date;
  updatedAt: Date;
}
```

## 데이터 액세스를 위한 TypeScript 클래스 만들기

다음으로 데이터 삽입, 업데이트 및 쿼리와 같은 데이터 액세스 작업을 처리할 TypeScript 클래스를 만들어야 합니다. 이 클래스는 또한 데이터 모델에 대해 데이터의 유효성을 검사합니다.

```typescript
import { Collection } from 'mongodb';

export class UserRepository {
  constructor(private collection: Collection<User>) {}

  async create(user: User): Promise<User> {
    const { insertedId } = await this.collection.insertOne(user);
    return { ...user, _id: insertedId };
  }

  async update(user: User): Promise<User> {
    await this.collection.updateOne({ _id: user._id }, { $set: user });
    return user;
  }

  async getById(id: string): Promise<User | null> {
    return this.collection.findOne({ _id: id });
  }

  async getAll(): Promise<User[]> {
    return this.collection.find().toArray();
  }

  async delete(id: string): Promise<void> {
    await this.collection.deleteOne({ _id: id });
  }
}
```

`UserRepository` 클래스의 생성자에서 MongoDB 컬렉션을 나타내는 `Collection` 객체를 주입합니다. 그런 다음 이 컬렉션에서 데이터 액세스 작업을 수행하는 메서드를 정의합니다.

우리의 `create` 메서드는 `Promise<User>`를 반환합니다. 이는 `insertOne` 메서드가 `User` 개체에 할당해야 하는 `insertedId` 속성이 있는 개체를 반환하기 때문입니다.

## UserRepository 클래스 사용

이제 `UserRepository` 클래스를 정의했으므로 이를 사용하여 MongoDB 데이터베이스에 데이터를 유지할 수 있습니다. 새 사용자를 생성하고 데이터베이스에 저장하는 간단한 스크립트를 만들어 보겠습니다.

```typescript
const userRepository = new UserRepository(collection);

const user: User = {
  name: 'John Doe',
  email: 'johndoe@example.com',
  age: 30,
  createdAt: new Date(),
  updatedAt: new Date(),
};

const createdUser = await userRepository.create(user);

console.log(createdUser);
```

## 결론

데이터 지속성을 위해 TypeScript를 MongoDB와 통합하려면 데이터 모델을 정의하는 TypeScript 인터페이스와 데이터 액세스 작업을 처리하는 TypeScript 클래스를 생성해야 합니다. TypeScript를 사용하면 데이터가 올바른 유형이고 필요한 속성이 있는지 확인할 수 있으므로 응용 프로그램의 확장성과 유지 관리가 더 쉬워집니다.

## 외부 리소스

- [TypeScript 설명서](https://www.typescriptlang.org/docs/)
- [MongoDB Node.js 드라이버 설명서](https://mongodb.github.io/node-mongodb-native/)
- [MongoDB 아틀라스](https://www.mongodb.com/cloud/atlas)