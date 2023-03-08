---
title: MongoDB 데이터 관리를 위해 Mongoose와 함께 TypeScript 사용
description: 
published: true
date: 2023-02-01T08:18:10.814Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:18:09.311Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Using TypeScript with Mongoose for MongoDB Data Management***English** version of this document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-mongoose-for-mongodb-data-management)
{.links-list}


  기사 제목은 "MongoDB 데이터 관리를 위해 Mongoose와 함께 TypeScript 사용"이어야 합니다.

# MongoDB 데이터 관리를 위해 Mongoose와 함께 TypeScript 사용

Mongoose는 MongoDB용 데이터를 모델링하기 위한 스키마 기반 솔루션을 제공하는 ODM(개체 데이터 모델링) 라이브러리입니다. JavaScript로 작성되었으며 Node.js 및 웹 애플리케이션에서 사용할 수 있습니다.

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다.

이 기사에서는 Mongoose에서 TypeScript를 사용하는 방법을 보여줍니다. Mongoose와 함께 TypeScript를 사용할 때의 이점을 보여주는 간단한 예제를 만들 것입니다.

## 몽구스와 함께 TypeScript를 사용하는 이유는 무엇입니까?

TypeScript는 더 나은 코드를 작성하는 데 도움이 되는 강력한 언어입니다. 유형 시스템은 코드가 실행되기 전에 컴파일 시간에 오류를 포착할 수 있습니다. 이렇게 하면 시간을 절약하고 잠재적인 버그를 방지할 수 있습니다.

또한 TypeScript의 모듈 및 클래스 지원을 통해 코드를 더 잘 구성할 수 있습니다. 이렇게 하면 코드를 보다 유지 관리하기 쉽고 이해하기 쉽게 만들 수 있습니다.

## TypeScript 및 몽구스 설정

시작하기 전에 TypeScript와 Mongoose를 설정해야 합니다.

먼저 npm을 사용하여 TypeScript와 Mongoose를 설치합니다.

```
npm install -g typescript
npm install mongoose
```

다음으로 `schema.ts`라는 파일을 만들고 다음 코드를 추가합니다.

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

export default User;
```

이 코드는 `User` 모델에 대한 스키마를 생성합니다. 스키마에는 `name`, `age` 및 `email` 필드가 포함됩니다. 다음 섹션에서 이 스키마를 사용하여 `User` 모델을 생성합니다.

## 사용자 모델 만들기

이제 스키마가 있으므로 모델을 만들 수 있습니다. 모델은 데이터베이스를 쿼리하는 데 사용할 수 있는 스키마의 인스턴스입니다.

모델을 생성하기 위해 `schema.ts` 파일에 다음 코드를 추가합니다.

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

const user = new User({
  name: 'John',
  age: 25,
  email: 'john@example.com'
});

user.save((err, user) => {
  if (err) {
    console.log(err);
  } else {
    console.log(user);
  }
});

export default User;
```

이 코드에서는 새로운 `User` 모델을 생성하고 데이터베이스에 저장합니다. 'save' 메소드를 사용하여 모델을 데이터베이스에 저장할 수 있습니다. 이 메서드는 모델이 저장될 때 호출되는 콜백 함수를 사용합니다.

콜백 함수에는 `err` 및 `user`라는 두 개의 인수가 있습니다. `err`는 모델 저장에 오류가 있을 경우 설정되는 오류 객체입니다. `user`는 저장된 모델입니다.

## 데이터베이스 쿼리

모델을 저장한 후에는 데이터베이스를 쿼리하여 저장된 데이터를 가져올 수 있습니다.

데이터베이스를 쿼리하기 위해 `schema.ts` 파일에 다음 코드를 추가합니다.

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

User.find((err, users) => {
  if (err) {
    console.log(err);
  } else {
    console.log(users);
  }
});

export default User;
```

이 코드에서는 `find` 메서드를 사용하여 데이터베이스를 쿼리합니다. 이 메서드는 쿼리가 완료될 때 호출되는 콜백 함수를 사용합니다.

콜백 함수에는 `err` 및 `users`라는 두 개의 인수가 있습니다. `err`은 데이터베이스 쿼리 오류가 있을 경우 설정되는 오류 개체입니다. `users`는 쿼리와 일치하는 모델의 배열입니다.

## 사용자 삭제

데이터베이스에서 사용자를 삭제할 수도 있습니다. 이를 위해 `schema.ts` 파일에 다음 코드를 추가합니다.

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

User.findByIdAndRemove('5b9d7d4f4a6d4e0f1046b82b', (err, user) => {
  if (err) {
    console.log(err);
  } else {
    console.log(user);
  }
});

export default User;
```

이 코드에서는 `findByIdAndRemove` 메서드를 사용하여 데이터베이스에서 사용자를 삭제합니다. 이 메서드는 삭제할 사용자의 `_id`와 콜백 함수를 취합니다.

콜백 함수에는 `err` 및 `user`라는 두 개의 인수가 있습니다. `err`은 사용자 삭제 오류가 있을 경우 설정되는 오류 객체입니다. `user`는 삭제된 사용자입니다.

## 사용자 업데이트

데이터베이스에서 사용자를 업데이트할 수도 있습니다. 이를 위해 `schema.ts` 파일에 다음 코드를 추가합니다.

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

User.findByIdAndUpdate('5b9d7d4f4a6d4e0f1046b82b', { name: 'Jane' }, { new: true }, (err, user) => {
  if (err) {
    console.log(err);
  } else {
    console.log(user);
  }
});

export default User;
```

이 코드에서는 `findByIdAndUpdate` 메서드를 사용하여 데이터베이스의 사용자를 업데이트합니다. 이 메서드는 업데이트할 사용자의 `_id`, 업데이트할 필드 및 콜백 함수를 사용합니다.

콜백 함수에는 `err` 및 `user`라는 두 개의 인수가 있습니다. `err`은 사용자 업데이트 오류가 있는 경우 설정되는 오류 개체입니다. `user`는 업데이트된 사용자입니다.

## 결론

이 기사에서는 Mongoose에서 TypeScript를 사용하는 방법을 설명했습니다. Mongoose에서 TypeScript를 사용할 때의 이점을 보여주는 간단한 예제를 만들었습니다.

TypeScript는 더 나은 코드를 작성하는 데 도움이 되는 강력한 언어입니다. 유형 시스템은 코드가 실행되기 전에 컴파일 시간에 오류를 포착할 수 있습니다. 이렇게 하면 시간을 절약하고 잠재적인 버그를 방지할 수 있습니다.

또한 TypeScript의 모듈 및 클래스 지원을 통해 코드를 더 잘 구성할 수 있습니다. 이렇게 하면 코드를 보다 유지 관리하기 쉽고 이해하기 쉽게 만들 수 있습니다.

MongoDB를 위한 형식화된 솔루션을 찾고 있다면 TypeScript와 Mongoose가 훌륭한 옵션입니다.