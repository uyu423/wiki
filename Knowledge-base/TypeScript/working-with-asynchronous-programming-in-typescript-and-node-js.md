---
title: TypeScript 및 Node.js에서 비동기 프로그래밍 작업
description: 
published: true
date: 2023-02-16T13:19:33.899Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:19:23.149Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Working with Asynchronous Programming in TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-asynchronous-programming-in-typescript-and-node-js)
{.links-list}


# TypeScript 및 Node.js에서 비동기 프로그래밍 작업

비동기 프로그래밍은 차단 호출을 피함으로써 효율적인 코드 실행을 허용하는 널리 사용되는 프로그래밍 패러다임입니다. 이 기사에서는 TypeScript 및 Node.js에서 비동기 프로그래밍으로 작업하는 방법을 살펴보겠습니다.

## 비동기 프로그래밍이란?

비동기 프로그래밍은 차단 호출을 피함으로써 효율적인 코드 실행을 허용하는 프로그래밍 패러다임입니다. 차단 호출은 실행을 계속하기 전에 응답을 기다리는 호출로, 성능 문제를 일으킬 수 있습니다.

비동기 프로그래밍을 사용하면 프로그램이 차단 호출의 응답을 기다리는 동안 다른 코드를 계속 실행할 수 있습니다. 이렇게 하면 프로그램이 응답을 기다리지 않으므로 보다 효율적인 코드 실행이 가능합니다.

## TypeScript의 비동기 프로그래밍

TypeScript는 깨끗하고 간단한 JavaScript 코드로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다.

TypeScript는 대규모 애플리케이션 개발용으로 설계되었으며 JavaScript로 트랜스컴파일됩니다. 비동기 프로그래밍은 차단 호출을 피함으로써 효율적인 코드 실행을 허용하므로 TypeScript에서 널리 사용되는 프로그래밍 패러다임입니다.

TypeScript에서 비동기 프로그래밍을 사용하는 방법에는 두 가지가 있습니다: Promises와 async/await.

### 약속

Promise는 TypeScript에서 비동기 코드로 작업하는 방법입니다. 약속은 아직 완료되지 않았지만 앞으로 완료될 것으로 예상되는 작업을 나타냅니다.

약속은 TypeScript에서 비동기 작업을 처리하는 데 사용됩니다. Promise는 다음 세 가지 상태 중 하나일 수 있습니다.

- **Pending**: 작업이 아직 완료되지 않았습니다.
- **완료됨**: 작업이 성공적으로 완료되었습니다.
- **거부됨**: 작업이 실패했습니다.

약속은 `Promise` 생성자를 사용하여 만들 수 있습니다.

```typescript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

`Promise` 생성자는 `resolve` 및 `reject`라는 두 개의 매개변수가 있는 콜백 함수를 사용합니다. 비동기 작업이 성공적으로 완료되면 `resolve` 함수가 호출됩니다. 비동기 작업이 실패하면 'reject' 함수가 호출됩니다.

프라미스가 생성되면 `then()` 메서드를 사용하여 프라미스가 이행될 때 호출할 콜백 함수를 등록할 수 있습니다.

```typescript
promise.then((result) => {
  // do something with the result
});
```

또한 `catch()` 메서드를 사용하여 약속이 거부될 때 호출할 콜백 함수를 등록할 수 있습니다.

```typescript
promise.catch((error) => {
  // do something with the error
});
```

다음은 약속을 사용하여 URL에서 이미지를 로드하는 예입니다.

```typescript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

이 예제에서는 이미지가 로드되었을 때 이미지 URL로 확인하거나 이미지 로드에 실패하면 오류와 함께 거부하는 'Promise'를 만듭니다.

### 비동기/대기

Async/await는 TypeScript에서 비동기 코드로 작업하는 방법입니다. 이를 통해 동기 코드처럼 보이고 느껴지는 비동기 코드를 작성할 수 있습니다.

