---
title: Node.js 및 RabbitMQ: 메시지 큐에 대한 실습 가이드
description: 
published: true
date: 2023-01-31T17:05:09.868Z
tags: 
editor: markdown
dateCreated: 2023-01-31T17:05:08.124Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Node.js and RabbitMQ: A Hands-On Guide to Message Queues***English** version of this document is available*](/en/Knowledge-base/Nodejs/node-js-and-rabbitmq-a-hands-on-guide-to-message-queues)
{.links-list}


  IT 개발 학습 블로그에 "Node.js 및 RabbitMQ: 메시지 큐에 대한 실습 가이드"에 대한 기사를 작성하십시오.

Node.js는 개발자가 네트워크 애플리케이션을 빠르게 구축할 수 있게 해주는 프로그래밍 플랫폼입니다. RabbitMQ는 메시지 대기열 시스템을 구현하는 데 도움이 되는 오픈 소스 메시지 브로커입니다.

이 기사에서는 Node.js 및 RabbitMQ를 사용하여 메시지 대기열 시스템을 설정하는 방법을 보여줍니다. 시작하는 데 도움이 되는 몇 가지 코드 예제도 제공합니다.

메시지 대기열은 메시지를 비동기적으로 처리할 수 있도록 메시지를 저장하는 방법입니다. 즉, 서비스가 느리거나 사용할 수 없는 경우에도 애플리케이션을 계속 실행할 수 있습니다.

메시지 큐잉 시스템은 이미지 처리 또는 데이터 분석과 같이 시간이 많이 걸리거나 자원 집약적인 작업을 처리하는 데 사용할 수 있습니다. 또한 독립적으로 확장할 수 있도록 서비스를 분리하는 데 사용할 수 있습니다.

이 문서에서는 다음 항목을 다룹니다.

* 메시지 큐를 사용하는 이유는 무엇입니까?
* RabbitMQ 설정
* Node.js로 메시지 주고받기
* 작업자와 메시지 처리
* 모니터링 대기열

## 메시지 큐를 사용하는 이유는 무엇입니까?

애플리케이션에서 메시지 대기열을 사용하려는 몇 가지 이유가 있습니다.

### 비동기 처리

메시지 대기열의 주요 이점 중 하나는 작업을 비동기적으로 처리할 수 있다는 것입니다. 즉, 서비스가 느리거나 사용할 수 없는 경우에도 애플리케이션을 계속 실행할 수 있습니다.

예를 들어 전자 상거래 웹 사이트가 있는 경우 사용자가 사이트를 계속 탐색할 수 있도록 백그라운드에서 주문을 처리할 수 있습니다. 또는 소셜 미디어 애플리케이션이 있는 경우 사용자가 콘텐츠를 계속 업로드할 수 있도록 이미지와 비디오를 비동기적으로 처리할 수 있습니다.

### 디커플링 서비스

메시지 대기열의 또 다른 이점은 서비스를 분리하는 데 사용할 수 있다는 것입니다. 이는 애플리케이션의 다른 부분을 독립적으로 확장할 수 있음을 의미합니다.

예를 들어 이벤트 티켓을 판매하는 웹 사이트가 있는 경우 메시지 대기열을 사용하여 주문을 처리할 수 있습니다. 이렇게 하면 웹 사이트와 독립적으로 주문 처리 서비스를 확장할 수 있습니다.

### 안정적인 처리

메시지 대기열은 작업을 보다 안정적으로 처리하는 방법도 제공할 수 있습니다. 이는 메시지가 처리될 때까지 대기열에 저장되기 때문입니다.

서비스를 사용할 수 없는 경우 메시지는 서비스가 다시 온라인 상태가 될 때까지 큐에 저장됩니다. 즉, 서비스에 간헐적인 문제가 있어도 애플리케이션을 계속 실행할 수 있습니다.

## RabbitMQ 설정하기

RabbitMQ는 메시지 대기열 시스템을 구현하는 데 사용할 수 있는 오픈 소스 메시지 브로커입니다.

RabbitMQ에는 서버와 클라이언트라는 두 가지 주요 구성 요소가 있습니다. 서버는 큐에 메시지를 저장하는 역할을 합니다. 클라이언트는 메시지 송수신을 담당합니다.

RabbitMQ를 설정하려면 컴퓨터에 서버와 클라이언트를 설치해야 합니다.

### 서버 설치

