---
title: Node.js의 스트림 및 파이프: 실습 가이드
description: 
published: true
date: 2023-02-01T20:36:28.483Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:36:26.894Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Streams and Piping in Node.js: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/streams-and-piping-in-node-js-a-hands-on-guide)
{.links-list}


# Node.js의 스트림 및 파이프: 실습 가이드

Node.js 개발자라면 코드에서 스트림을 사용했을 가능성이 큽니다. 스트림은 Node.js의 기본 부분이며 HTTP 요청 및 응답 처리, 파일 읽기 및 쓰기 등을 비롯한 다양한 작업에 사용됩니다.

이 기사에서는 Node.js의 스트림 및 파이핑에 대해 배우는 실습 접근 방식을 사용합니다. 다음 주제를 다룹니다.

- 스트림이란 무엇입니까?
- 스트림 유형
- 스트림 생성
- 파이프 스트림
-오류 처리

## 스트림이란 무엇입니까?

스트림은 읽거나 쓸 수 있는 데이터로 작업하기 위한 추상화입니다. 스트림은 Node.js의 핵심 부분이며 HTTP 요청 및 응답 처리, 파일 읽기 및 쓰기 등 다양한 작업에 사용됩니다.

스트림은 소스에서 대상으로 스트림을 통해 데이터가 흐르는 데이터 파이프라인으로 생각할 수 있습니다. 스트림을 사용하여 소스에서 데이터를 읽거나 대상에 데이터를 쓰거나 둘 다 사용할 수 있습니다.

## 스트림 유형

스트림에는 읽기 가능, 쓰기 가능, 이중 및 변환의 네 가지 유형이 있습니다.

- 읽을 수 있는 스트림은 소스에서 데이터를 읽는 데 사용됩니다.
- 쓰기 가능한 스트림은 대상에 데이터를 쓰는 데 사용됩니다.
- 이중 스트림은 데이터 읽기 및 쓰기 모두에 사용됩니다.
- 변환 스트림은 스트림을 통해 흐르는 데이터를 변환하는 데 사용됩니다.

## 스트림 만들기

Node.js에서 스트림을 만드는 몇 가지 방법이 있습니다.

한 가지 방법은 내장 스트림 모듈을 사용하는 것입니다.

```javascript
const stream = require('stream');

const readableStream = new stream.Readable();
const writableStream = new stream.Writable();
const duplexStream = new stream.Duplex();
const transformStream = new stream.Transform();
```

또 다른 방법은 내장 `fs` 모듈을 사용하는 것입니다:

```javascript
const fs = require('fs');

const readableStream = fs.createReadStream('/path/to/file');
const writableStream = fs.createWriteStream('/path/to/file');
```

## 파이프 스트림

파이핑은 데이터가 한 스트림에서 다른 스트림으로 흐르도록 스트림을 함께 연결하는 방법입니다.

예를 들어 읽기 가능한 스트림을 쓰기 가능한 스트림으로 파이프할 수 있습니다.

```javascript
readableStream.pipe(writableStream);
```

파이프는 여러 스트림을 함께 연결하는 데 사용할 수 있습니다. 예를 들어 읽을 수 있는 스트림을 데이터를 변환하는 변환 스트림으로 파이프한 다음 변환 스트림을 쓰기 가능한 스트림으로 파이프할 수 있습니다.

```javascript
readableStream.pipe(transformStream).pipe(writableStream);
```

## 오류 처리

스트림으로 작업할 때 오류를 처리하는 것이 중요합니다. 스트림이 예기치 않게 닫히거나 데이터가 손상되는 등 다양한 이유로 오류가 발생할 수 있습니다.

스트림으로 작업할 때 오류를 처리하는 몇 가지 방법이 있습니다.

한 가지 방법은 스트림에서 `'error'` 이벤트를 수신하는 것입니다.

```javascript
stream.on('error', (err) => {
  // handle the error
});
```

또 다른 방법은 콜백 함수와 함께 `.pipe()` 메소드를 사용하는 것입니다:

```javascript
stream.pipe(destination, (err) => {
  // handle the error
});
```

마지막으로 약속과 함께 `.catch()` 메서드를 사용할 수 있습니다.

```javascript
stream.catch((err) => {
  // handle the error
});
```

## 결론

이 기사에서는 Node.js의 스트림 및 파이핑에 대해 배우기 위해 실습 방식을 취했습니다. 우리는 다음 주제를 다루었습니다.

- 스트림이란 무엇입니까?
- 스트림 유형
- 스트림 생성
- 파이프 스트림
- 오류 처리