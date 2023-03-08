---
title: 046: Using Nest.js with serverless databases such as AWS DynamoDB, Google Cloud Firestore, and more
description: 
published: true
date: 2023-02-11T22:55:29.693Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:55:27.846Z
---

- [046: uso de Nest.js con bases de datos sin servidor como AWS DynamoDB, Google Cloud Firestore y más***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/046-using-nest-js-with-serverless-databases-such-as-aws-dynamodb-google-cloud-firestore-and-more)
{.links-list}
- [046：将 Nest.js 与无服务器数据库（例如 AWS DynamoDB、Google Cloud Firestore 等）结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/046-using-nest-js-with-serverless-databases-such-as-aws-dynamodb-google-cloud-firestore-and-more)
{.links-list}
- [046: AWS DynamoDB, Google Cloud Firestore 등과 같은 서버리스 데이터베이스에서 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/046-using-nest-js-with-serverless-databases-such-as-aws-dynamodb-google-cloud-firestore-and-more)
{.links-list}


# Using Nest.js with serverless databases such as AWS DynamoDB, Google Cloud Firestore, and more

Nest.js is a powerful framework for building server-side applications. It is based on TypeScript and Node.js, and it uses the Express.js framework. Nest.js is a great choice for building serverless applications, because it is easy to use and it has good support for TypeScript.

In this post, we will learn how to use Nest.js with serverless databases such as AWS DynamoDB, Google Cloud Firestore, and more. We will also learn how to deploy our Nest.js application to AWS Lambda.

## Using Nest.js with AWS DynamoDB

AWS DynamoDB is a popular serverless database. It is a fast and scalable NoSQL database. DynamoDB is a great choice for serverless applications that need a fast and scalable database.

To use DynamoDB with Nest.js, we need to install the @nestjs/aws-serverless-dynamodb package. This package provides a DynamoDB data mapper for Nest.js.

```bash
$ npm install @nestjs/aws-serverless-dynamodb
```

Once the package is installed, we can create a DynamoDB data mapper.

```typescript
import { DynamoDB } from '@nestjs/aws-serverless-dynamodb';

@Injectable()
export class DynamoDbMapper {
  constructor(private readonly dynamoDb: DynamoDB) {}
}
```

The DynamoDB data mapper provides a DynamoDB client that we can use to access DynamoDB.

To use the DynamoDB data mapper, we need to create a DynamoDB table. We can do this using the AWS Management Console.

Once the DynamoDB table is created, we need to create a Nest.js module that imports the DynamoDB data mapper.

```typescript
import { Module } from '@nestjs/common';
import { DynamoDbMapper } from './dynamodb-mapper.service';

@Module({
  providers: [DynamoDbMapper],
  exports: [DynamoDbMapper],
})
export class DynamoDbModule {}
```

Now that we have created the DynamoDB data mapper, we can use it to access DynamoDB from our Nest.js application.

## Using Nest.js with Google Cloud Firestore

Google Cloud Firestore is a popular serverless database. It is a fast and scalable NoSQL database. Firestore is a great choice for serverless applications that need a fast and scalable database.

To use Firestore with Nest.js, we need to install the @nestjs/cloud-firestore package. This package provides a Firestore data mapper for Nest.js.

```bash
$ npm install @nestjs/cloud-firestore
```

Once the package is installed, we can create a Firestore data mapper.

```typescript
import { Firestore } from '@nestjs/cloud-firestore';

@Injectable()
export class FirestoreMapper {
  constructor(private readonly firestore: Firestore) {}
}
```

The Firestore data mapper provides a Firestore client that we can use to access Firestore.

To use the Firestore data mapper, we need to create a Firestore database. We can do this using the Google Cloud Console.

Once the Firestore database is created, we need to create a Nest.js module that imports the Firestore data mapper.

```typescript
import { Module } from '@nestjs/common';
import { FirestoreMapper } from './firestore-mapper.service';

@Module({
  providers: [FirestoreMapper],
  exports: [FirestoreMapper],
})
export class FirestoreModule {}
```

Now that we have created the Firestore data mapper, we can use it to access Firestore from our Nest.js application.

## Deploying Nest.js to AWS Lambda

AWS Lambda is a popular serverless platform. It is a great choice for serverless applications that need to scale quickly.

To deploy Nest.js to AWS Lambda, we need to install the @nestjs/serverless package. This package provides a Nest.js serverless adapter.

```bash
$ npm install @nestjs/serverless
```

Once the package is installed, we can create a Nest.js serverless adapter.

```typescript
import { ServerlessAdapter } from '@nestjs/serverless';

@Injectable()
export class ServerlessAdapter extends ServerlessAdapter {}
```

The ServerlessAdapter provides an Express.js server that we can use to run our Nest.js application on AWS Lambda.

To use the ServerlessAdapter, we need to create an AWS Lambda function. We can do this using the AWS Management Console.

Once the AWS Lambda function is created, we need to create a Nest.js module that imports the ServerlessAdapter.

```typescript
import { Module } from '@nestjs/common';
import { ServerlessAdapter } from './serverless-adapter.service';

@Module({
  providers: [ServerlessAdapter],
  exports: [ServerlessAdapter],
})
export class ServerlessModule {}
```

Now that we have created the ServerlessAdapter, we can use it to deploy our Nest.js application to AWS Lambda.