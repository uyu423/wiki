---
title: 025: Creating and consuming GraphQL APIs in Nest.js
description: 
published: true
date: 2023-02-15T05:32:33.532Z
tags: 
editor: markdown
dateCreated: 2023-02-15T05:32:25.796Z
---

- [025: Creación y consumo de API de GraphQL en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/025-creating-and-consuming-graphql-apis-in-nest-js)
{.links-list}
- [025：在 Nest.js 中创建和使用 GraphQL API***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/025-creating-and-consuming-graphql-apis-in-nest-js)
{.links-list}
- [025: Nest.js에서 GraphQL API 생성 및 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/025-creating-and-consuming-graphql-apis-in-nest-js)
{.links-list}


## Introduction

GraphQL is a query language for APIs that was developed by Facebook. It allows you to request specific data from an API and is often used with React. Nest.js is a framework for Node.js that makes it easy to build GraphQL APIs. In this post, we will learn how to create and consume GraphQL APIs in Nest.js.

## Creating a GraphQL API in Nest.js

Creating a GraphQL API in Nest.js is easy. First, we need to install the following dependencies:

```
npm install --save @nestjs/graphql graphql-tools graphql
```

Then, we can create a file called `graphql.module.ts` in the `src` directory and add the following code:

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

In the code above, we are imported the `GraphQLModule` from `@nestjs/graphql`. We are also specifying the path to our GraphQL schema files and the path to our generated definitions file.

Next, we need to create a file called `graphql.ts` in the `src` directory and add the following code:

```typescript
import { gql } from '@nestjs/graphql';

export const typeDefs = gql`
  type Query {
    hello: String
  }
`;
```

In the code above, we are importing the `gql` function from `@nestjs/graphql`. This function allows us to write GraphQL queries in a string. We are also defining a GraphQL type called `Query` with a field called `hello`.

Finally, we need to create a file called `resolvers.ts` in the `src` directory and add the following code:

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

In the code above, we are importing the `Query` and `Resolver` decorators from `@nestjs/graphql`. We are also creating a class called `QueryResolver` which is decorated with the `@Resolver` decorator. This class contains a method called `hello` which is decorated with the `@Query` decorator. This method returns the string `'Hello, world!'`.

Now that we have created our GraphQL API, let's learn how to consume it.

## Consuming a GraphQL API in Nest.js

There are two ways to consume a GraphQL API in Nest.js: using a REST client or using a GraphQL client.

### Using a REST Client

We can use a REST client like Postman to consume our GraphQL API. First, we need to start our Nest.js server:

```
nest start
```

Then, we can open Postman and make a POST request to `http://localhost:3000/graphql`. In the body of the request, we need to specify the following:

```
{
  "query": "query { hello }"
}
```

The `query` field contains our GraphQL query. In this case, we are querying the `hello` field on the `Query` type.

When we send the request, we should see the following response:

```
{
  "data": {
    "hello": "Hello, world!"
  }
}
```

### Using a GraphQL Client

We can also use a GraphQL client like Apollo Client to consume our GraphQL API. First, we need to install the following dependencies:

```
npm install --save apollo-client apollo-link-http apollo-cache-inmemory
```

Then, we can create a file called `app.js` in the `src` directory and add the following code:

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

In the code above, we are importing the `ApolloClient`, `HttpLink`, and `InMemoryCache` from `apollo-client`. We are also creating an `ApolloClient` instance with a `HttpLink` and an `InMemoryCache`. We are then making a query to the `hello` field on the `Query` type and logging the result to the console.

When we run the code above, we should see the following output:

```
{
  data: {
    hello: 'Hello, world!'
  }
}
```

## Conclusion

In this post, we learned how to create and consume GraphQL APIs in Nest.js. We also learned how to use a REST client and a GraphQL client to consume our GraphQL API.