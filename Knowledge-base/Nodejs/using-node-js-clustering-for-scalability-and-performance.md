---
title: 확장성과 성능을 위해 Node.js 클러스터링 사용
description: 
published: true
date: 2023-03-01T20:32:32.715Z
tags: 
editor: markdown
dateCreated: 2023-03-01T20:32:31.327Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using Node.js Clustering for Scalability and Performance***English** document is available*](/en/Knowledge-base/Nodejs/using-node-js-clustering-for-scalability-and-performance)
{.links-list}


# 확장성과 성능을 위해 Node.js 클러스터링 사용

Node.js는 개발자가 확장 가능한 고성능 애플리케이션을 만들 수 있는 JavaScript 런타임 환경입니다. Node.js 애플리케이션은 이벤트 기반이며 비차단 I/O 모델을 사용하므로 가볍고 효율적입니다.

Node.js 클러스터링은 단일 서버에서 Node.js 애플리케이션의 여러 인스턴스를 실행하는 프로세스입니다. 클러스터링은 Node.js 애플리케이션의 확장성과 성능을 높이는 방법입니다. Node.js 애플리케이션의 여러 인스턴스가 단일 서버에서 실행 중인 경우 각 인스턴스는 서로 다른 요청을 처리할 수 있습니다. 이렇게 하면 서버에서 더 많은 요청을 처리하고 더 빠르게 처리할 수 있습니다.

Node.js에서 클러스터링을 달성하는 방법에는 두 가지가 있습니다.

- 내장 클러스터 모듈 사용
- pm2와 같은 타사 모듈 사용

## 내장 클러스터 모듈 사용

Node.js는 클러스터링에 사용할 수 있는 `클러스터`라는 내장 모듈과 함께 제공됩니다. `클러스터` 모듈을 사용하면 개발자가 동일한 서버 포트를 공유하는 자식 프로세스를 만들 수 있습니다.

`클러스터` 모듈을 사용하려면 개발자는 먼저 애플리케이션에서 이를 요구해야 합니다.

```javascript
const cluster = require('cluster');
```

`cluster` 모듈을 요구한 후 개발자는 `fork()` 메서드를 사용하여 자식 프로세스를 만들 수 있습니다.

```javascript
if (cluster.isMaster) {
  // This code will be executed by the master process
  cluster.fork();
} else {
  // This code will be executed by the child process
}
```

`isMaster` 속성은 프로세스가 마스터 프로세스인지 하위 프로세스인지를 나타내는 부울 값입니다. 마스터 프로세스는 클러스터링을 초기화하는 프로세스이고 자식 프로세스는 마스터 프로세스와 서버 포트를 공유하는 프로세스입니다.