Async/await는 약속 위에 구축되며 `async` 및 `await` 키워드를 사용합니다.

`async` 키워드는 비동기 함수를 만드는 데 사용됩니다. 비동기 함수는 약속을 반환하는 함수입니다.

```typescript
async function loadImage(url: string): Promise<string> {
  // do something async
}
```

`await` 키워드는 약속이 해결되기를 기다리는 데 사용됩니다. `async` 함수 내에서만 사용할 수 있습니다.

```typescript
async function loadImage(url: string): Promise<string> {
  const image = await loadImage(url);
  // do something with the image
}
```

이 예에서는 `async` 키워드를 사용하여 비동기 함수를 만듭니다. `await` 키워드를 사용하여 `loadImage` 함수가 해결될 때까지 기다립니다.

비동기/대기는 동기 코드처럼 보이고 느껴지는 비동기 코드를 작성할 수 있기 때문에 TypeScript에서 비동기 코드로 작업하는 인기 있는 방법입니다.

## Node.js의 비동기 프로그래밍

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다. 가볍고 효율적인 이벤트 중심의 논블로킹 I/O 모델을 사용합니다.

Node.js는 확장 가능한 네트워크 애플리케이션을 구축하도록 설계되었습니다. 비동기 프로그래밍은 차단 호출을 피함으로써 효율적인 코드 실행을 가능하게 하므로 Node.js에서 널리 사용되는 프로그래밍 패러다임입니다.

Node.js에서 비동기 프로그래밍으로 작업하는 두 가지 방법은 콜백과 약속입니다.

### 콜백

콜백은 Node.js에서 비동기 코드로 작업하는 방법입니다. 콜백은 비동기 작업이 완료될 때 호출되는 함수입니다.

비동기 작업이 시작되면 콜백 함수가 제공됩니다. 비동기 작업이 완료되면 콜백 함수가 호출됩니다.

콜백 함수는 파일 I/O와 같은 비동기 작업을 위해 Node.js에서 일반적으로 사용됩니다.

다음은 콜백 함수를 사용하여 파일을 읽는 예입니다.

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) {
    // do something with the error
  } else {
    // do something with the data
  }
});
```

이 예제에서는 `fs.readFile` 함수를 사용하여 파일을 읽습니다. `fs.readFile` 함수는 파일 경로와 콜백 함수를 사용합니다. 콜백 함수는 `err` 및 `data` 매개변수로 호출됩니다. `err` 매개변수가 `null`이 아니면 오류가 발생한 것입니다. 그렇지 않으면 `data` 매개변수에 파일의 데이터가 포함됩니다.

### 약속

Promise는 Node.js에서 비동기 코드로 작업하는 방법입니다. 약속은 아직 완료되지 않았지만 앞으로 완료될 것으로 예상되는 작업을 나타냅니다.

Promise는 Node.js에서 비동기 작업을 처리하는 데 사용됩니다. Promise는 다음 세 가지 상태 중 하나일 수 있습니다.

- **Pending**: 작업이 아직 완료되지 않았습니다.
- **완료됨**: 작업이 성공적으로 완료되었습니다.
- **거부됨**: 작업이 실패했습니다.

약속은 `Promise` 생성자를 사용하여 만들 수 있습니다.

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

`Promise` 생성자는 `resolve` 및 `reject`라는 두 개의 매개변수가 있는 콜백 함수를 사용합니다. 비동기 작업이 성공적으로 완료되면 `resolve` 함수가 호출됩니다. 비동기 작업이 실패하면 'reject' 함수가 호출됩니다.

프라미스가 생성되면 `then()` 메서드를 사용하여 프라미스가 이행될 때 호출할 콜백 함수를 등록할 수 있습니다.

```javascript
promise.then((result) => {
  // do something with the result
});
```

또한 `catch()` 메서드를 사용하여 약속이 거부될 때 호출할 콜백 함수를 등록할 수 있습니다.

```javascript
promise.catch((error) => {
  // do something with the error
});
```

다음은 약속을 사용하여 URL에서 이미지를 로드하는 예입니다.

```javascript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

