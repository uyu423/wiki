---
title: 064: TensorFlow.js 및 Node.js를 사용한 실시간 챗봇
description: 
published: true
date: 2023-02-02T22:04:38.155Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:04:36.503Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [064: Real-Time Chatbots with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/064-real-time-chatbots-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 실시간 챗봇

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 실시간 챗봇을 만드는 방법을 살펴보겠습니다. 사전 훈련된 모델을 사용하여 챗봇을 구축하고 여러 동시 사용자를 처리할 수 있도록 서버리스 플랫폼에 배포할 것입니다.

## 챗봇이란?

챗봇은 인간의 대화를 시뮬레이션하는 컴퓨터 프로그램입니다. 챗봇은 고객 서비스, 마케팅, 엔터테인먼트 등 다양한 맥락에서 사용됩니다.

## TensorFlow.js를 사용하는 이유는 무엇인가요?

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 오픈 소스이자 크로스 플랫폼이며 브라우저 또는 Node.js 환경에서 사용할 수 있습니다.

## Node.js가 무엇인가요?

Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임 환경입니다. Node.js는 서버 측 애플리케이션 개발에 사용됩니다.

## 전제 조건

이 게시물은 JavaScript와 Node.js에 대한 기본 지식이 있다고 가정합니다. 이러한 기술을 처음 사용하는 경우 다음 리소스를 확인하는 것이 좋습니다.

- [자바스크립트 튜토리얼](https://www.w3schools.com/js/)
- [Node.js 튜토리얼](https://nodejs.org/en/docs/guides/getting-started-guide/)

## 시작하기

### 1. 새 Node.js 프로젝트 만들기

새 Node.js 프로젝트를 만들어 시작하겠습니다. 우리는 [Express](https://expressjs.com/) 웹 프레임워크를 사용할 것이므로 이 프레임워크도 설치해야 합니다.

```
npm init
npm install express --save
```

### 2. 모델 교육

다음으로 챗봇에서 사용할 수 있는 기계 학습 모델을 교육해야 합니다. 이 게시물에서는 [TensorFlow.js Model Zoo](https://js.tensorflow.org/tutorials/training-chatbot.html)의 선행 학습된 모델을 사용합니다.

자신의 모델을 훈련시키거나 사전 훈련된 모델을 사용할 수 있습니다. 고유한 모델을 교육하려면 대화 데이터의 데이터 세트를 제공해야 합니다. TensorFlow.js Model Zoo는 사용할 수 있는 몇 가지 데이터 세트를 제공합니다.

데이터세트를 선택하면 [TensorFlow.js Model Maker](https://js.tensorflow.org/tutorials/model-maker.html)를 사용하여 모델을 학습시킬 수 있습니다.

### 3. 모델 배포

이제 학습된 모델이 있으므로 챗봇에서 사용할 수 있도록 배포해야 합니다. 이를 위해 [TensorFlow.js 모델 서버](https://js.tensorflow.org/tutorials/serving-models.html)를 사용할 것입니다.

TensorFlow.js 모델 서버는 모든 플랫폼에 배포할 수 있는 Node.js 애플리케이션입니다. TensorFlow.js 모델을 제공하고 추론을 위한 REST API를 제공할 수 있습니다.

### 4. 챗봇 구현

이제 모델이 배포되었으므로 챗봇 구현을 시작할 수 있습니다. 이를 위해 [Botkit](https://botkit.ai/) 라이브러리를 사용할 것입니다.

Botkit은 Slack, Facebook Messenger 및 기타 채팅 플랫폼용 봇을 쉽게 만들 수 있는 Node.js 라이브러리입니다.

먼저 Botkit을 설치해야 합니다.

```
npm install botkit --save
```

그런 다음 `chatbot.js`라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

```javascript
const Botkit = require('botkit');

const controller = Botkit.slackbot({
  debug: false,
});

controller.spawn({
  token: process.env.SLACK_BOT_TOKEN,
}).startRTM();

controller.hears('hello', ['direct_message', 'direct_mention', 'mention'], (bot, message) => {
  bot.reply(message, 'Hi there!');
});
```

이 코드는 `hello` 명령에 응답하는 Slack 봇을 생성합니다.

### 5. 챗봇 배포

이제 챗봇이 구현되었으므로 배포해야 합니다. 이를 위해 [Now](https://zeit.co/now)를 사용합니다.

Now는 Node.js 애플리케이션을 쉽게 배포할 수 있는 서버리스 플랫폼입니다. 인프라를 관리하므로 코드에 집중할 수 있습니다.

먼저 Now 계정을 만들고 Now CLI를 설치해야 합니다.

```
npm install -g now
```

그런 다음 다음 명령을 사용하여 챗봇을 배포할 수 있습니다.

```
now --env SLACK_BOT_TOKEN=your-bot-token
```

이렇게 하면 챗봇이 배포되고 액세스하는 데 사용할 수 있는 URL이 제공됩니다.

## 결론

이번 포스팅에서는 TensorFlow.js와 Node.js를 이용하여 실시간 챗봇을 만드는 방법에 대해 알아보았습니다. 기계 학습 모델을 교육하고 서버리스 플랫폼에 배포했습니다. 또한 Botkit 라이브러리를 사용하여 챗봇을 구현했습니다.