---
title: 서버리스 개발을 위해 TypeScript를 AWS 서비스와 통합
description: 
published: true
date: 2023-02-15T15:56:17.445Z
tags: 
editor: markdown
dateCreated: 2023-02-15T15:56:15.437Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with AWS Services for Serverless Development***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-aws-services-for-serverless-development)
{.links-list}


# 서버리스 개발을 위해 TypeScript를 AWS 서비스와 통합

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다. TypeScript는 JavaScript에 익숙한 개발자가 배우기 쉽습니다. 이 기사에서는 TypeScript를 AWS 서비스와 함께 사용하여 서버리스 애플리케이션을 구축하는 방법을 살펴봅니다.

## TypeScript 설정

먼저 개발 머신에 TypeScript를 설정해야 합니다. Node.js 패키지 관리자(npm)를 사용하여 TypeScript를 설치합니다.

```
npm install -g typescript
```

TypeScript가 설치되면 TypeScript 버전을 확인하여 설치를 확인할 수 있습니다.

```
tsc --version
```

## JavaScript용 AWS SDK 설정

이제 TypeScript가 설치되었으므로 JavaScript용 AWS SDK를 설치할 수 있습니다. SDK는 TypeScript 코드에서 AWS 서비스와 상호 작용할 수 있는 API를 제공합니다. npm을 사용하여 SDK를 설치할 수도 있습니다.

```
npm install aws-sdk
```

## TypeScript 코드 작성

AWS 서비스와 상호 작용하는 TypeScript 코드를 작성해 보겠습니다. AWS 계정의 모든 S3 버킷을 나열하는 간단한 프로그램을 작성하여 시작하겠습니다.

먼저 TypeScript 코드에서 AWS SDK를 가져와야 합니다.

```typescript
import * as AWS from 'aws-sdk';
```

다음으로 AWS 자격 증명으로 AWS SDK를 구성해야 합니다. `AWS.config.credentials` 속성을 설정하여 이를 수행할 수 있습니다. 자격 증명을 설정하는 방법은 다양하지만 간단하게 하기 위해 'accessKeyId' 및 'secretAccessKey' 속성을 직접 설정합니다.

```typescript
AWS.config.credentials = new AWS.Credentials({
  accessKeyId: '<Your Access Key>',
  secretAccessKey: '<Your Secret Key>'
});
```

이제 AWS SDK를 가져오고 자격 증명을 구성했으므로 'S3' 서비스의 인스턴스를 생성할 수 있습니다.

```typescript
const s3 = new AWS.S3();
```

'S3' 서비스는 계정의 모든 S3 버킷을 나열하는 데 사용할 수 있는 'listBuckets' 작업을 제공합니다. `listBuckets` 작업은 약속을 반환하므로 `async/await` 키워드를 사용하여 코드를 더 쉽게 읽을 수 있습니다.

```typescript
async function listBuckets() {
  const response = await s3.listBuckets().promise();
  console.log(response.Buckets);
}

listBuckets();
```

`tsc` 명령을 사용하여 TypeScript 코드를 JavaScript로 컴파일할 수 있습니다.

```
tsc main.ts
```

그러면 동일한 디렉토리에 `main.js` 파일이 생성됩니다. Node.js를 사용하여 생성된 JavaScript 파일을 실행할 수 있습니다.

```
node main.js
```

## AWS Lambda와 TypeScript 통합

AWS Lambda는 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 서버리스 컴퓨팅 서비스입니다. Lambda는 기본 컴퓨팅 리소스의 모든 관리를 처리하므로 고객에게 가치를 제공하는 코드 작성에 집중할 수 있습니다.

AWS Lambda는 여러 언어를 지원하지만 Node.js는 Lambda 함수에 가장 많이 사용되는 언어입니다. 이 섹션에서는 TypeScript를 사용하여 Lambda 함수를 생성하는 방법을 살펴봅니다.

Lambda 함수를 위한 새 디렉터리를 생성하여 시작하겠습니다. 우리는 이 디렉토리를 `lambda-ts`라고 부를 것입니다.

```
mkdir lambda-ts
cd lambda-ts
```

다음으로 npm을 사용하여 디렉토리를 Node.js 프로젝트로 초기화합니다.

```
npm init -y
```

이제 TypeScript 컴파일러와 AWS SDK를 프로젝트의 종속 항목으로 설치해야 합니다.

```
npm install --save-dev typescript
npm install aws-sdk
```

이제 `lambda-ts` 디렉토리에 `tsconfig.json` 파일을 생성하여 TypeScript 컴파일러를 구성할 수 있습니다.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

TypeScript 코드를 저장하기 위해 `lambda-ts` 디렉토리에 `src` 디렉토리도 생성합니다.

```
mkdir src
```

이제 `src` 디렉토리에 TypeScript 파일 `src/index.ts`를 만들 수 있습니다. 이 파일에는 Lambda 함수 코드가 포함됩니다.

```typescript
import * as AWS from 'aws-sdk';

export async function handler(event: any, context: any) {
  console.log('Hello, world!');
}
```

`tsc` 명령을 사용하여 TypeScript 코드를 JavaScript로 컴파일할 수 있습니다.

```
tsc
```

