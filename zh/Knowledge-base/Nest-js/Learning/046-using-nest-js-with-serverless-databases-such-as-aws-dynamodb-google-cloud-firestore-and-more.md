---
title: 046：将 Nest.js 与无服务器数据库（例如 AWS DynamoDB、Google Cloud Firestore 等）结合使用
description: 
published: true
date: 2023-02-11T22:55:34.659Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:55:27.839Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [046: Using Nest.js with serverless databases such as AWS DynamoDB, Google Cloud Firestore, and more***English** document is available*](/en/Knowledge-base/Nest-js/Learning/046-using-nest-js-with-serverless-databases-such-as-aws-dynamodb-google-cloud-firestore-and-more)
{.links-list}


# 将 Nest.js 与无服务器数据库（如 AWS DynamoDB、Google Cloud Firestore 等）一起使用

Nest.js 是用于构建服务器端应用程序的强大框架。它基于 TypeScript 和 Node.js，并使用 Express.js 框架。 Nest.js 是构建无服务器应用程序的绝佳选择，因为它易于使用并且对 TypeScript 有很好的支持。

在本文中，我们将学习如何将 Nest.js 与无服务器数据库（例如 AWS DynamoDB、Google Cloud Firestore 等）结合使用。我们还将学习如何将我们的 Nest.js 应用程序部署到 AWS Lambda。

## 将 Nest.js 与 AWS DynamoDB 结合使用

AWS DynamoDB 是一种流行的无服务器数据库。它是一个快速且可扩展的 NoSQL 数据库。 DynamoDB 是需要快速且可扩展的数据库的无服务器应用程序的绝佳选择。

要将 DynamoDB 与 Nest.js 一起使用，我们需要安装 @nestjs/aws-serverless-dynamodb 包。这个包为 Nest.js 提供了一个 DynamoDB 数据映射器。

```bash
$ npm install @nestjs/aws-serverless-dynamodb
```

安装包后，我们可以创建 DynamoDB 数据映射器。

```typescript
import { DynamoDB } from '@nestjs/aws-serverless-dynamodb';

@Injectable()
export class DynamoDbMapper {
  constructor(private readonly dynamoDb: DynamoDB) {}
}
```

DynamoDB 数据映射器提供了一个 DynamoDB 客户端，我们可以使用它来访问 DynamoDB。

要使用 DynamoDB 数据映射器，我们需要创建一个 DynamoDB 表。我们可以使用 AWS 管理控制台执行此操作。

创建 DynamoDB 表后，我们需要创建一个导入 DynamoDB 数据映射器的 Nest.js 模块。

```typescript
import { Module } from '@nestjs/common';
import { DynamoDbMapper } from './dynamodb-mapper.service';

@Module({
  providers: [DynamoDbMapper],
  exports: [DynamoDbMapper],
})
export class DynamoDbModule {}
```

现在我们已经创建了 DynamoDB 数据映射器，我们可以使用它从我们的 Nest.js 应用程序访问 DynamoDB。

## 将 Nest.js 与 Google Cloud Firestore 结合使用

Google Cloud Firestore 是一种流行的无服务器数据库。它是一个快速且可扩展的 NoSQL 数据库。 Firestore 是需要快速且可扩展的数据库的无服务器应用程序的绝佳选择。

要将 Firestore 与 Nest.js 一起使用，我们需要安装 @nestjs/cloud-firestore 包。这个包为 Nest.js 提供了一个 Firestore 数据映射器。

```bash
$ npm install @nestjs/cloud-firestore
```

安装包后，我们可以创建一个 Firestore 数据映射器。

```typescript
import { Firestore } from '@nestjs/cloud-firestore';

@Injectable()
export class FirestoreMapper {
  constructor(private readonly firestore: Firestore) {}
}
```

Firestore 数据映射器提供了一个 Firestore 客户端，我们可以使用它来访问 Firestore。

要使用 Firestore 数据映射器，我们需要创建一个 Firestore 数据库。我们可以使用 Google Cloud Console 来做到这一点。

创建 Firestore 数据库后，我们需要创建一个导入 Firestore 数据映射器的 Nest.js 模块。

```typescript
import { Module } from '@nestjs/common';
import { FirestoreMapper } from './firestore-mapper.service';

@Module({
  providers: [FirestoreMapper],
  exports: [FirestoreMapper],
})
export class FirestoreModule {}
```

现在我们已经创建了 Firestore 数据映射器，我们可以使用它从我们的 Nest.js 应用程序访问 Firestore。

## 将 Nest.js 部署到 AWS Lambda

AWS Lambda 是一种流行的无服务器平台。对于需要快速扩展的无服务器应用程序来说，这是一个很好的选择。

要将 Nest.js 部署到 AWS Lambda，我们需要安装 @nestjs/serverless 包。这个包提供了一个 Nest.js 无服务器适配器。

```bash
$ npm install @nestjs/serverless
```

安装包后，我们可以创建一个 Nest.js 无服务器适配器。

```typescript
import { ServerlessAdapter } from '@nestjs/serverless';

@Injectable()
export class ServerlessAdapter extends ServerlessAdapter {}
```

ServerlessAdapter 提供了一个 Express.js 服务器，我们可以使用它在 AWS Lambda 上运行我们的 Nest.js 应用程序。

要使用 ServerlessAdapter，我们需要创建一个 AWS Lambda 函数。我们可以使用 AWS 管理控制台执行此操作。

创建 AWS Lambda 函数后，我们需要创建一个导入 ServerlessAdapter 的 Nest.js 模块。

```typescript
import { Module } from '@nestjs/common';
import { ServerlessAdapter } from './serverless-adapter.service';

@Module({
  providers: [ServerlessAdapter],
  exports: [ServerlessAdapter],
})
export class ServerlessModule {}
```

现在我们已经创建了 ServerlessAdapter，我们可以使用它来将我们的 Nest.js 应用程序部署到 AWS Lambda。