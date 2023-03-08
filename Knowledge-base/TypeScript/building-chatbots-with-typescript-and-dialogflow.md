---
title: TypeScript와 Dialogflow로 챗봇 만들기
description: 
published: true
date: 2023-03-05T23:32:31.213Z
tags: 
editor: markdown
dateCreated: 2023-03-05T23:32:23.945Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Chatbots with TypeScript and Dialogflow***English** document is available*](/en/Knowledge-base/TypeScript/building-chatbots-with-typescript-and-dialogflow)
{.links-list}

TypeScript와 Dialogflow로 챗봇 만들기

챗봇은 고객과의 커뮤니케이션을 자동화하고 사용자 경험을 개선하는 방법으로 최근 몇 년 동안 점점 인기를 얻고 있습니다. Dialogflow는 개발자가 자연어 이해 기능을 갖춘 챗봇을 구축할 수 있는 강력한 도구입니다. 이 기사에서는 Dialogflow 및 TypeScript를 사용하여 챗봇을 구축하는 방법을 살펴보겠습니다.

### Dialogflow란?

Dialogflow는 개발자가 대화형 인터페이스를 설계하고 모바일 앱, 웹 애플리케이션, 장치 및 봇에 통합할 수 있도록 하는 자연어 이해 플랫폼입니다. Dialogflow는 기계 학습을 사용하여 자연어 입력을 이해하고 다양한 메시징 플랫폼 및 음성 도우미와 통합할 수 있습니다. 이전에는 API.ai로 알려졌으며 2016년 Google에 인수되었습니다.

### 타입스크립트란?

TypeScript는 JavaScript의 상위 집합인 프로그래밍 언어입니다. 정적 타이핑, 클래스, 인터페이스 및 모듈과 같은 추가 기능을 제공하여 대규모 애플리케이션을 보다 쉽게 구축할 수 있습니다. TypeScript는 일반 JavaScript로 컴파일되어 모든 브라우저 또는 JavaScript 런타임과 호환됩니다.

### Dialogflow 설정

Dialogflow를 시작하려면 Dialogflow 웹사이트에서 무료 계정을 만들어야 합니다. 가입하고 나면 구축할 챗봇인 새 에이전트를 만들 수 있습니다. Dialogflow 에이전트는 인텐트, 항목, 컨텍스트로 구성됩니다.

의도는 사용자의 의도 또는 요청을 나타내며 챗봇의 특정 작업 또는 응답에 매핑됩니다. 엔터티는 날짜, 시간 또는 위치와 같이 사용자가 요청에서 참조할 수 있는 특정 유형의 개체입니다. 컨텍스트는 대화 상태를 나타내며 챗봇이 컨텍스트에서 사용자의 요청을 이해하는 데 도움이 됩니다.

### Dialogflow와 TypeScript 통합

Dialogflow를 TypeScript와 통합하려면 Node.js용 Dialogflow 패키지를 설치해야 합니다.

```bash
npm install dialogflow
```

그런 다음 새 TypeScript 파일을 만들고 Dialogflow 패키지를 가져올 수 있습니다.

```typescript
import * as dialogflow from 'dialogflow';
```

다음으로 서비스 계정 키를 사용하여 Dialogflow API로 인증해야 합니다. Dialogflow 콘솔에서 서비스 계정 키를 다운로드하고 JSON 파일에 저장할 수 있습니다. 그런 다음 `fromJSON` 메서드를 사용하여 키를 로드할 수 있습니다.

```typescript
const credentials = require('./credentials.json');
const sessionClient = new dialogflow.SessionsClient({
  credentials: credentials,
});
```

또한 챗봇에 대한 세션 ID를 생성해야 합니다. 세션 ID는 사용자와 챗봇 간의 대화를 나타내며 각 사용자마다 고유해야 합니다. `uuid` 패키지를 사용하여 세션 ID를 생성할 수 있습니다.

```typescript
import * as uuid from 'uuid';

const sessionId = uuid.v4();
```

### 사용자 입력 처리

Dialogflow 에이전트를 설정하고 TypeScript와 통합하면 사용자 입력 처리를 시작할 수 있습니다. `detectIntent` 메서드를 사용하여 사용자의 메시지를 Dialogflow에 보낼 수 있습니다.

```typescript
async function handleUserMessage(message: string): Promise<string> {
  const sessionPath = sessionClient.sessionPath('my-project-id', sessionId);
  const request = {
    session: sessionPath,
    queryInput: {
      text: {
        text: message,
        languageCode: 'en-US',
      },
    },
  };
  const response = await sessionClient.detectIntent(request);
  return response.queryResult.fulfillmentText;
}
```

이 코드는 사용자의 메시지를 Dialogflow로 보내고 챗봇의 응답을 반환합니다. 그런 다음 이 코드를 챗봇의 프런트엔드 또는 백엔드에 통합하여 사용자 입력을 처리할 수 있습니다.

### 결론

Dialogflow 및 TypeScript로 챗봇을 구축하면 사용자 경험을 크게 개선하고 고객과의 커뮤니케이션을 자동화할 수 있습니다. 자연어 이해 및 정적 타이핑 기능을 통해 비즈니스 요구 사항을 충족하는 강력하고 확장 가능한 챗봇을 만들 수 있습니다.

외부 리소스:

- [Dialogflow 문서](https://cloud.google.com/dialogflow/docs)
- [TypeScript 설명서](https://www.typescriptlang.org/docs/)