---
title: 동시 처리를 위한 Node.js 작업자 작업
description: 
published: true
date: 2023-02-05T06:17:28.584Z
tags: 
editor: markdown
dateCreated: 2023-02-05T06:17:23.244Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Working with Node.js Workers for Concurrent Processing***English** document is available*](/en/Knowledge-base/Nodejs/working-with-node-js-workers-for-concurrent-processing)
{.links-list}


# 동시 처리를 위한 Node.js 작업자 작업

이 기사에서는 동시 처리를 위해 Node.js 작업자와 작업하는 방법에 대해 설명합니다.

동시 처리는 여러 처리 장치가 작업의 서로 다른 부분에서 동시에 작동하는 병렬 처리의 한 형태입니다. 컴퓨터 프로그래밍에서 이는 작업을 병렬로 실행할 수 있는 더 작은 하위 작업으로 나누어 달성하는 경우가 많습니다.

Node.js는 동시 처리를 허용하는 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다. Node.js 작업자는 기본 Node.js 프로세스와 독립적으로 실행할 수 있는 별도의 프로세스입니다. 이러한 작업자는 이미지 처리 또는 데이터 암호화와 같은 CPU 집약적인 작업을 수행하는 데 사용할 수 있습니다.

Node.js에서 작업자를 만드는 방법에는 두 가지가 있습니다.

- `child_process.fork()` 메서드를 사용하여 새 프로세스를 만듭니다.
- `클러스터` 모듈을 사용하여 작업자를 생성합니다.

`child_process.fork()` 메서드는 작업자를 생성하는 데 권장되는 방법입니다. 이 메서드를 사용하면 부모 프로세스와 자식 프로세스 간에 데이터를 전달할 수 있으며 프로세스 간에 메시지를 보내는 `send()` 메서드도 제공합니다.

`클러스터` 모듈은 작업자를 생성할 수 있는 내장 모듈입니다. 클러스터 모듈은 많은 수의 작업자를 생성해야 하는 경우에 유용합니다.

## 일꾼 만들기

`child_process.fork()` 메서드를 사용하여 작업자를 생성하는 것으로 시작하겠습니다.

```javascript
const {fork} = require('child_process');

const worker = fork('worker.js');
```

위의 코드는 `fork()` 메소드를 호출하여 새로운 프로세스를 생성합니다. `fork()` 메서드는 새 프로세스에서 실행될 JavaScript 파일의 경로를 사용합니다. 이 경우에는 `worker.js` 파일의 경로를 전달합니다.

`worker.js` 파일에는 다음 코드가 포함되어 있습니다.

```javascript
console.log('Worker started');

process.on('message', (message) => {
  console.log(`Message from parent: ${message}`);
});

process.send('Hello from the child!');
```

위의 코드는 `message` 이벤트에 대한 리스너를 설정합니다. 이 이벤트는 상위 프로세스가 하위 프로세스에 메시지를 보낼 때 발생합니다. 리스너는 메시지를 콘솔에 기록합니다.

자식 프로세스도 `send()` 메서드를 사용하여 부모 프로세스에게 메시지를 보냅니다.

## 메시지 보내기

작업자를 생성하고 부모 프로세스와 자식 프로세스 간에 메시지를 보내는 방법을 살펴보았으니 이제 부모 프로세스에서 자식 프로세스로 메시지를 보내는 방법을 살펴보겠습니다.

```javascript
worker.send('Hello from the parent!');
```

위의 코드는 부모 프로세스에서 자식 프로세스로 메시지를 보냅니다. 메시지는 `worker.js` 파일에서 생성한 `message` 이벤트 리스너에 의해 수신됩니다.

## 오류 처리

작업자와 작업할 때 오류를 처리하는 것이 중요합니다. 그렇지 않으면 오류가 눈에 띄지 않고 예기치 않은 동작이 발생할 수 있습니다.

하위 프로세스의 오류를 처리하려면 `error` 이벤트를 사용할 수 있습니다.

```javascript
worker.on('error', (err) => {
  console.error(err);
});
```

위의 코드는 자식 프로세스에서 `error` 이벤트 리스너를 설정합니다. 이 이벤트는 자식 프로세스에 오류가 있을 때 발생합니다. 리스너는 오류를 콘솔에 기록합니다.

## 작업자 종료

`kill()` 메서드를 사용하여 작업자를 종료할 수 있습니다.

```javascript
worker.kill();
```

위의 코드는 작업자 프로세스를 종료합니다.

## 요약

이 기사에서는 동시 처리를 위해 Node.js 작업자로 작업하는 방법을 살펴보았습니다. 또한 작업자를 만들고 부모 프로세스와 자식 프로세스 간에 메시지를 보내고 오류를 처리하는 방법도 살펴보았습니다.