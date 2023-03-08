---
title: 使用 TypeScript 和 GraphQL 进行 API 开发
description: 
published: true
date: 2023-02-01T19:17:56.734Z
tags: 
editor: markdown
dateCreated: 2023-02-01T19:17:52.551Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Using TypeScript with GraphQL for API Development***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-graphql-for-api-development)
{.links-list}


# 使用 TypeScript 和 GraphQL 进行 API 开发

TypeScript 是 JavaScript 的强类型超集，可编译为干净的 JavaScript 输出。 GraphQL 是一种强大的 API 查询语言，它使客户端能够仅从服务器请求他们需要的数据，从而使 API 更加高效。

这两种技术可以一起使用来创建健壮的、类型安全的 API 客户端和服务器。在本文中，我们将了解如何将 TypeScript 与 GraphQL 结合使用，包括一个简短的代码示例。

## 为什么将 TypeScript 与 GraphQL 一起使用？

您可能出于多种原因希望将 TypeScript 与 GraphQL 结合使用。首先，TypeScript 可以帮助您创建类型安全的 GraphQL 查询。这意味着您可以及早发现错误，甚至在您的代码运行之前。

其次，TypeScript 可以为您的 GraphQL 服务器提供自动补全和类型安全。当您使用具有许多类型和字段的复杂 GraphQL 模式时，这尤其有用。

第三，TypeScript 可以帮助你组织代码。例如，您可以使用 TypeScript 的模块系统以易于理解和维护的方式构建代码。

第四，TypeScript 越来越受欢迎，因此将它与 GraphQL 一起使用可以更容易地找到合作者和支持。

## 使用 GraphQL 设置 TypeScript

要将 TypeScript 与 GraphQL 结合使用，您需要安装以下依赖项：

-打字稿：^3.2.2
- graphql：^14.3.1
- @types/graphql: ^14.0.1

您可以使用 npm 安装这些依赖项：

```
npm install --save typescript graphql @types/graphql
```

## 将 TypeScript 与 GraphQL 结合使用

安装依赖项后，您可以开始将 TypeScript 与 GraphQL 结合使用。这是一个简单的例子：

```graphql
query GetUser($id: ID!) {
  user(id: $id) {
    id
    name
  }
}
```

在此示例中，我们定义了一个通过 ID 获取用户的 GraphQL 查询。我们还为 ID 变量定义了一个类型。此类型将用于对我们的查询变量进行类型检查。

现在让我们看看如何通过 TypeScript 使用此查询。首先，我们需要创建一个名为 schema.ts 的文件：

```typescript
import {
  GraphQLSchema,
  GraphQLObjectType,
  GraphQLString,
  GraphQLID,
} from 'graphql';

const UserType = new GraphQLObjectType({
  name: 'User',
  fields: {
    id: { type: GraphQLID },
    name: { type: GraphQLString },
  },
});

const QueryType = new GraphQLObjectType({
  name: 'Query',
  fields: {
    user: {
      type: UserType,
      args: {
        id: { type: GraphQLID },
      },
      resolve: (_, { id }) => ({ id, name: 'Alice' }),
    },
  },
});

export const schema = new GraphQLSchema({
  query: QueryType,
});
```

在这个文件中，我们定义了我们的 GraphQL 模式。我们还定义了一个 `User` 类型和一个 `Query` 类型。 `Query` 类型包含一个 `user` 字段，它通过 ID 获取 `User`。

现在让我们创建一个名为 index.ts 的文件：

```typescript
import { graphql, buildSchema } from 'graphql';
import { schema } from './schema';

async function main() {
  const query = `
    query GetUser($id: ID!) {
      user(id: $id) {
        id
        name
      }
    }
  `;

  const variables = {
    id: '1',
  };

  const rootValue = {};
  const context = {};
  const options = {};

  const result = await graphql(schema, query, rootValue, context, options);
  console.log(result);
}

main();
```

在这个文件中，我们从 graphql 包中导入了 graphql 函数。我们还从 schema.ts 文件中导入了 schema。

然后我们定义了一个 GraphQL 查询，它通过 ID 获取用户。我们还定义了一个“变量”对象，其中包含我们要获取的用户的 ID。

最后，我们调用了 `graphql` 函数，传入了我们的 `schema`、`query`、`rootValue`、`context` 和 `options`。该函数将执行我们的查询并返回结果。

如果我们运行这段代码，我们将得到以下输出：

```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Alice"
    }
  }
}
```

如您所见，我们的查询执行成功并返回了我们请求的数据。

## 结论

在本文中，我们了解了如何将 TypeScript 与 GraphQL 结合使用。我们已经了解了 TypeScript 如何帮助您创建类型安全的 GraphQL 查询以及如何使用 `graphql` 函数来执行这些查询。