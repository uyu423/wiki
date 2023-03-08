---
title: 将 TypeScript 与 AWS 服务集成以实现无服务器开发
description: 
published: true
date: 2023-02-15T15:56:17.438Z
tags: 
editor: markdown
dateCreated: 2023-02-15T15:56:15.437Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Integrating TypeScript with AWS Services for Serverless Development***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-aws-services-for-serverless-development)
{.links-list}


# 将 TypeScript 与 AWS 服务集成以进行无服务器开发

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它提供类、模块和接口来帮助您构建健壮的组件。对于熟悉 JavaScript 的开发人员来说，TypeScript 很容易学习。在本文中，我们将探讨如何将 TypeScript 与 AWS 服务结合使用来构建无服务器应用程序。

## 设置打字稿

首先，我们需要在我们的开发机器上设置 TypeScript。我们将使用 Node.js 包管理器 (npm) 来安装 TypeScript。

```
npm install -g typescript
```

安装 TypeScript 后，我们可以通过检查 TypeScript 版本来验证安装。

```
tsc --version
```

## 设置适用于 JavaScript 的 AWS 开发工具包

现在我们已经安装了 TypeScript，我们可以安装适用于 JavaScript 的 AWS 开发工具包。 SDK 将为我们提供 API，以便从我们的 TypeScript 代码与 AWS 服务进行交互。我们也可以使用 npm 安装 SDK。

```
npm install aws-sdk
```

## 编写 TypeScript 代码

让我们编写一些 TypeScript 代码来与 AWS 服务交互。我们将首先编写一个简单的程序来列出我们 AWS 账户中的所有 S3 存储桶。

首先，我们需要在 TypeScript 代码中导入 AWS SDK。

```typescript
import * as AWS from 'aws-sdk';
```

接下来，我们需要使用我们的 AWS 凭证配置 AWS SDK。我们可以通过设置 AWS.config.credentials 属性来做到这一点。设置凭据的方法有多种，但为了简单起见，我们将直接设置 `accessKeyId` 和 `secretAccessKey` 属性。

```typescript
AWS.config.credentials = new AWS.Credentials({
  accessKeyId: '<Your Access Key>',
  secretAccessKey: '<Your Secret Key>'
});
```

现在我们已经导入了 AWS SDK 并配置了我们的凭据，我们可以创建“S3”服务的实例。

```typescript
const s3 = new AWS.S3();
```

`S3` 服务提供了一个 `listBuckets` 操作，我们可以使用它来列出我们帐户中的所有 S3 存储桶。 `listBuckets` 操作返回一个 promise，因此我们可以使用 `async/await` 关键字来使我们的代码更易于阅读。

```typescript
async function listBuckets() {
  const response = await s3.listBuckets().promise();
  console.log(response.Buckets);
}

listBuckets();
```

我们可以使用 `tsc` 命令将 TypeScript 代码编译为 JavaScript。

```
tsc main.ts
```

这将在同一目录中生成一个 `main.js` 文件。我们可以使用 Node.js 运行生成的 JavaScript 文件。

```
node main.js
```

## 将 TypeScript 与 AWS Lambda 集成

AWS Lambda 是一种无服务器计算服务，让您无需预置或管理服务器即可运行代码。 Lambda 处理底层计算资源的所有管理，因此您可以专注于编写为客户带来价值的代码。

AWS Lambda 支持多种语言，但 Node.js 是 Lambda 函数最流行的语言。在本节中，我们将了解如何使用 TypeScript 创建 Lambda 函数。

我们将从为 Lambda 函数创建一个新目录开始。我们将此目录称为“lambda-ts”。

```
mkdir lambda-ts
cd lambda-ts
```

接下来，我们将使用 npm 将目录初始化为 Node.js 项目。

```
npm init -y
```

现在，我们需要安装 TypeScript 编译器和 AWS SDK 作为项目的依赖项。

```
npm install --save-dev typescript
npm install aws-sdk
```

我们现在可以在 lambda-ts 目录中创建一个 tsconfig.json 文件来配置 TypeScript 编译器。

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

