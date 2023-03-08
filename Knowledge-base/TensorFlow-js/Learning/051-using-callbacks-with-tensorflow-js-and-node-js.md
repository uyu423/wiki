---
title: 051: TensorFlow.js 및 Node.js에서 콜백 사용
description: 
published: true
date: 2023-02-02T18:43:29.457Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:43:27.809Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [051: Using Callbacks with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/051-using-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js에서 콜백 사용

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. Node.js는 서버에서 JavaScript를 실행할 수 있게 해주는 JavaScript 런타임입니다. 이 게시물에서는 TensorFlow.js 및 Node.js에서 콜백을 사용하는 방법을 보여줍니다.

## 콜백이란 무엇인가요?

콜백은 다른 함수에 인수로 전달되는 함수입니다. 콜백 함수는 다른 함수의 실행이 완료되면 호출됩니다. 콜백은 일반적으로 자바스크립트에서 비동기 작업을 수행하는 데 사용됩니다.

## TensorFlow.js에서 콜백 사용

TensorFlow.js는 비동기 작업을 수행할 수 있는 콜백 API를 제공합니다. 콜백 API는 `tf.tensor` 클래스에서 사용할 수 있습니다.

콜백 API를 사용하려면 먼저 `tf.tensor` 객체를 생성해야 합니다. `tf.tensor` 클래스는 데이터 배열과 모양 배열을 인수로 사용합니다. 데이터 배열은 텐서에 대한 데이터를 포함하는 JavaScript 배열입니다. 모양 배열은 텐서의 차원을 포함하는 JavaScript 배열입니다.

`tf.tensor` 객체를 생성했으면 `.then()` 메서드를 사용하여 콜백 함수를 등록할 수 있습니다. `.then()` 메서드는 콜백 함수를 인수로 받습니다. 콜백 함수는 `tf.tensor` 객체가 준비되면 호출됩니다.

`.then()` 메소드는 `Promise` 객체를 반환합니다. `Promise` 개체는 `.then()` 메서드의 결과를 나타냅니다. `Promise` 개체에는 다른 콜백 함수를 등록하는 데 사용할 수 있는 `.then()` 메서드가 있습니다.

다음은 `.then()` 메서드를 사용하여 콜백 함수를 등록하는 예입니다.

```javascript
const tensor = tf.tensor([1, 2, 3, 4], [2, 2]);

tensor.then(t => {
  // The callback function is called when the tensor is ready.
  // The tensor is passed as an argument to the callback function.
  // The tensor can be used in the callback function.
  console.log(t);
});
```

## Node.js에서 콜백 사용

Node.js는 비동기 작업을 수행할 수 있는 콜백 API를 제공합니다. 콜백 API는 `fs` 모듈에서 사용할 수 있습니다.

`fs` 모듈은 파일 시스템과 상호 작용하기 위한 API를 제공합니다. `fs` 모듈에는 파일을 비동기적으로 읽는 데 사용할 수 있는 `readFile()` 메서드가 있습니다. `readFile()` 메서드는 파일 경로와 콜백 함수를 인수로 받습니다. 콜백 함수는 파일을 읽을 때 호출됩니다. 파일 데이터는 콜백 함수에 인수로 전달됩니다.

다음은 `readFile()` 메서드를 사용하여 파일을 비동기적으로 읽는 예입니다.

```javascript
const fs = require('fs');

fs.readFile('file.txt', (err, data) => {
  // The callback function is called when the file is read.
  // The file data is passed as an argument to the callback function.
  // The file data can be used in the callback function.
  console.log(data);
});
```

## 추가 정보

- [약속 사용](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [Node.js 콜백](https://nodejs.org/api/fs.html# fs_fs_readfile_path_options_callback)