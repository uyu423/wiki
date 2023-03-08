---
title: 061: Filesystem API와 함께 Nest.js 사용하기
description: 
published: true
date: 2023-02-10T10:56:24.848Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:56:18.452Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [061: Using Nest.js with the Filesystem API***English** document is available*](/en/Knowledge-base/Nest-js/Learning/061-using-nest-js-with-the-filesystem-api)
{.links-list}


# Filesystem API와 함께 Nest.js 사용

Nest.js는 확장 가능한 서버 측 애플리케이션을 만드는 데 도움이 되는 Node.js 프레임워크입니다. TypeScript를 사용하고 Node.js 생태계와 잘 통합됩니다.

이 게시물에서는 파일 시스템 API와 함께 Nest.js를 사용하는 방법을 살펴보겠습니다. 다음 모듈을 사용할 것입니다.

- [fs](https://nodejs.org/api/fs.html): Node.js 파일 시스템 모듈입니다.
- [경로](https://nodejs.org/api/path.html): Node.js 경로 모듈입니다.
- [util](https://nodejs.org/api/util.html): Node.js util 모듈입니다.

## 파일 읽기 및 쓰기

가장 먼저 할 일은 파일을 읽고 쓰는 방법을 배우는 것입니다. 파일을 읽고 그 내용을 콘솔에 출력하는 간단한 예제부터 시작하겠습니다.

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    throw err;
  }

  console.log(data);
});
```

위의 코드에서 `fs.readFile()` 메서드를 사용하여 파일 내용을 읽었습니다. 첫 번째 인수는 파일 경로이고 두 번째 인수는 인코딩입니다. 콜백 함수는 `err` 개체와 파일의 `data`라는 두 가지 인수를 사용합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 `data` 인수에 파일 내용이 포함됩니다.

파일을 동기식으로 읽기 위해 `fs.readFileSync()` 메서드를 사용할 수도 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

이제 파일을 작성하는 방법을 살펴보겠습니다. 다음 예제에서는 파일에 문자열을 씁니다.

```javascript
const fs = require('fs');

fs.writeFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

위의 코드에서 파일에 문자열을 쓰기 위해 `fs.writeFile()` 메서드를 사용했습니다. 첫 번째 인수는 파일의 경로이고 두 번째 인수는 쓸 문자열이며 세 번째 인수는 인코딩입니다. 콜백 함수는 `err` 객체라는 하나의 인수를 취합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 파일이 성공적으로 기록됩니다.

또한 `fs.writeFileSync()` 메서드를 사용하여 파일을 동기적으로 쓸 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 파일 추가

 기존 파일을 덮어쓰는 대신 데이터를 추가해야 하는 경우가 있습니다. `fs.appendFile()` 메서드를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const fs = require('fs');

fs.appendFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

위의 코드에서 `fs.appendFile()` 메서드를 사용하여 문자열을 파일에 추가했습니다. 첫 번째 인수는 파일 경로이고 두 번째 인수는 추가할 문자열이며 세 번째 인수는 인코딩입니다. 콜백 함수는 `err` 객체라는 하나의 인수를 취합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 파일이 성공적으로 기록됩니다.

또한 `fs.appendFileSync()` 메서드를 사용하여 파일을 동기식으로 추가할 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 파일 이름 바꾸기

`fs.rename()` 메서드를 사용하여 파일 이름을 바꿀 수 있습니다.

```javascript
const fs = require('fs');

fs.rename('old-file.txt', 'new-file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

위의 코드에서 `fs.rename()` 메서드를 사용하여 파일 이름을 변경했습니다. 첫 번째 인수는 이전 경로이고 두 번째 인수는 새 경로입니다. 콜백 함수는 `err` 객체라는 하나의 인수를 취합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 파일 이름이 성공적으로 변경됩니다.

또한 `fs.renameSync()` 메서드를 사용하여 파일 이름을 동기식으로 바꿀 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 파일 삭제

`fs.unlink()` 메서드를 사용하여 파일을 삭제할 수 있습니다.

```javascript
const fs = require('fs');

