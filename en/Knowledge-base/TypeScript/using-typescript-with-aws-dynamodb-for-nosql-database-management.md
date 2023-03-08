---
title: Using TypeScript with AWS DynamoDB for NoSQL Database Management
description: 
published: true
date: 2023-01-31T21:04:51.485Z
tags: 
editor: markdown
dateCreated: 2023-01-31T21:04:47.781Z
---

- [NoSQL 데이터베이스 관리를 위해 AWS DynamoDB와 함께 TypeScript 사용***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/using-typescript-with-aws-dynamodb-for-nosql-database-management)
{.links-list}
- [NoSQL データベース管理のために AWS DynamoDB で TypeScript を使用する***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/using-typescript-with-aws-dynamodb-for-nosql-database-management)
{.links-list}
- [使用 TypeScript 和 AWS DynamoDB 进行 NoSQL 数据库管理***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/using-typescript-with-aws-dynamodb-for-nosql-database-management)
{.links-list}


# Using TypeScript with AWS DynamoDB for NoSQL Database Management

DynamoDB is a powerful NoSQL database service provided by Amazon Web Services (AWS). It is fast, scalable, and provides high availability and security. DynamoDB can be used with various programming languages, including TypeScript. In this article, we will look at how to use TypeScript with DynamoDB.

## What is DynamoDB?

DynamoDB is a fast and scalable NoSQL database service provided by Amazon Web Services (AWS). It is used to store and retrieve data in a DynamoDB table. DynamoDB is a managed service, meaning that AWS manages the infrastructure and security for you. DynamoDB is a good choice for applications that require high availability and low latency.

## What is TypeScript?

TypeScript is a programming language that is a superset of JavaScript. TypeScript is statically typed, meaning that variables have a type that is checked at compile time. This can help to prevent errors in your code. TypeScript is also object-oriented, meaning that it supports classes and interfaces.

## Using TypeScript with DynamoDB

There are two ways to use TypeScript with DynamoDB:

1. Use the DynamoDB JavaScript SDK.
2. Use the DynamoDB TypeScript SDK.

### Using the DynamoDB JavaScript SDK

The DynamoDB JavaScript SDK can be used with TypeScript. To use the DynamoDB JavaScript SDK with TypeScript, you will need to use a type definition file. A type definition file is a file that contains the types for a JavaScript library. The DynamoDB JavaScript SDK type definition file can be found here:

https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/aws-sdk/index.d.ts

To use the DynamoDB JavaScript SDK with TypeScript, you will need to install the following dependencies:

* aws-sdk
* @types/aws-sdk

You can install these dependencies using npm:

```
npm install aws-sdk @types/aws-sdk
```

Once you have installed the dependencies, you can import the DynamoDB JavaScript SDK into your TypeScript code:

```typescript
import * as AWS from 'aws-sdk';
```

You can then use the DynamoDB JavaScript SDK with TypeScript. For example, the following code shows how to create a DynamoDB table:

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

### Using the DynamoDB TypeScript SDK

The DynamoDB TypeScript SDK is a wrapper around the DynamoDB JavaScript SDK that provides TypeScript types. The DynamoDB TypeScript SDK can be found here:

https://github.com/types/aws-dynamodb-data-types

To use the DynamoDB TypeScript SDK, you will need to install the following dependencies:

* aws-sdk
* @types/aws-sdk
* dynamodb-data-types

You can install these dependencies using npm:

```
npm install aws-sdk @types/aws-sdk dynamodb-data-types
```

Once you have installed the dependencies, you can import the DynamoDB TypeScript SDK into your TypeScript code:

```typescript
import * as AWS from 'aws-sdk';
import { DynamoDB } from 'dynamodb-data-types';
```

You can then use the DynamoDB TypeScript SDK with TypeScript. For example, the following code shows how to create a DynamoDB table:

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

## Conclusion

In this article, we have looked at how to use TypeScript with DynamoDB. We have seen that there are two ways to use TypeScript with DynamoDB: using the DynamoDB JavaScript SDK, or using the DynamoDB TypeScript SDK.