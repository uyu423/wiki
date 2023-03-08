---
title: 073: Node.js 클러스터에서 TensorFlow.js 사용
description: 
published: true
date: 2023-02-02T23:43:28.283Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:43:26.641Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [073: Using TensorFlow.js with Node.js Clusters***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/073-using-tensorflow-js-with-node-js-clusters)
{.links-list}


# TensorFlow.js를 Node.js 클러스터와 함께 사용

TensorFlow.js는 브라우저와 Node.js 서버에서 기계 학습 모델을 훈련하고 배포하는 데 사용할 수 있는 강력한 도구입니다. 이 게시물에서는 TensorFlow.js를 Node.js 클러스터와 함께 사용하는 방법을 살펴보겠습니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 브라우저와 Node.js 서버에서 사용할 수 있는 기계 학습용 오픈 소스 라이브러리입니다. 이를 통해 JavaScript에서 기계 학습 모델을 교육하고 배포할 수 있습니다.

## Node.js 클러스터란?

Node.js 클러스터는 단일 시스템에서 Node.js 프로세스의 여러 인스턴스를 실행하여 Node.js 애플리케이션의 성능을 향상시키는 방법입니다. 클러스터는 기계 학습과 같은 CPU 집약적인 작업의 성능을 개선하는 데 사용할 수 있습니다.

## TensorFlow.js를 Node.js 클러스터와 함께 사용하는 방법

Node.js 클러스터와 함께 TensorFlow.js를 사용하는 것은 기계 학습 애플리케이션의 성능을 향상시키는 좋은 방법입니다. TensorFlow.js를 Node.js 클러스터와 함께 사용하려면 `cluster` 모듈을 사용해야 합니다.

`cluster` 모듈을 사용하면 Node.js 프로세스의 클러스터를 만들 수 있습니다. `클러스터` 모듈을 사용하려면 마스터 프로세스와 작업자 프로세스를 생성해야 합니다. 마스터 프로세스는 작업자 프로세스 생성을 담당합니다. 작업자 프로세스는 작업 실행을 담당합니다.

애플리케이션에서 마스터 프로세스용 코드가 포함된 파일과 작업자 프로세스용 코드가 포함된 파일을 만들어야 합니다. 마스터 프로세스 파일은 다음과 같아야 합니다.

```javascript
const cluster = require('cluster');

// The code for the master process

cluster.on('exit', (worker, code, signal) => {
  console.log(`worker ${worker.process.pid} died`);
});

```

작업자 프로세스 파일은 다음과 같아야 합니다.

```javascript
const cluster = require('cluster');

// The code for the worker process

if (cluster.isWorker) {
  console.log(`I am a worker, my id is ${cluster.worker.id}`);
}

```

애플리케이션을 실행하려면 `클러스터` 모듈을 사용해야 합니다. 예를 들어, 4개의 작업자에서 애플리케이션을 실행하려면 다음 명령을 사용할 수 있습니다.

```javascript
node master.js 4
```

## 추가 정보

- `cluster` 모듈에 대한 자세한 내용은 [Node.js 문서](https://nodejs.org/api/cluster.html)에서 확인할 수 있습니다.
- TensorFlow.js에 대한 자세한 내용은 [TensorFlow.js 설명서](https://js.tensorflow.org/)에서 확인할 수 있습니다.