---
title: Microsoft Bot Framework로 챗봇 개발
description: 
published: true
date: 2023-02-12T19:18:22.601Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:18:20.742Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Developing Chatbots with Microsoft Bot Framework***English** document is available*](/en/Knowledge-base/Common/developing-chatbots-with-microsoft-bot-framework)
{.links-list}


# Microsoft Bot Framework로 챗봇 개발하기

더 많은 기업이 고객 상호 작용을 자동화하는 방법을 모색함에 따라 챗봇 개발은 IT 업계에서 뜨거운 주제가 되었습니다. Microsoft Bot Framework는 챗봇 구축을 위한 선도적인 플랫폼 중 하나로 개발자가 사용자와 자연스러운 방식으로 상호 작용할 수 있는 봇을 만들 수 있는 사용하기 쉬운 도구 및 서비스 세트를 제공합니다.

이 기사에서는 Microsoft Bot Framework를 사용하여 챗봇을 개발하는 데 필요한 사항을 살펴보겠습니다. 먼저 프레임워크의 다양한 구성 요소와 함께 작동하는 방식을 살펴보겠습니다. 그런 다음 몇 가지 코드 예제를 살펴보고 자신만의 챗봇 구축을 시작하는 방법을 보여줍니다.

## Microsoft Bot Framework란?

Microsoft Bot Framework는 개발자가 Facebook Messenger, Skype, Slack 등 다양한 플랫폼용 챗봇을 빌드하는 데 도움이 되는 도구 및 서비스 집합입니다. 프레임워크에는 봇 구축을 위한 API 집합과 봇 대화 관리를 위한 도구 및 서비스 집합을 제공하는 Bot Builder SDK가 포함되어 있습니다.

Bot Builder SDK를 사용하면 개발자가 자연어를 이해할 수 있는 봇을 만들 수 있습니다. SDK에는 대화 시스템, 자연어 처리 도구 세트, 봇 대화 관리용 도구 세트를 포함하여 봇 구축을 위한 도구 세트가 포함되어 있습니다.

또한 SDK에는 Facebook Messenger, Skype, Slack 등을 비롯한 다양한 서비스와 봇을 통합하기 위한 일련의 API가 포함되어 있습니다.

## Microsoft Bot Framework 작동 방식

Microsoft Bot Framework는 개발자가 자연어를 이해할 수 있는 봇을 만들 수 있도록 함으로써 작동합니다. 프레임워크에는 대화 시스템, 자연어 처리 도구 세트, 봇 대화 관리용 도구 세트를 포함하여 봇 구축을 위한 도구 세트가 포함되어 있습니다.

프레임워크에는 Facebook Messenger, Skype, Slack 등을 비롯한 다양한 서비스와 봇을 통합하기 위한 일련의 API도 포함되어 있습니다.

## Microsoft Bot Framework 시작하기

이제 Microsoft Bot Framework가 무엇이고 어떻게 작동하는지 살펴보았으므로 몇 가지 코드 예제를 시작하겠습니다.

가장 먼저 해야 할 일은 새 Microsoft Bot Framework 프로젝트를 만드는 것입니다. Microsoft Bot Framework Yeoman 생성기를 사용하여 이 작업을 수행할 수 있습니다.

생성기를 설치하려면 머신에 Node.js와 Yeoman이 설치되어 있어야 합니다. Node.js를 설치하려면 Node.js 웹사이트로 이동하여 운영 체제에 맞는 설치 프로그램을 다운로드하세요.

Node.js가 설치되면 다음 명령을 사용하여 Yeoman 생성기를 설치할 수 있습니다.

```
npm install -g yo generator-botframework
```

생성기가 설치되면 다음 명령을 사용하여 새 프로젝트를 만들 수 있습니다.

```
yo botframework
```

이름, 설명 및 버전을 포함하여 프로젝트에 대한 몇 가지 세부 정보를 입력하라는 메시지가 표시됩니다.

프로젝트가 생성되면 종속 항목을 설치해야 합니다. 이렇게 하려면 프로젝트 디렉터리로 이동하여 다음 명령을 실행합니다.

