---
title: 使用 TypeScript 和 AWS DynamoDB 进行 NoSQL 数据库管理
description: 
published: true
date: 2023-01-31T21:04:49.405Z
tags: 
editor: markdown
dateCreated: 2023-01-31T21:04:47.788Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Using TypeScript with AWS DynamoDB for NoSQL Database Management***English** version of this document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-aws-dynamodb-for-nosql-database-management)
{.links-list}


# 使用 TypeScript 和 AWS DynamoDB 进行 NoSQL 数据库管理

DynamoDB 是 Amazon Web Services (AWS) 提供的功能强大的 NoSQL 数据库服务。它速度快、可扩展，并提供高可用性和安全性。 DynamoDB 可以与各种编程语言一起使用，包括 TypeScript。在本文中，我们将了解如何将 TypeScript 与 DynamoDB 结合使用。

## 什么是 DynamoDB？

DynamoDB 是由 Amazon Web Services (AWS) 提供的一种快速且可扩展的 NoSQL 数据库服务。它用于在 DynamoDB 表中存储和检索数据。 DynamoDB 是一项托管服务，这意味着 AWS 为您管理基础设施和安全性。对于需要高可用性和低延迟的应用程序，DynamoDB 是一个不错的选择。

## 什么是打字稿？

TypeScript 是一种编程语言，是 JavaScript 的超集。 TypeScript 是静态类型的，这意味着变量具有在编译时检查的类型。这有助于防止代码中出现错误。 TypeScript 也是面向对象的，这意味着它支持类和接口。

## 将 TypeScript 与 DynamoDB 结合使用

有两种方法可以将 TypeScript 与 DynamoDB 结合使用：

1. 使用 DynamoDB JavaScript SDK。
2. 使用 DynamoDB TypeScript SDK。

### 使用 DynamoDB JavaScript SDK

DynamoDB JavaScript SDK 可以与 TypeScript 一起使用。要将 DynamoDB JavaScript SDK 与 TypeScript 结合使用，您需要使用类型定义文件。类型定义文件是包含 JavaScript 库类型的文件。 DynamoDB JavaScript SDK 类型定义文件可在此处找到：

https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/aws-sdk/index.d.ts

要将 DynamoDB JavaScript SDK 与 TypeScript 一起使用，您需要安装以下依赖项：

* aws-sdk
* @types/aws-sdk

您可以使用 npm 安装这些依赖项：

```
npm install aws-sdk @types/aws-sdk
```

安装依赖项后，您可以将 DynamoDB JavaScript SDK 导入到您的 TypeScript 代码中：

```typescript
import * as AWS from 'aws-sdk';
```

然后，您可以将 DynamoDB JavaScript SDK 与 TypeScript 结合使用。例如，以下代码显示了如何创建 DynamoDB 表：

```typescript
const dynamodb = new AWS.DynamoDB();

const params = {
    TableName: 'my-table',
    AttributeDefinitions: [
        {
            AttributeName: 'my-hash-key',
            AttributeType: 'S'
        },
        {
            AttributeName: 'my-range-key',
            AttributeType: 'N'
        }
    ],
    KeySchema: [
        {
            AttributeName: 'my-hash-key',
            KeyType: 'HASH'
        },
        {
            AttributeName: 'my-range-key',
            KeyType: 'RANGE'
        }
    ],
    ProvisionedThroughput: {
        ReadCapacityUnits: 1,
        WriteCapacityUnits: 1
    }
};

dynamodb.createTable(params, (err, data) => {
    if (err) {
        console.error(err);
    } else {
        console.log(data);
    }
});
```

### 使用 DynamoDB TypeScript SDK

DynamoDB TypeScript SDK 是提供 TypeScript 类型的 DynamoDB JavaScript SDK 的包装器。 DynamoDB TypeScript SDK 可以在这里找到：

https://github.com/types/aws-dynamodb-data-types

要使用 DynamoDB TypeScript SDK，您需要安装以下依赖项：

* aws-sdk
* @types/aws-sdk
* dynamodb 数据类型

您可以使用 npm 安装这些依赖项：

```
npm install aws-sdk @types/aws-sdk dynamodb-data-types
```

安装依赖项后，您可以将 DynamoDB TypeScript SDK 导入到您的 TypeScript 代码中：

```typescript
import * as AWS from 'aws-sdk';
import { DynamoDB } from 'dynamodb-data-types';
```

然后，您可以将 DynamoDB TypeScript SDK 与 TypeScript 一起使用。例如，以下代码显示了如何创建 DynamoDB 表：

```typescript
const dynamodb = new AWS.DynamoDB();
const dynamoDbDataTypes = new DynamoDB();

const params = {
    TableName: 'my-table',
    AttributeDefinitions: [
        {
            AttributeName: 'my-hash-key',
            AttributeType: 'S'
        },
        {
            AttributeName: 'my-range-key',
            AttributeType: 'N'
        }
    ],
    KeySchema: [
        {
            AttributeName: 'my-hash-key',
            KeyType: 'HASH'
        },
        {
            AttributeName: 'my-range-key',
            KeyType: 'RANGE'
        }
    ],
    ProvisionedThroughput: {
        ReadCapacityUnits: 1,
        WriteCapacityUnits: 1
    }
};

dynamodb.createTable(params, (err, data) => {
    if (err) {
        console.error(err);
    } else {
        console.log(data);
    }
});
```

## 结论

在本文中，我们了解了如何将 TypeScript 与 DynamoDB 结合使用。我们已经看到有两种方法可以将 TypeScript 与 DynamoDB 结合使用：使用 DynamoDB JavaScript SDK，或使用 DynamoDB TypeScript SDK。