fs.unlink('file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

위의 코드에서 `fs.unlink()` 메서드를 사용하여 파일을 삭제했습니다. 첫 번째 인수는 파일 경로입니다. 콜백 함수는 `err` 객체라는 하나의 인수를 취합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 파일이 성공적으로 삭제됩니다.

또한 `fs.unlinkSync()` 메서드를 사용하여 파일을 동기식으로 삭제할 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 파일 설명

파일에 대한 정보를 얻기 위해 `fs.stat()` 메소드를 사용할 수 있습니다:

```javascript
const fs = require('fs');

fs.stat('file.txt', (err, stats) => {
  if (err) {
    throw err;
  }

  console.log(stats);
});
```

위의 코드에서 파일에 대한 정보를 얻기 위해 `fs.stat()` 메서드를 사용했습니다. 첫 번째 인수는 파일 경로입니다. 콜백 함수는 `err` 개체와 `stats` 개체라는 두 가지 인수를 사용합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 `stats` 개체에 파일에 대한 정보가 포함됩니다.

또한 `fs.statSync()` 메서드를 사용하여 파일에 대한 정보를 동기식으로 얻을 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 파일 보기

파일의 변경 사항을 감시하기 위해 `fs.watch()` 메서드를 사용할 수 있습니다:

```javascript
const fs = require('fs');

fs.watch('file.txt', (eventType, filename) => {
  console.log(eventType, filename);
});
```

위의 코드에서 파일의 변경 사항을 감시하기 위해 `fs.watch()` 메서드를 사용했습니다. 첫 번째 인수는 파일 경로입니다. 콜백 함수는 `eventType` 문자열과 `filename` 문자열의 두 가지 인수를 사용합니다.

`eventType` 인수는 다음 중 하나입니다.

- `rename`: 파일 이름이 변경되었습니다.
- `change`: 파일이 변경되었습니다.

`filename` 인수는 이름이 변경된 경우 파일의 새 경로가 되고 파일이 변경된 경우 `null`이 됩니다.

파일의 변경 사항을 감시하기 위해 `fs.watchFile()` 메서드를 사용할 수도 있습니다. 그러나 이 방법은 비용이 많이 들 수 있는 폴링을 사용합니다.

## 디렉토리 읽기

디렉토리의 내용을 읽기 위해 `fs.readdir()` 메소드를 사용할 수 있습니다:

```javascript
const fs = require('fs');

fs.readdir('/path/to/directory', (err, files) => {
  if (err) {
    throw err;
  }

  console.log(files);
});
```

위의 코드에서 우리는 `fs.readdir()` 메서드를 사용하여 디렉토리의 내용을 읽었습니다. 첫 번째 인수는 디렉토리 경로입니다. 콜백 함수는 `err` 객체와 `files` 배열의 두 가지 인수를 사용합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 `files` 배열에는 디렉토리에 있는 파일의 이름이 포함됩니다.

또한 `fs.readdirSync()` 메서드를 사용하여 디렉토리의 내용을 동기식으로 읽을 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 디렉토리 만들기

`fs.mkdir()` 메소드를 사용하여 디렉토리를 생성할 수 있습니다:

```javascript
const fs = require('fs');

fs.mkdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

위의 코드에서 `fs.mkdir()` 메서드를 사용하여 디렉토리를 생성했습니다. 첫 번째 인수는 디렉토리 경로입니다. 콜백 함수는 `err` 객체라는 하나의 인수를 취합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 디렉토리가 성공적으로 생성됩니다.

또한 `fs.mkdirSync()` 메서드를 사용하여 디렉토리를 동기식으로 생성할 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 디렉토리 삭제

`fs.rmdir()` 메소드를 사용하여 디렉토리를 삭제할 수 있습니다:

```javascript
const fs = require('fs');

fs.rmdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

위의 코드에서 `fs.rmdir()` 메서드를 사용하여 디렉토리를 삭제했습니다. 첫 번째 인수는 디렉토리 경로입니다. 콜백 함수는 `err` 객체라는 하나의 인수를 취합니다.

오류가 있으면 `err` 개체가 설정됩니다. 그렇지 않으면 디렉토리가 성공적으로 삭제됩니다.

또한 `fs.rmdirSync()` 메서드를 사용하여 디렉터리를 동기식으로 삭제할 수 있습니다. 그러나 이 방법은 이벤트 루프를 차단하므로 일반적으로 권장되지 않습니다.

## 결론

이 게시물에서는 파일 시스템 API와 함께 Nest.js를 사용하는 방법을 살펴보았습니다. 우리는 파일을 읽고 쓰는 방법, 파일에 데이터를 추가하는 방법, 파일 이름을 바꾸고 삭제하는 방법, 파일에 대한 정보를 얻는 방법, 파일의 변경 사항을 감시하는 방법, 디렉토리의 내용을 읽는 방법, 디렉토리 생성 및 삭제.