```
npm install
```

종속성이 설치되면 챗봇 개발을 시작할 수 있습니다.

## 챗봇 개발

Microsoft Bot Framework는 챗봇을 쉽게 개발할 수 있는 도구 및 서비스 집합과 함께 제공됩니다. 이 섹션에서는 프레임워크의 다양한 구성 요소를 사용하여 챗봇을 개발하는 방법을 살펴보겠습니다.

### 봇 빌더 SDK

Bot Builder SDK는 자연어를 이해할 수 있는 봇을 빌드할 수 있는 도구 세트입니다. SDK에는 대화 시스템, 자연어 처리 도구 세트 및 봇 대화 관리용 도구 세트가 포함되어 있습니다.

SDK를 시작하려면 프로젝트의 루트 디렉터리에 새 파일을 만들어야 합니다. 파일 이름은 `bot.js`여야 합니다.

`bot.js` 파일에서 `botbuilder` 모듈을 요구하고 새 `BotBuilder` 인스턴스를 생성해야 합니다.

```javascript
var builder = require('botbuilder');

var bot = new builder.BotBuilder();
```

### 대화 시스템

대화 시스템은 Bot Builder SDK의 핵심입니다. 사용자와 챗봇 간의 대화 흐름을 정의할 수 있습니다.

대화 시스템은 대화의 개념을 기반으로 합니다. 대화는 사용자와 챗봇 간의 대화 단위입니다. 대화 상자는 중첩될 수 있습니다. 즉, 대화 상자에 다른 대화 상자가 포함될 수 있습니다.

대화 상자를 만들려면 프로젝트의 `/dialogs` 디렉터리에 새 파일을 만들어야 합니다. 파일 이름은 `{dialog_name}.js`여야 합니다.

`{dialog_name}.js` 파일에서 `botbuilder` 모듈을 요구하고 새 `Dialog` 인스턴스를 생성해야 합니다.

```javascript
var builder = require('botbuilder');

var dialog = new builder.Dialog();
```

`Dialog` 인스턴스가 있으면 `stack` 속성에 대화를 추가하여 대화의 흐름을 정의할 수 있습니다.

```javascript
dialog.stack(
    // First dialog in the stack
    function (session, args, next) {
        // Do something here
    },
    // Second dialog in the stack
    function (session, args, next) {
        // Do something here
    }
);
```

`addDialog` 메서드를 사용하여 `stack` 속성에 대화 상자를 추가할 수도 있습니다.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
});
```

`addDialog` 메서드는 `onSelector` 함수를 허용하여 대화 상자를 실행할 시기를 지정할 수 있습니다. 'onSelector' 함수는 대화상자가 실행되어야 할 때 'true'를 반환하고 그렇지 않아야 할 때 'false'를 반환해야 합니다.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
});
```

`addDialog` 메서드는 `onReject` 함수도 허용하여 대화 상자가 실행되지 않는 경우 발생할 일을 지정할 수 있습니다. 'onReject' 함수는 스택의 다음 대화로 전달되어야 하는 값으로 해결되는 'Promise'를 반환해야 합니다.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return false when the dialog should not be executed
    return false;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

`addDialog` 메서드는 또한 `onPost` 함수를 허용하여 대화 상자가 실행된 후 발생해야 하는 작업을 지정할 수 있습니다. `onPost` 함수는 스택의 다음 대화로 전달되어야 하는 값으로 해결되는 `Promise`를 반환해야 합니다.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

### 자연어 처리 도구

Bot Builder SDK에는 자연어 처리를 위한 도구 세트가 포함되어 있습니다. 이러한 도구를 사용하여 사용자의 의도를 이해하고 사용자 입력에서 엔터티를 추출하는 등의 작업을 수행할 수 있습니다.

자연어 처리 도구는 'LuisRecognizer' 및 'QnAMakerRecognizer' 클래스를 기반으로 합니다.

자연어 처리 도구를 사용하려면 프로젝트의 `/recognizers` 디렉터리에 새 파일을 만들어야 합니다. 파일 이름은 `{recognizer_name}.js`여야 합니다.

