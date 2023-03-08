---
title: SMS 및 음성 통신을 위해 TypeScript를 Twilio와 통합
description: 
published: true
date: 2023-02-17T18:07:44.778Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:17:27.610Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Integrating TypeScript with Twilio for SMS and Voice Communications***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-twilio-for-sms-and-voice-communications)
{.links-list}


# SMS 및 음성 통신을 위해 TypeScript를 Twilio와 통합

개발자는 애플리케이션에 SMS 또는 음성 기능을 추가해야 하는 상황에 처할 수 있습니다. 예를 들어 사용자가 회사의 고객 서비스 번호로 SMS 메시지를 보낼 수 있도록 웹 사이트에 "문의하기" 양식을 추가해야 할 수 있습니다. 또는 사용자가 웹 또는 모바일 앱에서 전화를 걸 수 있는 기능을 추가해야 할 수도 있습니다.

Twilio는 애플리케이션에 음성 및 SMS 기능을 추가할 수 있는 클라우드 커뮤니케이션 플랫폼입니다. 이 기사에서는 TypeScript 프로그래밍 언어를 사용하여 Twilio를 웹 또는 모바일 앱과 통합하는 방법을 보여줍니다.

## 타입스크립트란?

TypeScript는 Microsoft에서 개발 및 유지 관리하는 무료 오픈 소스 프로그래밍 언어입니다. 모든 JavaScript 코드가 유효한 TypeScript 코드임을 의미하는 JavaScript의 상위 집합입니다.

TypeScript는 대규모 애플리케이션을 더 쉽게 개발할 수 있도록 JavaScript에 기능을 추가합니다. 예를 들어 TypeScript는 변수 및 함수에 유형 정보를 추가할 수 있는 유형 주석을 지원합니다. 이를 통해 개발 프로세스 초기에 버그를 발견할 수 있습니다.

##타입스크립트 설치

TypeScript를 설치하려면 컴퓨터에 Node.js와 npm이 설치되어 있어야 합니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있는 JavaScript 런타임입니다. npm은 TypeScript 및 기타 JavaScript 라이브러리를 설치할 수 있는 Node.js용 패키지 관리자입니다.

Node.js와 npm이 설치되면 다음 명령을 사용하여 TypeScript를 설치할 수 있습니다.

```
npm install -g typescript
```

## TypeScript 프로젝트 설정

TypeScript가 설치되면 다음 명령을 실행하여 TypeScript 프로젝트를 설정할 수 있습니다.

```
tsc --init
```

이렇게 하면 프로젝트 디렉토리에 `tsconfig.json`이라는 파일이 생성됩니다. 이 파일에는 프로젝트에 대한 TypeScript 구성이 포함되어 있습니다.

기본적으로 TypeScript 컴파일러는 최신 JavaScript 표준(ES6)과 호환되는 JavaScript 코드를 생성합니다. 이전 버전의 JavaScript와 호환되는 코드를 생성해야 하는 경우 `tsconfig.json`에서 `target` 컴파일러 옵션을 설정할 수 있습니다. 예를 들어 ES5 표준과 호환되는 코드를 생성하려면 `target` 옵션을 `"es5"`로 설정합니다.

## TypeScript 코드 컴파일

TypeScript 프로젝트가 설정되면 다음 명령을 사용하여 TypeScript 코드를 JavaScript로 컴파일할 수 있습니다.

```
tsc
```

이렇게 하면 프로젝트의 모든 TypeScript 코드가 JavaScript로 컴파일됩니다. 출력 JavaScript 파일은 `out` 디렉토리에 배치됩니다.

다음 명령을 실행하여 특정 TypeScript 파일을 컴파일할 수도 있습니다.

```
tsc file.ts
```

## Twilio와 TypeScript 통합

TypeScript의 기본 사항을 살펴보았으므로 이제 TypeScript를 사용하여 Twilio API를 사용하여 SMS 또는 음성 기능을 앱에 추가하는 방법을 살펴보겠습니다.

### SMS 메시지 보내기

TypeScript를 사용하여 SMS 메시지를 보내려면 Twilio 계정을 설정하고 Twilio 전화번호를 구매해야 합니다. Twilio 계정과 전화번호가 있으면 다음 TypeScript 코드를 사용하여 SMS 메시지를 보낼 수 있습니다.

```typescript
import * as twilio from "twilio";

const accountSid = "your-twilio-account-sid";
const authToken = "your-twilio-auth-token";
const client = twilio(accountSid, authToken);

client.messages
  .create({
     body: "Hello, world!",
     from: "your-twilio-phone-number",
     to: "your-phone-number"
   })
  .then(message => console.log(message.sid));
```

위의 코드에서 `import` 키워드를 사용하여 Twilio 라이브러리를 가져왔습니다. 그런 다음 계정 자격 증명을 사용하여 새 'Twilio' 클라이언트를 설정합니다. 마지막으로 `client.messages.create` 메서드를 사용하여 SMS 메시지를 보냈습니다.

### 전화 걸기

TypeScript를 사용하여 전화를 걸려면 Twilio 계정을 설정하고 Twilio 전화번호를 구입해야 합니다. Twilio 계정과 전화번호가 있으면 다음 TypeScript 코드를 사용하여 전화를 걸 수 있습니다.

```typescript
import * as twilio from "twilio";

const accountSid = "your-twilio-account-sid";
const authToken = "your-twilio-auth-token";
const client = twilio(accountSid, authToken);

client.calls
  .create({
     url: "your-twiML-url",
     to: "your-phone-number",
     from: "your-twilio-phone-number"
   })
  .then(call => console.log(call.sid));
```

위의 코드에서 `import` 키워드를 사용하여 Twilio 라이브러리를 가져왔습니다. 그런 다음 계정 자격 증명을 사용하여 새 'Twilio' 클라이언트를 설정합니다. 마지막으로 `client.calls.create` 메서드를 사용하여 전화를 걸었습니다.

## 결론

이 기사에서는 TypeScript를 사용하여 Twilio API를 사용하여 웹 또는 모바일 앱에 SMS 및 음성 기능을 추가하는 방법을 설명했습니다. 또한 TypeScript를 설치하는 방법과 TypeScript 프로젝트를 설정하는 방법을 포함하여 TypeScript의 기본 사항을 살펴보았습니다.