fork()` 메서드는 자식 프로세스를 만들고 `worker` 개체를 반환합니다. `worker` 개체에는 `worker.id` 및 `worker.process.pid` 속성을 포함하여 하위 프로세스에 대한 정보가 포함되어 있습니다.

`worker.id` 속성은 각 하위 프로세스에 고유한 숫자 값입니다. `worker.process.pid` 속성은 자식 프로세스의 프로세스 ID입니다.

자식 프로세스를 만든 후 마스터 프로세스는 `worker.send()` 메서드를 사용하여 자식 프로세스에 메시지를 보낼 수 있습니다.

```javascript
worker.send('Message from the master process');
```

자식 프로세스는 `worker.on('message')` 이벤트를 사용하여 마스터 프로세스로부터 메시지를 받을 수 있습니다.

```javascript
worker.on('message', (message) => {
  console.log(`Message from the master process: ${message}`);
});
```

`worker.on('message')` 이벤트는 하위 프로세스가 마스터 프로세스로부터 메시지를 수신할 때 트리거됩니다. `message` 인수는 마스터 프로세스에서 보낸 메시지입니다.

마스터 프로세스는 `cluster.workers` 속성을 사용하여 모든 하위 프로세스에 메시지를 보낼 수도 있습니다.

```javascript
for (const id in cluster.workers) {
  cluster.workers[id].send('Message from the master process');
}
```

`cluster.workers` 속성은 모든 하위 프로세스를 포함하는 개체입니다. `id` 속성은 자식 프로세스의 고유 ID이고 `cluster.workers[id]` 속성은 자식 프로세스 개체입니다.

마스터 프로세스는 `cluster.on('message')` 이벤트를 사용하여 모든 하위 프로세스로부터 메시지를 수신할 수도 있습니다.

```javascript
cluster.on('message', (worker, message) => {
  console.log(`Message from worker ${worker.id}: ${message}`);
});
```

`cluster.on('message')` 이벤트는 마스터 프로세스가 자식 프로세스로부터 메시지를 수신할 때 트리거됩니다. `worker` 인수는 메시지를 보낸 자식 프로세스이고 `message` 인수는 보낸 메시지입니다.

마스터 프로세스는 `worker.kill()` 메서드를 사용하여 하위 프로세스를 종료할 수도 있습니다.

```javascript
worker.kill();
```

`worker.kill()` 메서드는 `SIGTERM` 신호를 자식 프로세스에 전송하여 자식 프로세스를 종료합니다.

마스터 프로세스는 `worker.disconnect()` 메서드를 사용하여 하위 프로세스의 연결을 끊을 수도 있습니다.

```javascript
worker.disconnect();
```

`worker.disconnect()` 메서드는 마스터 프로세스에서 자식 프로세스의 연결을 끊습니다. 하위 프로세스는 계속 실행되지만 더 이상 마스터 프로세스와 통신할 수 없습니다.

## PM2 사용

PM2는 클러스터링에 사용할 수 있는 타사 모듈입니다. PM2는 Node.js 애플리케이션을 위한 생산 프로세스 관리자입니다. 이를 통해 개발자는 여러 프로세스 및 프로세스 그룹을 만들고 관리할 수 있습니다.

PM2를 사용하려면 개발자는 먼저 NPM을 사용하여 설치해야 합니다.

```javascript
npm install pm2 -g
```

PM2를 설치한 후 개발자는 `pm2 start` 명령을 사용하여 Node.js 애플리케이션을 시작할 수 있습니다.

```javascript
pm2 start app.js
```

`app.js` 파일은 Node.js 애플리케이션의 진입점입니다.

PM2는 Node.js 애플리케이션의 여러 인스턴스를 자동으로 시작하고 인스턴스 간의 요청 부하를 분산합니다.

또한 PM2를 사용하면 개발자가 애플리케이션의 상태를 모니터링할 수 있습니다. 개발자는 `pm2 monit` 명령을 사용하여 애플리케이션의 현재 요청, 메모리 사용량 및 CPU 사용량을 볼 수 있습니다.

```javascript
pm2 monit
```

또한 PM2를 사용하면 개발자가 애플리케이션의 로그 출력을 볼 수 있습니다. 개발자는 `pm2 logs` 명령을 사용하여 애플리케이션의 모든 인스턴스에 대한 결합된 로그 출력을 볼 수 있습니다.

```javascript
pm2 logs
```

개발자는 `--instance` 옵션을 사용하여 애플리케이션의 특정 인스턴스에 대한 로그 출력을 볼 수도 있습니다.

```javascript
pm2 logs --instance 0
```

`--instance` 옵션은 인스턴스의 인덱스를 지정합니다. 첫 번째 인스턴스의 인덱스는 '0'입니다.

개발자는 `--lines` 옵션을 사용하여 애플리케이션의 모든 인스턴스에 대한 로그 출력을 실시간으로 볼 수도 있습니다.

```javascript
pm2 logs --lines 1000
```

`--lines` 옵션은 표시할 로그 출력의 줄 수를 지정합니다.

또한 PM2를 사용하면 개발자가 애플리케이션을 다시 시작할 수 있습니다. 개발자는 `pm2 restart` 명령을 사용하여 애플리케이션의 모든 인스턴스를 다시 시작할 수 있습니다.

```javascript
pm2 restart app.js
```

개발자는 `--instance` 옵션을 사용하여 애플리케이션의 특정 인스턴스를 다시 시작할 수도 있습니다.

```javascript
pm2 restart app.js --instance 0
```

개발자는 애플리케이션을 중지할 수도 있습니다. 개발자는 `pm2 stop` 명령을 사용하여 애플리케이션의 모든 인스턴스를 중지할 수 있습니다.

```javascript
pm2 stop app.js
```

개발자는 `--instance` 옵션을 사용하여 애플리케이션의 특정 인스턴스를 중지할 수도 있습니다.

```javascript
pm2 stop app.js --instance 0
```

## 결론

Node.js 클러스터링은 단일 서버에서 Node.js 애플리케이션의 여러 인스턴스를 실행하는 프로세스입니다. 클러스터링은 Node.js 애플리케이션의 확장성과 성능을 높이는 방법입니다.

Node.js에서 클러스터링을 달성하는 방법에는 두 가지가 있습니다.

- 내장 클러스터 모듈 사용
- pm2와 같은 타사 모듈 사용