`{recognizer_name}.js` 파일에서 `botbuilder` 모듈을 요구하고 새 `LuisRecognizer` 또는 `QnAMakerRecognizer` 인스턴스를 생성해야 합니다.

```javascript
var builder = require('botbuilder');

var recognizer = new builder.LuisRecognizer();
```

`LuisRecognizer` 또는 `QnAMakerRecognizer` 인스턴스가 있으면 `recognize` 메서드를 사용하여 사용자 입력을 처리할 수 있습니다.

```javascript
recognizer.recognize('What is your name?', function (err, result) {
    // Handle the result here
});
```

`recognize` 메서드는 인식 결과와 함께 호출되는 `callback` 함수를 허용합니다. `callback` 함수에는 `err` 및 `result`라는 두 개의 인수가 전달됩니다.

`err` 인수는 인식 중 오류가 발생한 경우 전달되는 오류 개체입니다.

`result` 인수는 인식 결과를 포함하는 객체입니다. 개체에는 다음과 같은 속성이 있습니다.

- `의도`: 인식된 의도의 이름입니다.
- `score`: 0과 1 사이의 신뢰도 점수입니다.
- `엔티티`: 사용자 입력에서 추출한 엔티티를 포함하는 개체입니다.

### 봇 대화 관리 도구

Bot Builder SDK에는 봇 대화를 관리하기 위한 도구 세트가 포함되어 있습니다. 이러한 도구를 사용하여 사용자에게 메시지를 보내고 대화를 종료하는 등의 작업을 수행할 수 있습니다.

봇 대화 관리 도구를 사용하려면 `botbuilder` 모듈이 필요하고 새 `ConversationBot` 인스턴스를 생성해야 합니다.

```javascript
var builder = require('botbuilder');

var bot = new builder.ConversationBot();
```

`ConversationBot` 인스턴스가 있으면 `message` 메서드를 사용하여 사용자에게 메시지를 보낼 수 있습니다.

```javascript
bot.message('Hello, world!');
```

`message` 메소드는 사용자에게 보내야 하는 메시지인 `text` 인수와 메시지가 전송되었을 때 호출되는 `callback` 함수를 허용합니다.

'endConversation' 메서드를 사용하여 대화를 종료할 수도 있습니다.

```javascript
bot.endConversation();
```

`endConversation` 메서드는 인수를 허용하지 않습니다.

## 챗봇 배포

챗봇을 개발했으면 사용자가 사용할 수 있도록 서버에 배포해야 합니다.

Microsoft Bot Framework는 챗봇 배포를 위한 일련의 도구 및 서비스와 함께 제공됩니다. 프레임워크에는 챗봇을 Facebook Messenger, Skype, Slack 등 다양한 채팅 플랫폼에 연결할 수 있는 Bot Connector 서비스가 포함되어 있습니다.

챗봇을 배포하려면 먼저 프로젝트의 루트 디렉터리에 새 파일을 만들어야 합니다. 파일 이름은 `.env`여야 합니다.

`.env` 파일에서 다음 환경 변수를 추가해야 합니다.

- `PORT`: 챗봇이 실행될 포트입니다.
- `MICROSOFT_APP_ID`: Microsoft 앱 ID입니다.
- `MICROSOFT_APP_PASSWORD`: Microsoft 앱 비밀번호입니다.

`.env` 파일에 환경 변수를 추가했으면 다음 명령을 사용하여 챗봇을 시작할 수 있습니다.

```
npm start
```

이제 'PORT' 환경 변수에 지정된 포트에서 챗봇이 실행됩니다.

## 결론

이 기사에서는 Microsoft Bot Framework를 사용하여 챗봇을 개발하는 데 필요한 사항을 살펴보았습니다. 우리는 프레임워크의 다양한 구성 요소와 함께 작동하는 방식을 살펴보았습니다. 또한 자신만의 챗봇 구축을 시작하는 방법에 대한 몇 가지 코드 예제도 보았습니다.