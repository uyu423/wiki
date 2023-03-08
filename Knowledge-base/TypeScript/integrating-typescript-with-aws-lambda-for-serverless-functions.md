---
title: 서버리스 기능을 위해 TypeScript를 AWS Lambda와 통합
description: 
published: true
date: 2023-02-11T02:17:23.547Z
tags: 
editor: markdown
dateCreated: 2023-02-11T02:17:21.921Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with AWS Lambda for Serverless Functions***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-aws-lambda-for-serverless-functions)
{.links-list}


# 서버리스 기능을 위해 TypeScript를 AWS Lambda와 통합

TypeScript는 Microsoft에서 개발 및 유지 관리하는 무료 오픈 소스 프로그래밍 언어입니다. 타이핑 및 클래스 기반 객체 지향 프로그래밍을 언어에 추가하는 JavaScript의 상위 집합입니다.

AWS Lambda는 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 클라우드 기반 컴퓨팅 서비스입니다. 이벤트에 대한 응답으로 코드를 실행하고 컴퓨팅 리소스를 자동으로 관리하는 서버리스 플랫폼입니다.

AWS Lambda와 함께 TypeScript를 사용하여 서버리스 함수를 작성할 수 있습니다. 이 기사에서는 TypeScript 함수를 작성하고 AWS Lambda에 배포하는 방법을 보여줍니다.

## TypeScript 함수 작성

TypeScript 함수는 이벤트에 대한 응답으로 실행되는 코드 조각입니다. HTTP 요청, 데이터베이스 작업 또는 기타 항목에 의해 트리거될 수 있습니다.

HTTP 요청에 의해 트리거되는 TypeScript 함수를 만들어 봅시다. 먼저 `index.ts`라는 파일을 만들고 다음 코드를 추가합니다.

```typescript
import { APIGatewayProxyEvent, APIGatewayProxyResult } from 'aws-lambda';

export const handler = async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {
  const body = JSON.parse(event.body);

  return {
    statusCode: 200,
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      message: `Hello, ${body.name}`
    })
  };
};
```

이 함수는 HTTP 요청에 의해 트리거되고 인사말 메시지를 반환합니다. `handler` 함수는 함수의 진입점입니다. 이는 `event` 객체를 인수로 사용하고 `APIGatewayProxyResult` 객체로 확인되는 `Promise`를 반환합니다.

`event` 객체에는 헤더, 본문 및 쿼리 매개변수와 같은 HTTP 요청에 대한 정보가 포함되어 있습니다. `event` 개체의 `body` 속성에는 요청의 JSON 인코딩 본문이 포함되어 있습니다.

`handler` 함수는 요청 본문을 구문 분석하고 JSON 인코딩 응답을 반환합니다. 응답의 'statusCode' 속성은 요청이 성공했음을 나타내기 위해 '200'으로 설정됩니다. `headers` 속성은 응답의 `Content-Type` 헤더를 설정하는 데 사용됩니다. `body` 속성에는 호출자에게 반환되는 메시지가 포함됩니다.

## 함수 배포

이제 TypeScript 함수를 작성했으므로 AWS Lambda에 배포해야 합니다. [Serverless Framework](https://serverless.com/)를 사용하여 기능을 배포합니다.

서버리스 프레임워크는 서버리스 애플리케이션을 AWS Lambda에 배포할 수 있는 Node.js 기반 프레임워크입니다. 이를 통해 서버리스 기능을 쉽게 관리할 수 있으며 [기능 버전 관리](https://serverless.com/blog/serverless-app-versioning/), [기능 별칭](https:// serverless.com/blog/serverless-app-aliases/) 및 [기능 단계](https://serverless.com/blog/serverless-app-stages/).

먼저 npm을 사용하여 Serverless Framework를 설치합니다.

```
npm install -g serverless
```

다음으로 프로젝트의 루트에 `serverless.yml`이라는 파일을 만들고 다음 코드를 추가합니다.

```yaml
service: my-service

provider:
  name: aws
  runtime: nodejs8.10

functions:
  myFunction:
    handler: index.handler
    events:
      - http:
          path: /
          method: post
```

이 파일에는 서버리스 애플리케이션에 대한 구성이 포함되어 있습니다. `service` 속성은 애플리케이션의 이름입니다. `provider` 속성은 공급자(이 경우 AWS)를 구성하는 데 사용됩니다. `runtime` 속성은 함수가 사용할 Node.js 런타임을 지정하는 데 사용됩니다.

`functions` 속성은 서버리스 기능을 구성하는 데 사용됩니다. 이 경우에는 `myFunction`이라는 함수가 하나 있습니다. `handler` 속성은 함수(`index.handler`)의 진입점을 지정하는 데 사용됩니다. `events` 속성은 함수를 트리거할 이벤트를 구성하는 데 사용됩니다. 이 경우 `/` 경로에 대한 `POST` 요청이 있을 때 트리거되는 HTTP 이벤트를 구성했습니다.

이제 서버리스 애플리케이션을 구성했으므로 `serverless deploy` 명령을 사용하여 배포할 수 있습니다.

```
serverless deploy
```

이 명령은 서버리스 애플리케이션을 AWS에 배포합니다. AWS Lambda 함수와 Amazon API Gateway API를 생성합니다.

`/` 경로에 `POST` 요청을 만들어 기능을 테스트할 수 있습니다. 다음과 같은 메시지가 표시됩니다.

```
{
    "message": "Hello, John"
}
```

## 마무리

이 기사에서는 TypeScript 함수를 작성하고 AWS Lambda에 배포하는 방법을 보여주었습니다. TypeScript는 JavaScript에 유형 검사 및 클래스 기반 객체 지향 프로그래밍을 추가하기 때문에 서버리스 함수를 작성하기 위한 훌륭한 언어입니다.

TypeScript에 대해 자세히 알아보려면 [TypeScript 웹사이트](https://www.typescriptlang.org/)를 확인하세요.

AWS Lambda에 대해 자세히 알아보려면 [AWS Lambda 설명서](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html)를 확인하세요.