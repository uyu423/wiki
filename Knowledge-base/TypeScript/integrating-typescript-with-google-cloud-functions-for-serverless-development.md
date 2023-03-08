---
title: 서버리스 개발을 위해 TypeScript를 Google Cloud Functions와 통합
description: 
published: true
date: 2023-02-08T02:55:26.551Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:55:24.674Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with Google Cloud Functions for Serverless Development***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-google-cloud-functions-for-serverless-development)
{.links-list}


# 서버리스 개발을 위해 TypeScript를 Google Cloud Functions와 통합

TypeScript는 대규모 애플리케이션 개발을 가능하게 하는 유형이 지정된 JavaScript 상위 집합입니다. 이벤트에 대한 응답으로 코드를 실행하는 서버리스 컴퓨팅 서비스인 Google Cloud Functions에서 점점 더 많이 사용되고 있는 인기 있는 프로그래밍 언어입니다.

이 기사에서는 Google Cloud Functions에서 TypeScript를 사용하는 방법을 살펴보겠습니다. TypeScript로 작성된 함수를 작성하고 배포하는 방법을 살펴보고 Cloud Functions에서 TypeScript를 사용할 때의 몇 가지 이점에 대해서도 알아봅니다.

## TypeScript 함수 작성

TypeScript로 작성된 간단한 Cloud Function을 작성하는 것부터 시작하겠습니다. HTTP 요청에 응답하는 함수를 만드는 `http` 트리거 템플릿을 사용합니다.

먼저 프로젝트의 새 디렉터리를 만듭니다.

```
mkdir my-project
```

다음으로 이 디렉터리에서 TypeScript 프로젝트를 초기화합니다.

```
cd my-project
ts init
```

이렇게 하면 프로젝트에 `tsconfig.json` 파일이 생성됩니다. 이 파일은 TypeScript 컴파일러를 구성하는 데 사용됩니다.

이제 `@types/node` 및 `firebase-functions` npm 패키지를 설치해 보겠습니다. 이 패키지는 각각 Node.js 및 Firebase SDK에 대한 TypeScript 정의에 대한 액세스를 제공합니다.

```
npm install --save @types/node firebase-functions
```

이러한 종속성이 설치되었으므로 이제 Cloud 함수를 작성할 수 있습니다. 프로젝트 디렉터리에 `index.ts`라는 파일을 만들고 다음 코드를 추가합니다.

```typescript
import * as functions from 'firebase-functions';

export const helloWorld = functions.https.onRequest((request, response) => {
 response.send('Hello from Firebase!');
});
```

이 함수는 `https` 트리거를 사용하여 HTTP 요청을 처리합니다. 호출되면 단순히 'Hello from Firebase!'라는 문자열을 반환합니다.

## TypeScript 함수 배포

이제 TypeScript 함수가 있으므로 Cloud Functions에 배포해 보겠습니다. 먼저 TypeScript 코드를 JavaScript로 컴파일해야 합니다. TypeScript 컴파일러를 사용하여 이 작업을 수행할 수 있습니다.

```
tsc
```

이렇게 하면 프로젝트 디렉토리에 `index.js` 파일이 생성됩니다. 이 파일에는 함수에 대한 컴파일된 JavaScript 코드가 포함되어 있습니다.

이제 Firebase CLI를 사용하여 함수를 배포할 수 있습니다.

```
firebase deploy --only functions
```

이렇게 하면 함수가 Cloud Functions에 배포됩니다. 배포되면 HTTP를 통해 호출하여 테스트할 수 있습니다.

```
curl https://YOUR_PROJECT_ID.cloudfunctions.net/helloWorld
```

다음과 같은 응답이 표시됩니다.

```
Hello from Firebase!
```

## Cloud Functions에서 TypeScript를 사용할 때의 이점

Cloud Functions에서 TypeScript를 사용하면 여러 가지 이점이 있습니다. 첫째, TypeScript는 더 강력한 타이핑 및 코드 인텔리전스 기능을 제공하여 개발 환경을 개선하는 데 도움이 될 수 있습니다. 예를 들어 TypeScript 컴파일러는 코드를 배포하기 전에 코드의 오류를 포착하는 데 도움이 될 수 있습니다.

둘째, TypeScript를 사용하면 Cloud Functions의 성능을 개선하는 데 도움이 될 수 있습니다. TypeScript 컴파일러는 코드에서 최적화를 수행하여 더 작고 빠른 JavaScript 코드를 생성할 수 있습니다.

마지막으로 TypeScript를 사용하면 대규모 Cloud Functions 프로젝트를 더 쉽게 개발할 수 있습니다. 코드를 모듈화하는 방법을 제공함으로써 TypeScript는 프로젝트를 관리하기 쉬운 더 작은 조각으로 나누는 데 도움을 줄 수 있습니다.

## 결론

이 기사에서는 Google Cloud Functions에서 TypeScript를 사용하는 방법을 배웠습니다. TypeScript 함수를 작성하고 배포하는 방법을 보았고 Cloud Functions와 함께 TypeScript를 사용할 때의 몇 가지 이점에 대해서도 배웠습니다.