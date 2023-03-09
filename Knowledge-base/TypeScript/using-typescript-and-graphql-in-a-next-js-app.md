---
title: Next.js 앱에서 TypeScript 및 GraphQL 사용
description: 
published: true
date: 2023-03-09T02:33:03.414Z
tags: 
editor: markdown
dateCreated: 2023-03-09T02:33:03.414Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript and GraphQL in a Next.js App***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-and-graphql-in-a-next-js-app)
{.links-list}

## 소개

개발자는 효율적이고 확장 가능하며 유지 관리 가능한 웹 응용 프로그램을 만들기 위해 노력합니다. 이를 달성하기 위해 그들은 종종 **TypeScript** 및 **GraphQL**과 같은 최신 웹 기술을 사용합니다. 이 기사에서는 **Next.js** 웹 애플리케이션에서 TypeScript 및 GraphQL을 구현하는 방법에 대해 설명합니다.

## Next.js가 무엇인가요?

Next.js는 개발자가 서버측 렌더링(SSR) 애플리케이션을 쉽게 구축할 수 있도록 하는 인기 있는 **React** 프레임워크입니다. 자동 코드 분할, 서버 측 렌더링 및 정적 사이트 생성과 같은 기능을 제공합니다. Next.js 애플리케이션은 클라우드에 쉽게 배포할 수도 있습니다.

## 타입스크립트란?

TypeScript는 정적 타이핑, 클래스 및 인터페이스를 언어에 추가하는 JavaScript의 상위 집합입니다. 개발자가 개발 프로세스 초기에 오류를 포착하고 더 나은 코드 편집기 지원을 제공하는 데 도움이 됩니다. TypeScript 코드는 모든 브라우저에서 실행할 수 있는 JavaScript로 변환됩니다.

## GraphQL이란?

GraphQL은 클라이언트가 서버에서 필요한 데이터를 정확히 지정할 수 있도록 하는 API용 쿼리 언어입니다. 기존 REST API에 대한 보다 효율적이고 유연한 대안을 제공합니다. GraphQL을 사용하면 클라이언트는 단일 요청으로 여러 리소스를 가져와 네트워크 오버헤드를 줄일 수 있습니다.

## TypeScript로 Next.js 앱 설정하기

TypeScript로 Next.js 앱을 설정하려면 필요한 종속성을 설치해야 합니다. 다음 명령을 사용하여 TypeScript로 새 Next.js 앱을 만들 수 있습니다.

```bash
npx create-next-app --typescript my-app
```

이 명령은 TypeScript를 지원하는 새로운 Next.js 앱을 만듭니다. 다음 명령을 사용하여 앱을 실행할 수 있습니다.

```bash
cd my-app
npm run dev
```

이제 `http://localhost:3000`의 브라우저에서 앱을 열 수 있습니다.

## Next.js 앱에 GraphQL 추가하기

Next.js 앱에 GraphQL을 추가하려면 다음 종속성을 설치해야 합니다.

```bash
npm install graphql apollo-server-micro apollo-boost isomorphic-unfetch
```

- **`graphql`**: GraphQL 런타임 라이브러리.
- **`apollo-server-micro`**: Next.js용 경량 GraphQL 서버입니다.
- **`apollo-boost`**: GraphQL 클라이언트를 설정하는 간단한 방법을 제공하는 패키지입니다.
- **`isomorphic-unfetch`**: 서버와 클라이언트 모두에서 HTTP 요청을 만드는 간단한 방법을 제공하는 패키지입니다.

### GraphQL 서버 설정

Next.js는 서버리스 기능을 생성할 수 있는 내장 API 경로 기능을 제공합니다. 이 기능을 사용하여 GraphQL 서버를 만들 수 있습니다.

다음 코드를 사용하여 새 파일 `api/graphql.ts`를 만듭니다.

```typescript
import { ApolloServer, gql } from "apollo-server-micro";
import { NextApiRequest, NextApiResponse } from "next";
import fetch from "isomorphic-unfetch";

const typeDefs = gql`
  type Query {
    hello: String
  }
`;

const resolvers = {
  Query: {
    hello: () => "Hello world!",
  },
};

const apolloServer = new ApolloServer({
  typeDefs,
  resolvers,
  context: async ({ req }: { req: NextApiRequest }) => {
    const token = req.headers.authorization || "";
    const user = await fetch("https://api.example.com/user", {
      headers: { authorization: token },
    }).then((res) => res.json());

    return { user };
  },
});

export const config = {
  api: {
    bodyParser: false,
  },
};

export default apolloServer.createHandler({ path: "/api/graphql" });
```

