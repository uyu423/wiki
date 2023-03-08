---
title: TypeScript 및 Node.js에서 데이터 스트림 작업
description: 
published: true
date: 2023-02-17T18:06:35.056Z
tags: 
editor: markdown
dateCreated: 2023-01-30T15:36:42.644Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Working with Data Streams in TypeScript and Node.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/working-with-data-streams-in-typescript-and-node-js)
{.links-list}

    
# 소개

이 기사에서는 TypeScript 및 Node.js에서 데이터 스트림으로 작업하는 방법을 살펴보겠습니다. Node.js에서 사용할 수 있는 다양한 유형의 스트림, 생성 방법 및 데이터 작업에 스트림을 사용하는 방법을 다룰 것입니다.

Node.js 스트림은 데이터를 보다 효율적으로 사용하는 데 도움이 되는 강력한 도구입니다. 스트림은 데이터를 읽고 쓰는 데 사용할 수 있으며 함께 연결하여 데이터에 대한 복잡한 작업을 수행할 수 있습니다.

Node.js에서 사용할 수 있는 스트림에는 읽기 가능, 쓰기 가능, 이중 및 변환의 네 가지 주요 유형이 있습니다. 읽기 가능한 스트림을 사용하면 소스에서 데이터를 읽을 수 있고 쓰기 가능한 스트림을 사용하면 대상에 데이터를 쓸 수 있으며 이중 스트림을 사용하면 데이터를 읽고 쓸 수 있으며 변환 스트림을 사용하면 데이터를 읽거나 쓸 때 데이터를 수정할 수 있습니다.

이 기사에서는 스트림의 처음 두 가지 유형인 읽기 가능 및 쓰기 가능에 초점을 맞출 것입니다. 읽고 쓸 수 있는 스트림을 만드는 방법과 이를 사용하여 데이터를 읽고 쓰는 방법을 살펴보겠습니다.

# 읽을 수 있는 스트림 만들기

Node.js에서 읽을 수 있는 스트림을 만드는 몇 가지 방법이 있습니다. 가장 간단한 방법은 `fs.createReadStream()` 메서드를 사용하는 것입니다.

```javascript
const fs = require('fs');

const readableStream = fs.createReadStream('/path/to/file');
```

이 메서드는 파일 경로를 유일한 인수로 사용하고 파일 내용을 읽는 데 사용할 수 있는 읽기 가능한 스트림을 반환합니다.

읽을 수 있는 스트림을 만드는 또 다른 방법은 `net.createServer()` 메서드를 사용하는 것입니다.

```javascript
const net = require('net');

const server = net.createServer((socket) => {
  // socket is a readable stream
});
```

이 메서드는 TCP 서버를 만들고 서버에서 데이터를 읽는 데 사용할 수 있는 읽기 가능한 스트림을 반환합니다.

# 쓰기 가능한 스트림 만들기

쓰기 가능한 스트림은 `fs.createWriteStream()` 메서드를 사용하여 만들 수 있습니다.

```javascript
const fs = require('fs');

const writableStream = fs.createWriteStream('/path/to/file');
```

이 메서드는 파일에 대한 경로를 유일한 인수로 사용하고 파일에 데이터를 쓰는 데 사용할 수 있는 쓰기 가능한 스트림을 반환합니다.

쓰기 가능한 스트림을 만드는 또 다른 방법은 `net.createServer()` 메서드를 사용하는 것입니다.

```javascript
const net = require('net');

const server = net.createServer((socket) => {
  // socket is a writable stream
});
```

이 메서드는 TCP 서버를 만들고 서버에 데이터를 쓰는 데 사용할 수 있는 쓰기 가능한 스트림을 반환합니다.

# 읽을 수 있는 스트림에서 읽기

읽을 수 있는 스트림을 만든 후에는 `read()` 메서드를 사용하여 스트림에서 데이터 읽기를 시작할 수 있습니다.

```javascript
readableStream.read();
```

이 메서드는 스트림에서 데이터를 읽고 문자열로 반환합니다.

읽을 수 있는 데이터가 없으면 `read()` 메서드는 `null`을 반환합니다.

# 쓰기 가능한 스트림에 쓰기

쓰기 가능한 스트림을 만든 후에는 `write()` 메서드를 사용하여 데이터 쓰기를 시작할 수 있습니다.

```javascript
writableStream.write('some data');
```

이 메서드는 스트림에 데이터를 씁니다. 데이터는 문자열 또는 버퍼일 수 있습니다.

# 스트림을 함께 배관하기

Node.js 스트림의 가장 강력한 기능 중 하나는 스트림을 함께 연결하는 기능입니다.

파이핑을 사용하면 두 개 이상의 스트림을 함께 연결하여 한 스트림의 데이터가 자동으로 다른 스트림으로 전송되도록 할 수 있습니다.

예를 들어 읽기 가능한 스트림을 쓰기 가능한 스트림으로 파이프할 수 있습니다.

```javascript
readableStream.pipe(writableStream);
```

이로 인해 읽기 가능한 스트림의 데이터가 쓰기 가능한 스트림에 기록됩니다.

여러 스트림을 함께 파이프할 수도 있습니다. 예를 들어 읽을 수 있는 스트림을 변환 스트림으로 파이프한 다음 변환 스트림을 쓰기 가능한 스트림으로 파이프할 수 있습니다.

```javascript
readableStream
  .pipe(transformStream)
  .pipe(writableStream);
```

이로 인해 읽을 수 있는 스트림의 데이터가 변환 스트림에 의해 변환된 다음 쓰기 가능한 스트림에 기록됩니다.

# 결론

이 기사에서는 TypeScript 및 Node.js에서 데이터 스트림으로 작업하는 방법을 살펴보았습니다. Node.js에서 사용할 수 있는 다양한 유형의 스트림, 생성 방법 및 데이터 작업에 스트림을 사용하는 방법을 다루었습니다.

Node.js 스트림은 데이터를 보다 효율적으로 사용하는 데 도움이 되는 강력한 도구입니다. 스트림은 데이터를 읽고 쓰는 데 사용할 수 있으며 함께 연결하여 데이터에 대한 복잡한 작업을 수행할 수 있습니다.

Node.js에서 데이터 작업에 대해 자세히 알아보려면 다음과 같은 다른 유용한 리소스를 확인하세요.

- [Node.js 스트림 핸드북](https://nodestreams.com/)
- [Node.js 스트림 API](https://nodejs.org/api/stream.html)
- [Node.js에서 스트리밍 데이터로 작업하기](https://www.twilio.com/blog/working-with-streaming-data-in-node-js)
- [Node.js 스트림: 알아야 할 모든 것](https://www.freecodecamp.org/news/node-js-streams-everything-you-need-to-know-c9143706be93/)