[RabbitMQ 웹사이트](https://www.rabbitmq.com/download.html)에서 RabbitMQ 서버를 다운로드할 수 있습니다.

서버를 다운로드했으면 설치해야 합니다. Windows에서는 RabbitMQ를 서비스로 설치할 수 있습니다. Linux에서는 apt-get과 같은 패키지 관리자를 사용하여 설치할 수 있습니다.

### 클라이언트 설치

[npm 패키지 관리자](https://www.npmjs.com/)를 사용하여 RabbitMQ 클라이언트를 설치할 수 있습니다.

RabbitMQ 클라이언트를 설치하려면 터미널을 열고 다음 명령을 실행합니다.

```
npm install rabbitmq-client
```

## Node.js로 메시지 주고받기

이제 RabbitMQ를 설치했으므로 메시지 송수신을 시작할 수 있습니다.

이 섹션에서는 Node.js를 사용하여 메시지를 보내고 받는 방법을 보여줍니다.

### 메시지 보내기

메시지를 보내려면 RabbitMQ 서버에 대한 연결을 생성해야 합니다. `createConnection` 메소드를 사용하여 이를 수행할 수 있습니다.

연결을 만든 후에는 채널을 만들어야 합니다. 채널은 메시지를 보내고 받는 데 사용됩니다.

메시지를 보내려면 `sendToQueue` 메서드를 사용해야 합니다. 이 메서드는 큐 이름과 메시지라는 두 가지 인수를 사용합니다.

다음은 메시지를 보내는 방법의 예입니다.

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection({
  host: 'localhost',
  port: 5672
});

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.sendToQueue('my-queue', 'Hello, world!');
});
```

이 예에서는 RabbitMQ 서버에 대한 연결을 생성했습니다. 또한 채널을 만들고 `sendToQueue` 메서드를 사용하여 `my-queue` 대기열에 메시지를 보냈습니다.

### 메시지 수신

메시지를 수신하려면 `consume` 메소드를 사용해야 합니다. 이 메서드는 큐 이름과 콜백 함수라는 두 가지 인수를 사용합니다.

콜백 함수는 수신된 각 메시지에 대해 호출됩니다. 이 함수는 메시지와 콜백 함수라는 두 가지 인수를 사용합니다.

메시지 인수는 다음 속성을 포함하는 개체입니다.

* `content`: 메시지 내용
* `fields`: 메시지 필드를 포함하는 객체
* `properties`: 메시지 속성을 포함하는 객체

콜백 함수는 메시지를 확인하는 데 사용됩니다. 이것은 RabbitMQ에게 메시지가 처리되었고 큐에서 제거될 수 있음을 알려줍니다.

다음은 메시지를 받는 방법의 예입니다.

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection({
  host: 'localhost',
  port: 5672
});

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.consume('my-queue', function(message) {
    console.log(message.content.toString());

    channel.ack(message);
  });
});
```

이 예에서는 RabbitMQ 서버에 대한 연결을 생성했습니다. 또한 채널을 만들고 `consume` 메서드를 사용하여 `my-queue` 대기열의 메시지를 소비했습니다.

또한 수신된 각 메시지에 대해 호출될 콜백 함수를 정의했습니다. 이 함수는 메시지를 콘솔에 출력하고 `ack` 메서드를 호출하여 메시지를 Ack합니다.

## 작업자로 메시지 처리

이전 섹션에서는 메시지를 보내고 받는 방법을 설명했습니다. 이 섹션에서는 작업자를 사용하여 메시지를 처리하는 방법을 보여줍니다.

작업자는 백그라운드에서 실행되고 대기열의 메시지를 처리하는 Node.js 스크립트입니다.

작업자를 만들려면 `fork` 메서드를 사용해야 합니다. 이 메서드는 작업자 스크립트의 경로와 인수 배열이라는 두 가지 인수를 사용합니다.

작업자 스크립트에는 다음 인수가 전달됩니다.

* RabbitMQ 서버의 경로
* 대기열 이름

다음은 작업자를 만드는 방법의 예입니다.

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection({
  host: 'localhost',
  port: 5672
});

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.fork('worker.js', ['my-queue']);
});
```

이 예에서는 RabbitMQ 서버에 대한 연결을 생성했습니다. 또한 채널을 만들고 `fork` 메서드를 사용하여 작업자를 분기했습니다.

작업자는 RabbitMQ 서버 및 `my-queue` 큐에 대한 경로를 전달받습니다.

작업자 스크립트(`worker.js`)는 다음과 같습니다.

```javascript
var rabbitmq = require('rabbitmq-client');

var connection = rabbitmq.createConnection(process.argv[0]);

connection.on('ready', function() {
  var channel = connection.createChannel();

  channel.consume(process.argv[1], function(message) {
    // process the message
  });
});
```

이 스크립트에서는 RabbitMQ 서버에 대한 연결을 생성했습니다. 또한 채널을 만들고 `consume` 메서드를 사용하여 큐에서 메시지를 소비했습니다.

## 모니터링 대기열

문제를 식별하고 수정할 수 있도록 대기열을 모니터링하는 것이 중요합니다.

RabbitMQ는 대기열을 모니터링하는 데 사용할 수 있는 웹 인터페이스를 제공합니다. 웹 인터페이스에 액세스하려면 `rabbitmq-server` 명령으로 RabbitMQ 서버를 시작해야 합니다.

서버가 실행되면 http://localhost:15672/에서 웹 인터페이스에 액세스할 수 있습니다.

웹 인터페이스는 다음에 대한 정보를 제공합니다.

* 대기열에 있는 메시지 수
* 전달된 메시지 수
* 확인된 메시지 수
* 거부된 메시지 수

웹 인터페이스를 사용하여 메시지 내용을 볼 수도 있습니다.

## 결론

이 기사에서는 Node.js 및 RabbitMQ를 사용하여 메시지 대기열 시스템을 설정하는 방법을 보여주었습니다. 시작하는 데 도움이 되는 몇 가지 코드 예제도 제공했습니다.