이 코드에서는 단일 쿼리 `hello`로 간단한 GraphQL 스키마를 정의합니다. 또한 문자열 "Hello world!"를 반환하는 쿼리에 대한 확인자를 정의합니다.

그런 다음 스키마와 리졸버를 사용하여 `ApolloServer` 인스턴스를 생성합니다. 또한 요청 헤더의 인증 토큰을 사용하여 외부 API에서 사용자 개체를 가져오는 컨텍스트 함수를 정의합니다.

마지막으로 GraphQL 서버 핸들러를 사용하여 Next.js API 경로를 내보냅니다. 또한 Apollo 서버가 이미 요청 본문을 구문 분석하므로 API 경로 구성에서 기본 본문 구문 분석기를 비활성화합니다.

### GraphQL 클라이언트 설정

GraphQL 클라이언트를 설정하기 위해 `apollo-boost` 패키지를 사용할 수 있습니다. 다음 코드를 사용하여 새 파일 `lib/apollo.ts`를 만듭니다.

```typescript
import { ApolloClient, InMemoryCache } from "apollo-boost";

export const client = new ApolloClient({
  uri: "/api/graphql",
  cache: new InMemoryCache(),
});
```

이 코드에서는 GraphQL 서버 엔드포인트(`/api/graphql`)와 메모리 내 캐시를 사용하여 `ApolloClient`의 새 인스턴스를 생성합니다.

## Next.js 앱에서 TypeScript 및 GraphQL 사용

이제 TypeScript로 Next.js 앱을 설정하고 GraphQL 서버와 클라이언트를 추가했으므로 애플리케이션에서 사용할 수 있습니다.

### GraphQL 쿼리 정의

GraphQL 쿼리를 정의하려면 쿼리 정의가 포함된 `.graphql` 파일을 생성해야 합니다. 다음 코드를 사용하여 새 파일 `queries/hello.graphql`을 만듭니다.

```graphql
query Hello {
  hello
}
```

이 코드에서는 단일 필드 `hello`로 GraphQL 쿼리 `Hello`를 정의합니다.

### 구성 요소에서 GraphQL 클라이언트 사용

구성 요소에서 GraphQL 클라이언트를 사용하려면 `@apollo/react-hooks` 패키지의 `useQuery` 후크를 사용할 수 있습니다.

다음 코드를 사용하여 새 파일 `pages/index.tsx`를 만듭니다.

```typescript
import { NextPage } from "next";
import { useQuery } from "@apollo/react-hooks";
import { client } from "../lib/apollo";
import HELLO_QUERY from "../queries/hello.graphql";

interface HelloData {
  hello: string;
}

const IndexPage: NextPage = () => {
  const { loading, error, data } = useQuery<HelloData>(HELLO_QUERY, {
    client,
  });

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return <p>{data?.hello}</p>;
};

export default IndexPage;
```

이 코드에서는 `useQuery` 후크와 `lib/apollo`에서 `client` 인스턴스를 가져옵니다. 또한 `queries/hello.graphql` 파일에서 `HELLO_QUERY` GraphQL 쿼리를 가져옵니다.

쿼리에서 반환된 데이터의 모양을 나타내는 인터페이스 `HelloData`를 정의합니다.

그런 다음 'useQuery' 후크를 사용하여 서버에서 데이터를 가져옵니다. `HELLO_QUERY` 및 `client`를 인수로 후크에 전달합니다. 쿼리가 실행되는 동안 로드 및 오류 상태도 제공합니다.

마지막으로 쿼리가 성공하면 `data.hello` 문자열을 렌더링합니다.

## 결론

이 기사에서는 Next.js 웹 애플리케이션에서 TypeScript 및 GraphQL을 구현하는 방법에 대해 논의했습니다. 우리는 GraphQL 서버와 클라이언트를 설정하고 서버에서 데이터를 가져오는 구성 요소에서 사용했습니다. 이 문서가 개발 여정에 도움이 되었기를 바랍니다.

## 외부 리소스

- [Next.js 문서](https://nextjs.org/docs)
- [TypeScript 설명서](https://www.typescriptlang.org/docs)
- [GraphQL 문서](https://graphql.org/learn)
- [Apollo 서버 설명서](https://www.apollographql.com/docs/apollo-server)
- [Apollo 클라이언트 문서](https://www.apollographql.com/docs/react)