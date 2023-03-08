---
title: Node.js 및 AI: 실습 가이드
description: 
published: true
date: 2023-02-01T23:57:25.112Z
tags: 
editor: markdown
dateCreated: 2023-02-01T23:57:23.426Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js and AI: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-ai-a-hands-on-guide)
{.links-list}


# Node.js와 AI: 실습 가이드

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 강력한 JavaScript 런타임입니다. 서버 측 및 네트워크 응용 프로그램 개발에 사용됩니다.

AI는 컴퓨터가 스스로 결정을 내리도록 프로그래밍하는 과정입니다. 이는 머신 러닝, 자연어 처리, 예측 분석 등 다양한 방법을 통해 수행할 수 있습니다.

이 기사에서는 Node.js와 AI를 함께 사용하여 강력한 애플리케이션을 만드는 방법을 살펴봅니다. 다음 주제를 다룰 것입니다.

- 개발 환경 설정
- 간단한 AI 애플리케이션 만들기
- Node.js로 기계 학습 사용

## 개발 환경 설정

AI 애플리케이션 개발을 시작하기 전에 개발 환경을 설정해야 합니다. 다음이 필요합니다.

- Node.js
- 텍스트 편집기

### Node.js

Node.js는 [공식 웹 사이트](https://nodejs.org/en/)에서 다운로드하여 설치할 수 있습니다. 설치가 완료되면 다음 명령을 실행하여 버전을 확인할 수 있습니다.

```
node -v
```

### 텍스트 편집기

코드를 편집하려면 텍스트 편집기가 필요합니다. [Sublime Text](https://www.sublimetext.com/), [Atom](https://atom.io/), [Visual Studio Code](https: //code.visualstudio.com/).

## 간단한 AI 애플리케이션 만들기

이제 개발 환경이 설정되었으므로 AI 애플리케이션 생성을 시작할 수 있습니다. `app.js`라는 파일을 생성하여 시작하겠습니다. 이 파일에는 `ai-sdk` 모듈이 필요합니다.

```javascript
const ai = require('ai-sdk');
```

이 모듈은 Node.js 애플리케이션 내에서 AI를 사용할 수 있는 기능을 제공합니다.

다음으로 문자열을 받아 응답을 반환하는 간단한 함수를 만듭니다.

```javascript
function getResponse(input) {
  return "You said: " + input;
}
```

이 함수는 문자열을 입력으로 받고 문자열을 출력으로 반환합니다.

이제 함수가 있으므로 함수를 호출하고 출력을 콘솔에 출력해야 합니다.

```javascript
console.log(getResponse("Hello, world!"));
```

`node` 명령으로 애플리케이션을 실행하면 다음 출력이 표시됩니다.

```
You said: Hello, world!
```

## Node.js로 기계 학습 사용

이 섹션에서는 Node.js에서 기계 학습을 사용하는 방법을 살펴봅니다. 우리는 `brain.js` 모듈을 사용하여 간단한 신경망을 훈련할 것입니다.

먼저 `brain.js` 모듈을 설치해야 합니다.

```
npm install brain.js --save
```

모듈이 설치되면 `app.js` 파일에서 모듈을 요구할 수 있습니다.

```javascript
const brain = require('brain.js');
```

다음으로 신경망을 만들어야 합니다. 입력을 받고 출력을 반환하는 함수를 만들겠습니다.

```javascript
function createNetwork() {
  const net = new brain.NeuralNetwork();

  net.train([
    {input: { r: 0.03, g: 0.7, b: 0.5 }, output: { black: 1 }},
    {input: { r: 0.16, g: 0.09, b: 0.2 }, output: { white: 1 }},
    {input: { r: 0.5, g: 0.5, b: 1.0 }, output: { white: 1 }}
  ]);

  const output = net.run({ r: 1, g: 0.4, b: 0 });  // { white: 0.99, black: 0.002 }

  return output;
}
```

이 기능에서는 `brain.js` 모듈을 사용하여 새로운 신경망을 만듭니다. 그런 다음 세 개의 데이터 포인트로 신경망을 훈련합니다. 첫 번째 데이터 포인트는 `{ r: 0.03, g: 0.7, b: 0.5 }`의 입력이고 출력은 `{ black: 1 }`입니다. 이것은 우리의 신경망이 입력이 `{ r: 0.03, g: 0.7, b: 0.5 }`일 때 출력이 `{ black: 1 }`이어야 한다는 것을 학습한다는 것을 의미합니다. 두 번째 및 세 번째 데이터 포인트에 대해 이 프로세스를 반복합니다.

마지막으로 `{ r: 1, g: 0.4, b: 0 }` 입력으로 신경망을 실행합니다. 그러면 `{ white: 0.99, black: 0.002 }`의 출력이 반환됩니다. 이것은 우리의 신경망이 입력이 '검은색'보다 '흰색'일 가능성이 더 높다고 예측했음을 의미합니다.

이제 신경망을 만들었으므로 이를 사용하여 예측할 수 있습니다. 입력을 받고 예측을 반환하는 함수를 만들 것입니다.

```javascript
function getPrediction(input) {
  const output = createNetwork().run(input);
  const prediction = Object.keys(output)[0];

  return prediction;
}
```

이 함수에서는 먼저 입력으로 신경망을 실행합니다. 그러면 `{ white: 0.99, black: 0.002 }`의 출력이 반환됩니다. 그런 다음 `Object.keys` 메서드를 사용하여 출력(`white`)에서 첫 번째 키를 가져옵니다. 이것은 우리의 예측입니다.

마지막으로 `getPrediction` 함수를 호출하고 예측을 콘솔에 출력합니다.

```javascript
console.log(getPrediction({ r: 1, g: 0.4, b: 0 })); // white
```

`node` 명령으로 애플리케이션을 실행하면 다음 출력이 표시됩니다.

```
white
```

이것은 우리의 신경망이 입력이 '흰색'이라고 올바르게 예측했음을 의미합니다.