---
title: 025: Nest.js에서 GraphQL API 생성 및 사용
description: 
published: true
date: 2023-02-15T05:32:27.441Z
tags: 
editor: markdown
dateCreated: 2023-02-15T05:32:25.788Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [025: Creating and consuming GraphQL APIs in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/025-creating-and-consuming-graphql-apis-in-nest-js)
{.links-list}


## 소개

GraphQL은 Facebook에서 개발한 API용 쿼리 언어입니다. API에서 특정 데이터를 요청할 수 있으며 React와 함께 자주 사용됩니다. Nest.js는 GraphQL API를 쉽게 구축할 수 있게 해주는 Node.js용 프레임워크입니다. 이 게시물에서는 Nest.js에서 GraphQL API를 만들고 사용하는 방법을 배웁니다.

## Nest.js에서 GraphQL API 생성

Nest.js에서 GraphQL API를 만드는 것은 쉽습니다. 먼저 다음 종속 항목을 설치해야 합니다.

```
npm install --save @nestjs/graphql graphql-tools graphql
```

그런 다음 `src` 디렉토리에 `graphql.module.ts`라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

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

위의 코드에서는 `@nestjs/graphql`에서 `GraphQLModule`을 가져옵니다. 또한 GraphQL 스키마 파일의 경로와 생성된 정의 파일의 경로를 지정하고 있습니다.

다음으로 `src` 디렉토리에 `graphql.ts`라는 파일을 만들고 다음 코드를 추가해야 합니다.

```typescript
import { gql } from '@nestjs/graphql';

export const typeDefs = gql`
  type Query {
    hello: String
  }
`;
```

위의 코드에서는 `@nestjs/graphql`에서 `gql` 함수를 가져옵니다. 이 함수를 사용하면 GraphQL 쿼리를 문자열로 작성할 수 있습니다. 또한 `hello`라는 필드를 사용하여 `Query`라는 GraphQL 유형을 정의합니다.

마지막으로 `src` 디렉토리에 `resolvers.ts`라는 파일을 만들고 다음 코드를 추가해야 합니다.

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

위의 코드에서는 `@nestjs/graphql`에서 `Query` 및 `Resolver` 데코레이터를 가져옵니다. 또한 `@Resolver` 데코레이터로 장식된 `QueryResolver`라는 클래스를 생성합니다. 이 클래스에는 `@Query` 데코레이터로 장식된 `hello`라는 메서드가 포함되어 있습니다. 이 메서드는 `'Hello, world!'` 문자열을 반환합니다.

이제 GraphQL API를 생성했으므로 이를 사용하는 방법을 알아보겠습니다.

## Nest.js에서 GraphQL API 사용

Nest.js에서 GraphQL API를 사용하는 방법에는 REST 클라이언트를 사용하거나 GraphQL 클라이언트를 사용하는 두 가지 방법이 있습니다.

### REST 클라이언트 사용

Postman과 같은 REST 클라이언트를 사용하여 GraphQL API를 사용할 수 있습니다. 먼저 Nest.js 서버를 시작해야 합니다.

```
nest start
```

그런 다음 Postman을 열고 `http://localhost:3000/graphql`에 POST 요청을 할 수 있습니다. 요청 본문에서 다음을 지정해야 합니다.

```
{
  "query": "query { hello }"
}
```

`query` 필드에는 GraphQL 쿼리가 포함되어 있습니다. 이 경우 `Query` 유형에서 `hello` 필드를 쿼리하고 있습니다.

요청을 보내면 다음과 같은 응답이 표시됩니다.

```
{
  "data": {
    "hello": "Hello, world!"
  }
}
```

### GraphQL 클라이언트 사용

Apollo 클라이언트와 같은 GraphQL 클라이언트를 사용하여 GraphQL API를 사용할 수도 있습니다. 먼저 다음 종속 항목을 설치해야 합니다.

```
npm install --save apollo-client apollo-link-http apollo-cache-inmemory
```

그런 다음 `src` 디렉토리에 `app.js`라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

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

위의 코드에서는 `apollo-client`에서 `ApolloClient`, `HttpLink` 및 `InMemoryCache`를 가져옵니다. 또한 `HttpLink` 및 `InMemoryCache`를 사용하여 `ApolloClient` 인스턴스를 생성하고 있습니다. 그런 다음 `Query` 유형의 `hello` 필드에 쿼리를 작성하고 그 결과를 콘솔에 기록합니다.

위의 코드를 실행하면 다음과 같은 결과가 표시됩니다.

```
{
  data: {
    hello: 'Hello, world!'
  }
}
```

## 결론

이 게시물에서는 Nest.js에서 GraphQL API를 만들고 사용하는 방법을 배웠습니다. 또한 REST 클라이언트와 GraphQL 클라이언트를 사용하여 GraphQL API를 사용하는 방법도 배웠습니다.