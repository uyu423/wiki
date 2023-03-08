---
title: TypeScript 및 Node.js에서 이진 데이터 작업
description: 
published: true
date: 2023-02-10T09:17:41.028Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:17:38.473Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Working with Binary Data in TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-binary-data-in-typescript-and-node-js)
{.links-list}


# TypeScript와 Node.js에서 바이너리 데이터 다루기

IT 개발자는 종종 이진 데이터로 작업해야 합니다. 이진 데이터를 반환하는 API로 작업 중이거나 파일에 이진 데이터를 읽거나 써야 하기 때문일 수 있습니다. TypeScript 및 Node.js에서 개발자는 이진 데이터 작업을 위한 다양한 옵션을 사용할 수 있습니다.

## 버퍼 클래스

Node.js에서 바이너리 데이터로 작업하는 한 가지 방법은 `Buffer` 클래스를 사용하는 것입니다. 이 클래스는 전역에서 사용할 수 있으므로 가져올 필요가 없습니다. `Buffer` 클래스는 이진 데이터를 읽고 쓰기 위한 여러 메서드를 제공합니다.

문자열에서 `Buffer`를 생성하기 위해 개발자는 `Buffer.from()` 메서드를 사용할 수 있습니다. 이 메서드는 문자열과 인코딩을 인수로 사용합니다. 인코딩 인수는 선택 사항이며 기본값은 `utf8`입니다. 다음 예는 `utf8` 인코딩을 사용하여 문자열에서 `Buffer`를 생성합니다.

    const buf = Buffer.from('hello world', 'utf8');

개발자는 `Buffer.alloc()` 메서드를 사용하여 `Buffer`에 바이너리 데이터를 쓸 수도 있습니다. 이 메서드는 바이트 단위의 `Buffer` 크기인 숫자를 인수로 사용합니다. 다음 예제에서는 크기가 10바이트인 빈 `버퍼`를 만듭니다.

    const buf = Buffer.alloc(10);

`Buffer`가 생성되면 개발자는 `Buffer.write()` 메서드를 사용하여 버퍼에 데이터를 쓸 수 있습니다. 이 메서드는 문자열, 오프셋 및 인코딩을 인수로 사용합니다. 오프셋은 문자열이 기록될 `Buffer`의 인덱스입니다. 인코딩 인수는 선택 사항이며 기본값은 `utf8`입니다. 다음 예제는 인덱스 0부터 시작하여 이전 예제에서 생성된 `Buffer`에 문자열 ` 'hello world'`를 씁니다.

    buf.write('안녕하세요', 0, 'utf8');

개발자는 `Buffer`에서 데이터를 읽으려면 `Buffer.toString()` 메서드를 사용할 수 있습니다. 이 메서드는 인코딩과 선택적으로 시작 및 끝 인덱스를 인수로 사용합니다. 다음 예제는 이전 예제에서 생성한 `Buffer`에서 데이터를 읽어 문자열로 출력합니다.

    console.log(buf.toString('utf8')); // '안녕하세요'

## Uint8Array 클래스

TypeScript에서 이진 데이터로 작업하는 또 다른 방법은 `Uint8Array` 클래스를 사용하는 것입니다. 이 클래스는 전역에서 사용할 수 있으므로 가져올 필요가 없습니다. `Uint8Array` 클래스는 이진 데이터를 읽고 쓰기 위한 여러 메서드를 제공합니다.

숫자 배열에서 `Uint8Array`를 생성하기 위해 개발자는 `Uint8Array.from()` 메서드를 사용할 수 있습니다. 이 메서드는 숫자 배열을 인수로 사용합니다. 다음 예제에서는 숫자 배열에서 `Uint8Array`를 만듭니다.

    const arr = Uint8Array.from([1, 2, 3, 4, 5]);

`Buffer`에서 `Uint8Array`를 생성하기 위해 개발자는 `Uint8Array.from()` 메서드를 사용할 수 있습니다. 이 메서드는 `Buffer`를 인수로 사용합니다. 다음 예제는 `Buffer`에서 `Uint8Array`를 생성합니다.

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const arr = Uint8Array.from(buf);

`Uint8Array`가 생성되면 개발자는 `Uint8Array.set()` 메서드를 사용하여 데이터를 쓸 수 있습니다. 이 메서드는 숫자 배열과 선택적으로 시작 인덱스를 인수로 사용합니다. 시작 인덱스는 숫자 배열이 기록될 `Uint8Array`의 인덱스입니다. 다음 예제는 인덱스 0에서 시작하여 이전 예제에서 생성된 `Uint8Array`에 숫자 `[6, 7, 8, 9, 10]`의 배열을 씁니다.

    arr.set([6, 7, 8, 9, 10], 0);

`Uint8Array`에서 데이터를 읽으려면 개발자가 `Uint8Array.subarray()` 메서드를 사용할 수 있습니다. 이 메서드는 시작 및 끝 인덱스를 인수로 사용합니다. 다음 예제는 이전 예제에서 생성한 `Uint8Array`에서 데이터를 읽어 배열로 출력합니다.

    console.log(arr.subarray(0, 5)); // [1, 2, 3, 4, 5]

## 이진 데이터 유형 간 변환

어떤 경우에는 개발자가 `Buffer`와 `Uint8Array` 사이를 변환해야 할 수도 있습니다. 이는 `Buffer.from()` 및 `Uint8Array.from()` 메서드를 사용하여 수행할 수 있습니다. 다음 예제는 `Uint8Array`에서 `Buffer`를 생성합니다.

    const arr = Uint8Array.from([1, 2, 3, 4, 5]);
    const buf = Buffer.from(arr);

다음 예제는 `Buffer`에서 `Uint8Array`를 생성합니다.

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const arr = Uint8Array.from(buf);

## 결론

개발자는 TypeScript 및 Node.js에서 이진 데이터로 작업하기 위한 다양한 옵션을 사용할 수 있습니다. `Buffer` 클래스는 이진 데이터 작업을 위한 여러 메서드를 제공하고 `Uint8Array` 클래스는 이진 데이터 작업을 위한 대체 방법을 제공합니다. 어떤 경우에는 개발자가 `Buffer`와 `Uint8Array` 사이를 변환해야 할 수도 있습니다.