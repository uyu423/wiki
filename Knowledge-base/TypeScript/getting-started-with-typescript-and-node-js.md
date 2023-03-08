---
title: TypeScript 및 Node.js 시작하기
description: 
published: true
date: 2023-02-01T10:57:23.747Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:57:22.328Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Getting Started with TypeScript and Node.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/getting-started-with-typescript-and-node-js)
{.links-list}



# TypeScript 및 Node.js 시작하기

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 모든 브라우저. 모든 호스트. 모든 OS. 오픈 소스.

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다.

## TypeScript를 사용하는 이유

TypeScript는 중요한 차이점이 있는 JavaScript입니다. TypeScript가 입력됩니다.

유형을 사용하면 TypeScript가 코드 완성, 리팩토링 및 유형 검사와 같은 주요 이점을 제공할 수 있습니다.

유형을 사용하면 코드를 더 쉽게 문서화할 수도 있습니다. 또한 Visual Studio Code와 같은 IDE와 함께 사용할 경우 형식은 코드 완성 및 인라인 문서를 제공하여 보다 풍부한 개발 환경을 제공할 수 있습니다.

## Node.js를 사용하는 이유

Node.js는 빠르고 확장 가능한 네트워크 애플리케이션을 구축하기 위한 플랫폼입니다.

Node.js는 가볍고 효율적인 이벤트 중심의 비차단 I/O 모델을 사용합니다.

Node.js의 패키지 생태계인 npm은 세계에서 가장 큰 오픈 소스 라이브러리 생태계입니다.

## 시작하기

TypeScript 및 Node.js를 시작하려면 Node.js를 설치해야 합니다.

Node.js가 설치되면 TypeScript 파일을 만들고 `tsc` 명령줄 도구를 사용하여 JavaScript로 컴파일할 수 있습니다.

```
// greeter.ts
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

```
tsc greeter.ts
```

이렇게 하면 컴파일된 JavaScript가 포함된 `greeter.js`라는 파일이 생성됩니다.

컴파일된 JavaScript를 실행하려면 Node.js 런타임을 사용해야 합니다.

```
node greeter.js
```

기존 JavaScript 코드와 함께 TypeScript를 사용할 수도 있습니다.

```
// greeter.ts
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

```
// greeter.js
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

## TypeScript 및 Node.js 리소스

- [타입스크립트](https://www.typescriptlang.org/)
- [Node.js](https://nodejs.org/)
- [비주얼 스튜디오 코드](https://code.visualstudio.com/)