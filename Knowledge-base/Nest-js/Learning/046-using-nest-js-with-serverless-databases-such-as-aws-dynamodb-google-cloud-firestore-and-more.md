---
title: 046: AWS DynamoDB, Google Cloud Firestore 등과 같은 서버리스 데이터베이스에서 Nest.js 사용
description: 
published: true
date: 2023-02-11T22:55:34.659Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:55:27.837Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [046: Using Nest.js with serverless databases such as AWS DynamoDB, Google Cloud Firestore, and more***English** document is available*](/en/Knowledge-base/Nest-js/Learning/046-using-nest-js-with-serverless-databases-such-as-aws-dynamodb-google-cloud-firestore-and-more)
{.links-list}


# AWS DynamoDB, Google Cloud Firestore 등과 같은 서버리스 데이터베이스와 함께 Nest.js 사용

Nest.js는 서버 측 애플리케이션을 구축하기 위한 강력한 프레임워크입니다. TypeScript 및 Node.js를 기반으로 하며 Express.js 프레임워크를 사용합니다. Nest.js는 사용하기 쉽고 TypeScript를 잘 지원하기 때문에 서버리스 애플리케이션을 구축하는 데 탁월한 선택입니다.

이 게시물에서는 AWS DynamoDB, Google Cloud Firestore 등과 같은 서버리스 데이터베이스에서 Nest.js를 사용하는 방법을 알아봅니다. 또한 Nest.js 애플리케이션을 AWS Lambda에 배포하는 방법도 배웁니다.

## AWS DynamoDB에서 Nest.js 사용

AWS DynamoDB는 널리 사용되는 서버리스 데이터베이스입니다. 빠르고 확장 가능한 NoSQL 데이터베이스입니다. DynamoDB는 빠르고 확장 가능한 데이터베이스가 필요한 서버리스 애플리케이션에 탁월한 선택입니다.

Nest.js와 함께 DynamoDB를 사용하려면 @nestjs/aws-serverless-dynamodb 패키지를 설치해야 합니다. 이 패키지는 Nest.js용 DynamoDB 데이터 매퍼를 제공합니다.

```bash
$ npm install @nestjs/aws-serverless-dynamodb
```

패키지가 설치되면 DynamoDB 데이터 매퍼를 생성할 수 있습니다.

```typescript
import { DynamoDB } from '@nestjs/aws-serverless-dynamodb';

@Injectable()
export class DynamoDbMapper {
  constructor(private readonly dynamoDb: DynamoDB) {}
}
```

DynamoDB 데이터 매퍼는 DynamoDB에 액세스하는 데 사용할 수 있는 DynamoDB 클라이언트를 제공합니다.

DynamoDB 데이터 매퍼를 사용하려면 DynamoDB 테이블을 생성해야 합니다. AWS Management Console을 사용하여 이 작업을 수행할 수 있습니다.

DynamoDB 테이블이 생성되면 DynamoDB 데이터 매퍼를 가져오는 Nest.js 모듈을 생성해야 합니다.

```typescript
import { Module } from '@nestjs/common';
import { DynamoDbMapper } from './dynamodb-mapper.service';

@Module({
  providers: [DynamoDbMapper],
  exports: [DynamoDbMapper],
})
export class DynamoDbModule {}
```

이제 DynamoDB 데이터 매퍼를 생성했으므로 이를 사용하여 Nest.js 애플리케이션에서 DynamoDB에 액세스할 수 있습니다.

## Google Cloud Firestore에서 Nest.js 사용

Google Cloud Firestore는 널리 사용되는 서버리스 데이터베이스입니다. 빠르고 확장 가능한 NoSQL 데이터베이스입니다. Firestore는 빠르고 확장 가능한 데이터베이스가 필요한 서버리스 애플리케이션에 적합합니다.

Firestore를 Nest.js와 함께 사용하려면 @nestjs/cloud-firestore 패키지를 설치해야 합니다. 이 패키지는 Nest.js용 Firestore 데이터 매퍼를 제공합니다.

```bash
$ npm install @nestjs/cloud-firestore
```

패키지가 설치되면 Firestore 데이터 매퍼를 만들 수 있습니다.

```typescript
import { Firestore } from '@nestjs/cloud-firestore';

@Injectable()
export class FirestoreMapper {
  constructor(private readonly firestore: Firestore) {}
}
```

Firestore 데이터 매퍼는 Firestore에 액세스하는 데 사용할 수 있는 Firestore 클라이언트를 제공합니다.

Firestore 데이터 매퍼를 사용하려면 Firestore 데이터베이스를 생성해야 합니다. Google Cloud Console을 사용하여 이 작업을 수행할 수 있습니다.

Firestore 데이터베이스가 생성되면 Firestore 데이터 매퍼를 가져오는 Nest.js 모듈을 생성해야 합니다.

```typescript
import { Module } from '@nestjs/common';
import { FirestoreMapper } from './firestore-mapper.service';

@Module({
  providers: [FirestoreMapper],
  exports: [FirestoreMapper],
})
export class FirestoreModule {}
```

이제 Firestore 데이터 매퍼를 만들었으므로 이를 사용하여 Nest.js 애플리케이션에서 Firestore에 액세스할 수 있습니다.

## AWS Lambda에 Nest.js 배포

AWS Lambda는 널리 사용되는 서버리스 플랫폼입니다. 빠르게 확장해야 하는 서버리스 애플리케이션에 적합합니다.

Nest.js를 AWS Lambda에 배포하려면 @nestjs/serverless 패키지를 설치해야 합니다. 이 패키지는 Nest.js 서버리스 어댑터를 제공합니다.

```bash
$ npm install @nestjs/serverless
```

패키지가 설치되면 Nest.js 서버리스 어댑터를 만들 수 있습니다.

```typescript
import { ServerlessAdapter } from '@nestjs/serverless';

@Injectable()
export class ServerlessAdapter extends ServerlessAdapter {}
```

ServerlessAdapter는 AWS Lambda에서 Nest.js 애플리케이션을 실행하는 데 사용할 수 있는 Express.js 서버를 제공합니다.

ServerlessAdapter를 사용하려면 AWS Lambda 함수를 생성해야 합니다. AWS Management Console을 사용하여 이 작업을 수행할 수 있습니다.

AWS Lambda 함수가 생성되면 ServerlessAdapter를 가져오는 Nest.js 모듈을 생성해야 합니다.

```typescript
import { Module } from '@nestjs/common';
import { ServerlessAdapter } from './serverless-adapter.service';

@Module({
  providers: [ServerlessAdapter],
  exports: [ServerlessAdapter],
})
export class ServerlessModule {}
```

이제 ServerlessAdapter를 생성했으므로 이를 사용하여 Nest.js 애플리케이션을 AWS Lambda에 배포할 수 있습니다.