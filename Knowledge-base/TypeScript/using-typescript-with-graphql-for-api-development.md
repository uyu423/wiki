---
title: API 개발을 위해 GraphQL과 함께 TypeScript 사용
description: 
published: true
date: 2023-02-01T19:17:56.734Z
tags: 
editor: markdown
dateCreated: 2023-02-01T19:17:52.569Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript with GraphQL for API Development***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-graphql-for-api-development)
{.links-list}


# API 개발을 위해 GraphQL과 함께 TypeScript 사용

TypeScript는 JavaScript 출력을 정리하기 위해 컴파일되는 강력한 형식의 JavaScript 상위 집합입니다. GraphQL은 클라이언트가 서버에서 필요한 데이터만 요청할 수 있는 권한을 제공하여 API를 보다 효율적으로 만드는 API용 강력한 쿼리 언어입니다.

두 기술을 함께 사용하여 강력하고 형식이 안전한 API 클라이언트 및 서버를 만들 수 있습니다. 이 기사에서는 짧은 코드 예제를 포함하여 GraphQL에서 TypeScript를 사용하는 방법을 살펴보겠습니다.

## GraphQL에서 TypeScript를 사용하는 이유는 무엇입니까?

GraphQL에서 TypeScript를 사용하려는 몇 가지 이유가 있습니다. 첫째, TypeScript는 형식이 안전한 GraphQL 쿼리를 생성하는 데 도움이 될 수 있습니다. 즉, 코드가 실행되기 전에 조기에 오류를 포착할 수 있습니다.

둘째, TypeScript는 GraphQL 서버에 대한 자동 완성 및 유형 안전성을 제공할 수 있습니다. 이것은 많은 유형과 필드가 있는 복잡한 GraphQL 스키마를 사용할 때 특히 유용합니다.

셋째, TypeScript는 코드 구성에 도움을 줄 수 있습니다. 예를 들어 TypeScript의 모듈 시스템을 사용하여 이해하고 유지하기 쉬운 방식으로 코드를 구성할 수 있습니다.

넷째, TypeScript는 점점 대중화되고 있으므로 GraphQL과 함께 사용하면 협력자와 지원을 더 쉽게 찾을 수 있습니다.

## GraphQL로 TypeScript 설정하기

GraphQL과 함께 TypeScript를 사용하려면 다음 종속 항목을 설치해야 합니다.

- 타자기: ^3.2.2
- graphql: ^14.3.1
- @types/graphql: ^14.0.1

npm을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install --save typescript graphql @types/graphql
```

## GraphQL과 함께 TypeScript 사용

종속 항목을 설치하면 GraphQL에서 TypeScript를 사용할 수 있습니다. 다음은 간단한 예입니다.

```graphql
query GetUser($id: ID!) {
  user(id: $id) {
    id
    name
  }
}
```

이 예에서는 ID로 사용자를 가져오는 GraphQL 쿼리를 정의했습니다. ID 변수에 대한 유형도 정의했습니다. 이 유형은 쿼리 변수의 유형을 확인하는 데 사용됩니다.

이제 이 쿼리를 TypeScript와 함께 사용하는 방법을 살펴보겠습니다. 먼저 `schema.ts`라는 파일을 만들어야 합니다.

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

이 파일에서 우리는 GraphQL 스키마를 정의했습니다. 또한 `User` 유형과 `Query` 유형도 정의했습니다. `Query` 유형에는 ID로 `User`를 가져오는 `user` 필드가 포함되어 있습니다.

이제 `index.ts`라는 파일을 만들어 보겠습니다.

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

이 파일에서는 `graphql` 패키지에서 `graphql` 함수를 가져왔습니다. 또한 `schema.ts` 파일에서 `schema`를 가져왔습니다.

그런 다음 ID로 사용자를 가져오는 GraphQL 쿼리를 정의했습니다. 또한 가져오려는 사용자의 ID를 포함하는 `variables` 객체를 정의했습니다.

마지막으로 `schema`, `query`, `rootValue`, `context` 및 `options`를 전달하는 `graphql` 함수를 호출했습니다. 이 함수는 쿼리를 실행하고 결과를 반환합니다.

이 코드를 실행하면 다음과 같은 결과가 표시됩니다.

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

보시다시피 쿼리가 성공적으로 실행되었고 요청한 데이터를 반환했습니다.

## 결론

이 기사에서는 GraphQL에서 TypeScript를 사용하는 방법을 살펴보았습니다. TypeScript가 유형에 안전한 GraphQL 쿼리를 만드는 데 어떻게 도움이 되는지, `graphql` 함수를 사용하여 이러한 쿼리를 실행하는 방법을 살펴보았습니다.