그러면 `lambda-ts` 디렉토리에 `dist/index.js` 파일이 생성됩니다. 이제 `dist` 디렉터리의 콘텐츠를 압축하고 압축 파일을 AWS Lambda에 업로드할 수 있습니다.

```
cd dist
zip -r ../function.zip .
```

이제 AWS Lambda 콘솔을 사용하여 Lambda 함수를 테스트할 수 있습니다.

## AWS DynamoDB와 TypeScript 통합

AWS DynamoDB는 빠르고 확장 가능한 NoSQL 데이터베이스 서비스입니다. 이 섹션에서는 DynamoDB에서 TypeScript를 사용하는 방법을 살펴보겠습니다.

DynamoDB 애플리케이션을 위한 새 디렉터리를 생성하는 것부터 시작하겠습니다. 이 디렉토리를 `dynamodb-ts`라고 합니다.

```
mkdir dynamodb-ts
cd dynamodb-ts
```

다음으로 npm을 사용하여 디렉토리를 Node.js 프로젝트로 초기화합니다.

```
npm init -y
```

이제 TypeScript 컴파일러와 AWS SDK를 프로젝트의 종속 항목으로 설치해야 합니다.

```
npm install --save-dev typescript
npm install aws-sdk
```

이제 `dynamodb-ts` 디렉토리에 `tsconfig.json` 파일을 생성하여 TypeScript 컴파일러를 구성할 수 있습니다.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

TypeScript 코드를 저장하기 위해 `dynamodb-ts` 디렉토리에 `src` 디렉토리도 생성합니다.

```
mkdir src
```

이제 `src` 디렉토리에 TypeScript 파일 `src/index.ts`를 만들 수 있습니다. 이 파일에는 DynamoDB 코드가 포함됩니다.

```typescript
import * as AWS from 'aws-sdk';

AWS.config.update({ region: 'us-east-1' });

const dynamodb = new AWS.DynamoDB();

async function createTable() {
  const params = {
    TableName: 'Users',
    KeySchema: [
      { AttributeName: 'email', KeyType: 'HASH' } //Partition key
    ],
    AttributeDefinitions: [
      { AttributeName: 'email', AttributeType: 'S' }
    ],
    ProvisionedThroughput: {
      ReadCapacityUnits: 10,
      WriteCapacityUnits: 10
    }
  };

  try {
    const data = await dynamodb.createTable(params).promise();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

createTable();
```

`tsc` 명령을 사용하여 TypeScript 코드를 JavaScript로 컴파일할 수 있습니다.

```
tsc
```

이렇게 하면 `dynamodb-ts` 디렉터리에 `dist/index.js` 파일이 생성됩니다. 이제 Node.js를 사용하여 생성된 JavaScript 파일을 실행할 수 있습니다.

```
node dist/index.js
```

## AWS S3와 TypeScript 통합

AWS S3는 고가용성과 내구성을 제공하는 간단한 스토리지 서비스입니다. 이 섹션에서는 S3에서 TypeScript를 사용하는 방법을 살펴봅니다.

S3 애플리케이션을 위한 새 디렉터리를 만드는 것으로 시작하겠습니다. 우리는 이 디렉토리를 `s3-ts`라고 부를 것입니다.

```
mkdir s3-ts
cd s3-ts
```

다음으로 npm을 사용하여 디렉토리를 Node.js 프로젝트로 초기화합니다.

```
npm init -y
```

이제 TypeScript 컴파일러와 AWS SDK를 프로젝트의 종속 항목으로 설치해야 합니다.

```
npm install --save-dev typescript
npm install aws-sdk
```

이제 `s3-ts` 디렉토리에 `tsconfig.json` 파일을 생성하여 TypeScript 컴파일러를 구성할 수 있습니다.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

TypeScript 코드를 저장하기 위해 `s3-ts` 디렉토리에 `src` 디렉토리도 생성합니다.

```
mkdir src
```

이제 `src` 디렉토리에 TypeScript 파일 `src/index.ts`를 만들 수 있습니다. 이 파일에는 S3 코드가 포함됩니다.

```typescript
import * as AWS from 'aws-sdk';

AWS.config.update({ region: 'us-east-1' });

const s3 = new AWS.S3();

async function putObject() {
  const params = {
    Bucket: '<Your Bucket Name>',
    Key: 'test.txt',
    Body: 'Hello, world!'
  };

  try {
    const data = await s3.putObject(params).promise();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

putObject();
```

`tsc` 명령을 사용하여 TypeScript 코드를 JavaScript로 컴파일할 수 있습니다.

```
tsc
```

이렇게 하면 `s3-ts` 디렉토리에 `dist/index.js` 파일이 생성됩니다. 이제 Node.js를 사용하여 생성된 JavaScript 파일을 실행할 수 있습니다.

```
node dist/index.js
```

## 더 읽을거리

- [타입스크립트](https://www.typescriptlang.org/)
- [JavaScript용 AWS SDK](https://aws.amazon.com/sdk-for-node-js/)
- [AWS 람다](https://aws.amazon.com/lambda/)
- [AWS DynamoDB](https://aws.amazon.com/dynamodb/)
- [AWS S3](https://aws.amazon.com/s3/)