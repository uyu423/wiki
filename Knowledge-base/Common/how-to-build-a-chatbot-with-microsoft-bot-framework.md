---
title: Microsoft Bot Framework로 챗봇을 구축하는 방법
description: 
published: true
date: 2023-02-12T09:17:32.189Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:17:30.474Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Chatbot with Microsoft Bot Framework***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-chatbot-with-microsoft-bot-framework)
{.links-list}


# Microsoft Bot Framework로 챗봇을 구축하는 방법

챗봇 개발은 어려운 작업처럼 보일 수 있지만 Microsoft Bot Framework를 사용하면 쉽고 재미있을 수 있습니다! 이 기사에서는 챗봇 구축을 시작하기 위해 알아야 할 모든 것을 살펴보겠습니다.

## 챗봇이란?

챗봇은 인간의 대화를 시뮬레이션하는 컴퓨터 프로그램입니다. 챗봇은 고객 서비스, 마케팅, 의료 등 다양한 산업에서 사용됩니다.

## 왜 챗봇을 만드나요?

챗봇은 고객 서비스를 개선하거나 사람들이 정보를 찾도록 돕는 좋은 방법이 될 수 있습니다. 또한 마케팅이나 재미로 사용할 수도 있습니다!

## 챗봇을 만들려면 무엇이 필요한가요?

챗봇을 구축하려면 인터넷에 연결된 컴퓨터와 텍스트 편집기가 필요합니다. Microsoft 계정도 필요합니다. 없는 경우 무료로 만들 수 있습니다.

## 챗봇은 어떻게 구축하나요?

챗봇을 구축하는 두 가지 주요 방법은 Bot Framework 도구를 사용하거나 Azure Bot Service를 사용하는 것입니다.

### Bot Framework 도구 사용

Bot Framework 도구는 챗봇 구축을 시작하는 좋은 방법입니다. 여기에는 Bot Builder SDK 및 CLI를 포함하여 시작하는 데 필요한 모든 것이 포함됩니다.

시작하려면 먼저 챗봇 프로젝트를 위한 새 폴더를 만드십시오. 그런 다음 텍스트 편집기에서 폴더를 열고 `app.js`라는 파일을 만듭니다.

다음으로 Bot Builder SDK를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install botbuilder
```

SDK가 설치되면 `app.js` 파일로 가져올 수 있습니다.

```js
const builder = require('botbuilder');
```

이제 코딩을 시작할 준비가 되었습니다!

먼저 봇 어댑터를 만들어야 합니다. 이는 챗봇을 Microsoft Bot Framework에 연결하는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
const adapter = new builder.BotFrameworkAdapter();
```

다음으로 봇 핸들러를 생성해야 합니다. 이것은 사용자로부터 들어오는 메시지를 처리하는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
const bot = new builder.UniversalBot(adapter);
```

이제 봇 핸들러에 코드를 추가할 준비가 되었습니다!

가장 먼저 해야 할 일은 ` WelcomeMessage` 대화 상자를 정의하는 것입니다. 이 대화 상자는 사용자에게 인사하고 시작하는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

보시다시피 이 대화 상자는 사용자에게 메시지를 보낸 다음 `GetName` 대화 상자를 시작합니다.

`GetName` 대화 상자는 사용자 이름을 가져오는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

보시다시피 이 대화 상자는 사용자에게 이름을 묻는 메시지를 표시한 다음 `results.response`라는 변수에 응답을 저장합니다. 그런 다음 대화 상자를 종료하고 사용자 이름과 함께 메시지를 보냅니다.

이제 챗봇을 테스트할 준비가 되었습니다! 이렇게 하려면 다음 명령을 실행해야 합니다.

```
node app.js
```

그러면 챗봇이 시작되고 이제 대화할 수 있습니다! "안녕하세요" 또는 "이름이 뭐죠?"라고 말해 보세요. 그리고 그것이 무엇을 하는지 보십시오.

### Azure 봇 서비스 사용

Azure Bot Service는 챗봇을 빌드하고 배포하는 좋은 방법입니다. 여기에는 Bot Builder SDK 및 CLI를 포함하여 시작하는 데 필요한 모든 것이 포함되어 있습니다.

시작하려면 먼저 챗봇 프로젝트를 위한 새 폴더를 만드십시오. 그런 다음 텍스트 편집기에서 폴더를 열고 `app.js`라는 파일을 만듭니다.

다음으로 Bot Builder SDK를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install botbuilder
```

SDK가 설치되면 `app.js` 파일로 가져올 수 있습니다.

```js
const builder = require('botbuilder');
```

이제 코딩을 시작할 준비가 되었습니다!

먼저 봇 어댑터를 만들어야 합니다. 이는 챗봇을 Microsoft Bot Framework에 연결하는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
const adapter = new builder.BotFrameworkAdapter();
```

다음으로 봇 핸들러를 생성해야 합니다. 이것은 사용자로부터 들어오는 메시지를 처리하는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
const bot = new builder.UniversalBot(adapter);
```

이제 봇 핸들러에 코드를 추가할 준비가 되었습니다!

가장 먼저 해야 할 일은 ` WelcomeMessage` 대화 상자를 정의하는 것입니다. 이 대화 상자는 사용자에게 인사하고 시작하는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

보시다시피 이 대화 상자는 사용자에게 메시지를 보낸 다음 `GetName` 대화 상자를 시작합니다.

`GetName` 대화 상자는 사용자 이름을 가져오는 데 사용됩니다. 다음 코드를 사용하여 이 작업을 수행할 수 있습니다.

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

보시다시피 이 대화 상자는 사용자에게 이름을 묻는 메시지를 표시한 다음 `results.response`라는 변수에 응답을 저장합니다. 그런 다음 대화 상자를 종료하고 사용자 이름과 함께 메시지를 보냅니다.

이제 챗봇을 테스트할 준비가 되었습니다! 이렇게 하려면 다음 명령을 실행해야 합니다.

```
node app.js
```

그러면 챗봇이 시작되고 이제 대화할 수 있습니다! "안녕하세요" 또는 "이름이 뭐죠?"라고 말해 보세요. 그리고 그것이 무엇을 하는지 보십시오.

## 자원

- [마이크로소프트 봇 프레임워크](https://dev.botframework.com/)
- [Azure 봇 서비스](https://azure.microsoft.com/en-us/services/bot-service/)
- [봇 빌더 SDK](https://docs.microsoft.com/en-us/javascript/api/botbuilder-core/botbuilder-core-sdk?view=botbuilder-js-stable)