---
title: 025：在 Nest.js 中创建和使用 GraphQL API
description: 
published: true
date: 2023-02-15T05:32:27.722Z
tags: 
editor: markdown
dateCreated: 2023-02-15T05:32:25.791Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [025: Creating and consuming GraphQL APIs in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/025-creating-and-consuming-graphql-apis-in-nest-js)
{.links-list}


## 介绍

GraphQL 是 Facebook 开发的 API 查询语言。它允许您从 API 请求特定数据，并且经常与 React 一起使用。 Nest.js 是 Node.js 的框架，可以轻松构建 GraphQL API。在本文中，我们将学习如何在 Nest.js 中创建和使用 GraphQL API。

## 在 Nest.js 中创建 GraphQL API

在 Nest.js 中创建 GraphQL API 很容易。首先，我们需要安装以下依赖项：

```
npm install --save @nestjs/graphql graphql-tools graphql
```

然后，我们可以在 `src` 目录中创建一个名为 `graphql.module.ts` 的文件并添加以下代码：

```typescript
import { Module } from '@nestjs/common';
import { GraphQLModule } from '@nestjs/graphql';
import { join } from 'path';

@Module({
  imports: [
    GraphQLModule.forRoot({
      typePaths: ['./**/*.graphql'],
      definitions: {
        path: join(process.cwd(), 'src/graphql.ts'),
      },
    }),
  ],
})
export class GraphQLModule {}
```

在上面的代码中，我们从 `@nestjs/graphql` 导入了 `GraphQLModule`。我们还指定了 GraphQL 模式文件的路径和生成的定义文件的路径。

接下来，我们需要在 `src` 目录中创建一个名为 `graphql.ts` 的文件并添加以下代码：

```typescript
import { gql } from '@nestjs/graphql';

export const typeDefs = gql`
  type Query {
    hello: String
  }
`;
```

在上面的代码中，我们从 `@nestjs/graphql` 导入了 `gql` 函数。这个函数允许我们在字符串中编写 GraphQL 查询。我们还定义了一个名为 Query 的 GraphQL 类型，其中包含一个名为 `hello` 的字段。

最后，我们需要在 `src` 目录中创建一个名为 `resolvers.ts` 的文件，并添加以下代码：

```typescript
import { Query, Resolver } from '@nestjs/graphql';

@Resolver('Query')
export class QueryResolver {
  @Query()
  hello() {
    return 'Hello, world!';
  }
}
```

在上面的代码中，我们从 @nestjs/graphql 导入了 Query 和 Resolver 装饰器。我们还创建了一个名为 QueryResolver 的类，它用 @Resolver 装饰器装饰。这个类包含一个名为“hello”的方法，它用“@Query”装饰器装饰。此方法返回字符串“Hello, world!”。

现在我们已经创建了 GraphQL API，让我们学习如何使用它。

## 在 Nest.js 中使用 GraphQL API

在 Nest.js 中使用 GraphQL API 有两种方式：使用 REST 客户端或使用 GraphQL 客户端。

### 使用 REST 客户端

我们可以使用像 Postman 这样的 REST 客户端来使用我们的 GraphQL API。首先，我们需要启动我们的 Nest.js 服务器：

```
nest start
```

然后，我们可以打开 Postman 并向 `http://localhost:3000/graphql` 发出 POST 请求。在请求的正文中，我们需要指定以下内容：

```
{
  "query": "query { hello }"
}
```

`query` 字段包含我们的 GraphQL 查询。在这种情况下，我们正在查询 `Query` 类型的 `hello` 字段。

当我们发送请求时，我们应该看到以下响应：

```
{
  "data": {
    "hello": "Hello, world!"
  }
}
```

### 使用 GraphQL 客户端

我们还可以使用像 Apollo Client 这样的 GraphQL 客户端来使用我们的 GraphQL API。首先，我们需要安装以下依赖项：

```
npm install --save apollo-client apollo-link-http apollo-cache-inmemory
```

然后，我们可以在 `src` 目录中创建一个名为 `app.js` 的文件并添加以下代码：

```javascript
import { ApolloClient } from 'apollo-client';
import { HttpLink } from 'apollo-link-http';
import { InMemoryCache } from 'apollo-cache-inmemory';

const client = new ApolloClient({
  link: new HttpLink({
    uri: 'http://localhost:3000/graphql',
  }),
  cache: new InMemoryCache(),
});

client
  .query({
    query: `
      query {
        hello
      }
    `,
  })
  .then((result) => console.log(result));
```

在上面的代码中，我们从 apollo-client 导入了 `ApolloClient`、`HttpLink` 和 `InMemoryCache`。我们还创建了一个带有 `HttpLink` 和 `InMemoryCache` 的 `ApolloClient` 实例。然后，我们对 `Query` 类型的 `hello` 字段进行查询，并将结果记录到控制台。

当我们运行上面的代码时，我们应该看到以下输出：

```
{
  data: {
    hello: 'Hello, world!'
  }
}
```

## 结论

在本文中，我们学习了如何在 Nest.js 中创建和使用 GraphQL API。我们还学习了如何使用 REST 客户端和 GraphQL 客户端来使用我们的 GraphQL API。