이 예제에서는 이미지가 로드되었을 때 이미지 URL로 확인하거나 이미지 로드에 실패하면 오류와 함께 거부하는 'Promise'를 만듭니다.

## Node.js의 비동기 프로그래밍

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다. 가볍고 효율적인 이벤트 중심의 논블로킹 I/O 모델을 사용합니다.

Node.js는 확장 가능한 네트워크 애플리케이션을 구축하도록 설계되었습니다. 비동기 프로그래밍은 차단 호출을 피함으로써 효율적인 코드 실행을 가능하게 하므로 Node.js에서 널리 사용되는 프로그래밍 패러다임입니다.

Node.js에서 비동기 프로그래밍으로 작업하는 두 가지 방법은 콜백과 약속입니다.

### 콜백

콜백은 Node.js에서 비동기 코드로 작업하는 방법입니다. 콜백은 비동기 작업이 완료될 때 호출되는 함수입니다.

비동기 작업이 시작되면 콜백 함수가 제공됩니다. 비동기 작업이 완료되면 콜백 함수가 호출됩니다.

콜백 함수는 파일 I/O와 같은 비동기 작업을 위해 Node.js에서 일반적으로 사용됩니다.

다음은 콜백 함수를 사용하여 파일을 읽는 예입니다.

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) {
    // do something with the error
  } else {
    // do something with the data
  }
});
```

이 예제에서는 `fs.readFile` 함수를 사용하여 파일을 읽습니다. `fs.readFile` 함수는 파일 경로와 콜백 함수를 사용합니다. 콜백 함수는 `err` 및 `data` 매개변수로 호출됩니다. `err` 매개변수가 `null`이 아니면 오류가 발생한 것입니다. 그렇지 않으면 `data` 매개변수에 파일의 데이터가 포함됩니다.

### 약속

Promise는 Node.js에서 비동기 코드로 작업하는 방법입니다. 약속은 아직 완료되지 않았지만 앞으로 완료될 것으로 예상되는 작업을 나타냅니다.

Promise는 Node.js에서 비동기 작업을 처리하는 데 사용됩니다. Promise는 다음 세 가지 상태 중 하나일 수 있습니다.

- **Pending**: 작업이 아직 완료되지 않았습니다.
- **완료됨**: 작업이 성공적으로 완료되었습니다.
- **거부됨**: 작업이 실패했습니다.

약속은 `Promise` 생성자를 사용하여 만들 수 있습니다.

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

`Promise` 생성자는 `resolve` 및 `reject`라는 두 개의 매개변수가 있는 콜백 함수를 사용합니다. 비동기 작업이 성공적으로 완료되면 `resolve` 함수가 호출됩니다. 비동기 작업이 실패하면 'reject' 함수가 호출됩니다.

프라미스가 생성되면 `then()` 메서드를 사용하여 프라미스가 이행될 때 호출할 콜백 함수를 등록할 수 있습니다.

```javascript
promise.then((result) => {
  // do something with the result
});
```

또한 `catch()` 메서드를 사용하여 약속이 거부될 때 호출할 콜백 함수를 등록할 수 있습니다.

```javascript
promise.catch((error) => {
  // do something with the error
});
```

다음은 약속을 사용하여 URL에서 이미지를 로드하는 예입니다.

```javascript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

이 예제에서는 이미지가 로드되었을 때 이미지 URL로 확인하거나 이미지 로드에 실패하면 오류와 함께 거부하는 'Promise'를 만듭니다.

## 외부 리소스

- [비동기 함수 - TypeScript](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html# async-functions)
- [Node.js의 콜백 함수](https://nodejs.org/en/knowledge/javascript-conventions/callbacks/)
- [Node.js에서 Promise 사용하기](https://nodejs.org/en/knowledge/javascript-conventions/using-promises-in-nodejs/)