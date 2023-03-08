---
title: NoSQL 데이터베이스 관리를 위해 AWS DynamoDB와 함께 TypeScript 사용
description: 
published: true
date: 2023-01-31T21:04:49.381Z
tags: 
editor: markdown
dateCreated: 2023-01-31T21:04:47.781Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Using TypeScript with AWS DynamoDB for NoSQL Database Management***English** version of this document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-aws-dynamodb-for-nosql-database-management)
{.links-list}


# NoSQL 데이터베이스 관리를 위해 AWS DynamoDB와 함께 TypeScript 사용

DynamoDB는 Amazon Web Services(AWS)에서 제공하는 강력한 NoSQL 데이터베이스 서비스입니다. 빠르고 확장 가능하며 고가용성 및 보안을 제공합니다. DynamoDB는 TypeScript를 비롯한 다양한 프로그래밍 언어와 함께 사용할 수 있습니다. 이 기사에서는 DynamoDB에서 TypeScript를 사용하는 방법을 살펴보겠습니다.

## DynamoDB란 무엇입니까?

DynamoDB는 Amazon Web Services(AWS)에서 제공하는 빠르고 확장 가능한 NoSQL 데이터베이스 서비스입니다. DynamoDB 테이블에 데이터를 저장하고 검색하는 데 사용됩니다. DynamoDB는 관리형 서비스입니다. 즉, AWS가 사용자 대신 인프라와 보안을 관리합니다. DynamoDB는 고가용성과 짧은 지연 시간이 필요한 애플리케이션에 적합합니다.

## 타입스크립트란?

TypeScript는 JavaScript의 상위 집합인 프로그래밍 언어입니다. TypeScript는 정적으로 유형이 지정됩니다. 즉, 변수에는 컴파일 시간에 확인되는 유형이 있습니다. 이것은 코드의 오류를 방지하는 데 도움이 될 수 있습니다. TypeScript는 객체 지향이기도 합니다. 즉, 클래스와 인터페이스를 지원합니다.

## DynamoDB에서 TypeScript 사용

DynamoDB에서 TypeScript를 사용하는 방법에는 두 가지가 있습니다.

1. DynamoDB JavaScript SDK를 사용합니다.
2. DynamoDB TypeScript SDK를 사용합니다.

### DynamoDB JavaScript SDK 사용

DynamoDB JavaScript SDK는 TypeScript와 함께 사용할 수 있습니다. TypeScript와 함께 DynamoDB JavaScript SDK를 사용하려면 유형 정의 파일을 사용해야 합니다. 유형 정의 파일은 JavaScript 라이브러리의 유형을 포함하는 파일입니다. DynamoDB JavaScript SDK 유형 정의 파일은 여기에서 찾을 수 있습니다.

https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/aws-sdk/index.d.ts

TypeScript와 함께 DynamoDB JavaScript SDK를 사용하려면 다음 종속성을 설치해야 합니다.

* aws-sdk
* @유형/aws-sdk

npm을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install aws-sdk @types/aws-sdk
```

종속성을 설치했으면 DynamoDB JavaScript SDK를 TypeScript 코드로 가져올 수 있습니다.

```typescript
import * as AWS from 'aws-sdk';
```

그런 다음 DynamoDB JavaScript SDK를 TypeScript와 함께 사용할 수 있습니다. 예를 들어 다음 코드는 DynamoDB 테이블을 생성하는 방법을 보여줍니다.

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

### DynamoDB TypeScript SDK 사용

DynamoDB TypeScript SDK는 TypeScript 유형을 제공하는 DynamoDB JavaScript SDK를 둘러싼 래퍼입니다. DynamoDB TypeScript SDK는 여기에서 찾을 수 있습니다.

https://github.com/types/aws-dynamodb-data-types

DynamoDB TypeScript SDK를 사용하려면 다음 종속성을 설치해야 합니다.

* aws-sdk
* @유형/aws-sdk
* dynamodb 데이터 유형

npm을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install aws-sdk @types/aws-sdk dynamodb-data-types
```

종속성을 설치했으면 DynamoDB TypeScript SDK를 TypeScript 코드로 가져올 수 있습니다.

```typescript
import * as AWS from 'aws-sdk';
import { DynamoDB } from 'dynamodb-data-types';
```

그런 다음 DynamoDB TypeScript SDK를 TypeScript와 함께 사용할 수 있습니다. 예를 들어 다음 코드는 DynamoDB 테이블을 생성하는 방법을 보여줍니다.

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

## 결론

이 기사에서는 DynamoDB에서 TypeScript를 사용하는 방법을 살펴보았습니다. DynamoDB에서 TypeScript를 사용하는 방법에는 DynamoDB JavaScript SDK를 사용하거나 DynamoDB TypeScript SDK를 사용하는 두 가지 방법이 있습니다.