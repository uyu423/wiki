---
title: 058: TensorFlow.js 및 Node.js 애플리케이션 테스트
description: 
published: true
date: 2023-02-02T20:36:35.181Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:36:33.574Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [058: Testing TensorFlow.js and Node.js Applications***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/058-testing-tensorflow-js-and-node-js-applications)
{.links-list}


# 058: TensorFlow.js 및 Node.js 애플리케이션 테스트

## 소개

이 게시물에서는 TensorFlow.js 및 Node.js 애플리케이션을 테스트하는 방법을 살펴보겠습니다. 다양한 유형의 테스트, 테스트 환경 설정 방법 및 테스트 실행 방법을 다룹니다.

## 테스트 유형

테스트에는 단위 테스트와 종단 간 테스트의 두 가지 주요 유형이 있습니다.

단위 테스트는 함수나 클래스와 같은 개별 코드 조각을 테스트하는 데 사용됩니다. 일반적으로 코드를 작성한 개발자가 작성합니다.

종단 간 테스트는 처음부터 끝까지 전체 애플리케이션을 테스트하는 데 사용됩니다. 일반적으로 별도의 테스터 팀이 작성합니다.

## 테스트 환경 설정

테스트 작성을 시작하기 전에 테스트 환경을 설정해야 합니다.

이를 수행하는 방법에는 여러 가지가 있지만 테스트 프레임워크를 사용하는 가장 일반적인 방법을 다룰 것입니다.

테스트 프레임워크는 테스트 작성 및 실행을 위한 일련의 도구를 제공하는 소프트웨어입니다. JavaScript용으로 가장 널리 사용되는 테스트 프레임워크는 Jest입니다.

Jest를 사용하려면 먼저 설치해야 합니다. 명령줄 또는 npm과 같은 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```
npm install --save-dev jest
```

Jest가 설치되면 구성 파일을 만들어야 합니다. 이 파일은 Jest에게 테스트 실행 방법을 알려줍니다.

이를 수행하는 가장 간단한 방법은 프로젝트의 루트에 jest.config.js라는 파일을 만드는 것입니다.

```js
module.exports = {
  // your config here
};
```

JSON 파일 또는 XML 파일을 사용할 수도 있습니다.

구성 파일이 있으면 테스트가 있는 위치를 Jest에 알려야 합니다. "testMatch" 속성을 설정하여 이를 수행할 수 있습니다.

```js
module.exports = {
  testMatch: ['**/__tests__/**/*.js?(x)']
};
```

이것은 Jest에게 __tests__ 디렉토리에서 .js 또는 .jsx로 끝나는 모든 파일을 찾도록 지시합니다.

## 테스트 작성

이제 테스트 환경이 설정되었으므로 테스트 작성을 시작할 수 있습니다.

테스트는 JavaScript로 작성됩니다. 일반적으로 __tests__ 디렉토리에 있지만 원하는 곳에 둘 수 있습니다.

테스트는 "테스트 사례"와 "예상 결과"의 두 부분으로 구성됩니다.

테스트 케이스는 테스트 중인 코드를 실행하는 코드 조각입니다. 예를 들어 두 개의 숫자를 더하는 함수를 테스트하는 경우 테스트 사례는 다음과 같을 수 있습니다.

```js
// test case
const result = add(1, 2);

// expected outcome
expect(result).toBe(3);
```

"예상 결과"는 코드가 수행할 것으로 기대하는 것입니다. 이 경우 결과는 3이 될 것으로 예상합니다.

테스트 중인 코드가 예상한 결과를 생성하지 않으면 테스트가 실패합니다.

## 테스트 실행

테스트를 작성하고 나면 명령줄이나 npm과 같은 패키지 관리자를 사용하여 테스트를 실행할 수 있습니다.

```
npm test
```

이렇게 하면 프로젝트의 모든 테스트가 실행됩니다.

테스트 또는 그룹의 이름을 전달하여 특정 테스트 또는 테스트 그룹을 실행할 수도 있습니다.

```
npm test my-test
```

```
npm test my-test-group
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js 애플리케이션을 테스트하는 방법을 다루었습니다. 다양한 유형의 테스트, 테스트 환경 설정 방법, 테스트 작성 및 실행 방법을 다루었습니다.