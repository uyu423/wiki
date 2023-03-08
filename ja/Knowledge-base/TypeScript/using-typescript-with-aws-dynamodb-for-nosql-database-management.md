---
title: NoSQL データベース管理のために AWS DynamoDB で TypeScript を使用する
description: 
published: true
date: 2023-01-31T21:04:49.405Z
tags: 
editor: markdown
dateCreated: 2023-01-31T21:04:47.788Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Using TypeScript with AWS DynamoDB for NoSQL Database Management***English** version of this document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-aws-dynamodb-for-nosql-database-management)
{.links-list}


# NoSQL データベースを管理するために AWS DynamoDB で TypeScript を使用する

DynamoDBは、Amazon Web Services（AWS）が提供する強力なNoSQLデータベースサービスです。迅速でスケーラブルで高可用性とセキュリティを提供します。 DynamoDBは、TypeScriptを含むさまざまなプログラミング言語で使用できます。この記事では、DynamoDBでTypeScriptを使用する方法について説明します。

## DynamoDBとは何ですか？

DynamoDBは、Amazon Web Services（AWS）が提供する迅速でスケーラブルなNoSQLデータベースサービスです。 DynamoDBテーブルにデータを保存して取得するために使用されます。 DynamoDBはマネージドサービスです。つまり、AWS はユーザーの代わりにインフラストラクチャとセキュリティを管理します。 DynamoDBは、高可用性と短い遅延時間を必要とするアプリケーションに適しています。

##タイプスクリプトとは何ですか？

TypeScriptは、JavaScriptの上位セットであるプログラミング言語です。 TypeScriptは静的に型指定されます。つまり、変数にはコンパイル時に確認される型があります。これはコードのエラーを防ぐのに役立ちます。 TypeScriptはオブジェクト指向でもあります。つまり、クラスとインタフェースをサポートします。

## DynamoDBでTypeScriptを使用する

DynamoDBでTypeScriptを使用する方法は2つあります。

1. DynamoDB JavaScript SDKを使用します。
2. DynamoDB TypeScript SDKを使用します。

### DynamoDB JavaScript SDKの使用

DynamoDB JavaScript SDK は TypeScript で使用できます。 TypeScriptでDynamoDB JavaScript SDKを使用するには、タイプ定義ファイルを使用する必要があります。型定義ファイルは、JavaScriptライブラリの型を含むファイルです。 DynamoDB JavaScript SDKタイプ定義ファイルはここにあります。

https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/aws-sdk/index.d.ts

TypeScriptでDynamoDB JavaScript SDKを使用するには、次の依存関係をインストールする必要があります。

* aws-sdk
* @タイプ/aws-sdk

npm を使用してこれらの依存関係をインストールできます。

```
npm install aws-sdk @types/aws-sdk
```

依存関係をインストールしたら、DynamoDB JavaScript SDKをTypeScriptコードにインポートできます。

```typescript
import * as AWS from 'aws-sdk';
```

その後、DynamoDB JavaScript SDKをTypeScriptで使用できます。たとえば、次のコードはDynamoDBテーブルを作成する方法を示しています。

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
    if(err){
        console.error（err）;
    }else{
        console.log（data）;
    }
}）;
```

### DynamoDB TypeScript SDKの使用

DynamoDB TypeScript SDKは、TypeScriptタイプを提供するDynamoDB JavaScript SDKを囲むラッパーです。 DynamoDB TypeScript SDK はここにあります。

https://github.com/types/aws-dynamodb-data-types

DynamoDB TypeScript SDKを使用するには、次の依存関係をインストールする必要があります。

* aws-sdk
* @タイプ/aws-sdk
*dynamodbデータ型

npm を使用してこれらの依存関係をインストールできます。

```
npm install aws-sdk @types/aws-sdk dynamodb-data-types
```

依存関係をインストールしたら、DynamoDB TypeScript SDKをTypeScriptコードにインポートできます。

```typescript
import * as AWS from 'aws-sdk';
import { DynamoDB } from 'dynamodb-data-types';
```

その後、DynamoDB TypeScript SDKをTypeScriptで使用できます。たとえば、次のコードはDynamoDBテーブルを作成する方法を示しています。

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
    if(err){
        console.error（err）;
    }else{
        console.log（data）;
    }
}）;
```

##結論

この記事では、DynamoDBでTypeScriptを使用する方法について説明しました。 DynamoDBでTypeScriptを使用する方法には、DynamoDB JavaScript SDKを使用するか、DynamoDB TypeScript SDKを使用する2つの方法があります。