我们还将在 `lambda-ts` 目录中创建一个 `src` 目录来存储我们的 TypeScript 代码。

```
mkdir src
```

我们现在可以在 `src` 目录中创建一个 TypeScript 文件 `src/index.ts`。该文件将包含我们的 Lambda 函数代码。

```typescript
import * as AWS from 'aws-sdk';

export async function handler(event: any, context: any) {
  console.log('Hello, world!');
}
```

我们可以使用 `tsc` 命令将 TypeScript 代码编译为 JavaScript。

```
tsc
```

这将在 lambda-ts 目录中生成一个 dist/index.js 文件。我们现在可以压缩 dist 目录的内容并将压缩文件上传到 AWS Lambda。

```
cd dist
zip -r ../function.zip .
```

我们现在可以使用 AWS Lambda 控制台测试我们的 Lambda 函数。

## 将 TypeScript 与 AWS DynamoDB 集成

AWS DynamoDB 是一种快速且可扩展的 NoSQL 数据库服务。在本节中，我们将了解如何将 TypeScript 与 DynamoDB 结合使用。

我们将从为 DynamoDB 应用程序创建一个新目录开始。我们将此目录称为“dynamodb-ts”。

```
mkdir dynamodb-ts
cd dynamodb-ts
```

接下来，我们将使用 npm 将目录初始化为 Node.js 项目。

```
npm init -y
```

现在，我们需要安装 TypeScript 编译器和 AWS SDK 作为项目的依赖项。

```
npm install --save-dev typescript
npm install aws-sdk
```

我们现在可以在 dynamodb-ts 目录中创建一个 tsconfig.json 文件来配置 TypeScript 编译器。

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

我们还将在 `dynamodb-ts` 目录中创建一个 `src` 目录来存储我们的 TypeScript 代码。

```
mkdir src
```

我们现在可以在 `src` 目录中创建一个 TypeScript 文件 `src/index.ts`。该文件将包含我们的 DynamoDB 代码。

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

我们可以使用 `tsc` 命令将 TypeScript 代码编译为 JavaScript。

```
tsc
```

这将在 dynamodb-ts 目录中生成一个 dist/index.js 文件。我们现在可以使用 Node.js 运行生成的 JavaScript 文件。

```
node dist/index.js
```

## 将 TypeScript 与 AWS S3 集成

AWS S3 是一种提供高可用性和持久性的简单存储服务。在本节中，我们将了解如何将 TypeScript 与 S3 结合使用。

我们将从为我们的 S3 应用程序创建一个新目录开始。我们将此目录称为“s3-ts”。

```
mkdir s3-ts
cd s3-ts
```

接下来，我们将使用 npm 将目录初始化为 Node.js 项目。

```
npm init -y
```

现在，我们需要安装 TypeScript 编译器和 AWS SDK 作为项目的依赖项。

```
npm install --save-dev typescript
npm install aws-sdk
```

我们现在可以在 s3-ts 目录中创建一个 tsconfig.json 文件来配置 TypeScript 编译器。

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist"
  }
}
```

我们还将在 s3-ts 目录中创建一个 src 目录来存储我们的 TypeScript 代码。

```
mkdir src
```

我们现在可以在 `src` 目录中创建一个 TypeScript 文件 `src/index.ts`。该文件将包含我们的 S3 代码。

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

我们可以使用 `tsc` 命令将 TypeScript 代码编译为 JavaScript。

```
tsc
```

这将在 `s3-ts` 目录中生成一个 `dist/index.js` 文件。我们现在可以使用 Node.js 运行生成的 JavaScript 文件。

```
node dist/index.js
```

## 延伸阅读

- [打字稿](https://www.typescriptlang.org/)
- [适用于 JavaScript 的 AWS 开发工具包](https://aws.amazon.com/sdk-for-node-js/)
- [AWS 拉姆达](https://aws.amazon.com/lambda/)
- [AWS DynamoDB](https://aws.amazon.com/dynamodb/)
- [AWS S3](https://aws.amazon.com/s3/)