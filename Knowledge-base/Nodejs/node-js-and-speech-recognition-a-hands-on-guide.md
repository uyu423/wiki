---
title: Node.js 및 음성 인식: 실습 가이드
description: 
published: true
date: 2023-02-02T06:36:44.705Z
tags: 
editor: markdown
dateCreated: 2023-02-02T06:36:43.019Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js and Speech Recognition: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-speech-recognition-a-hands-on-guide)
{.links-list}


# Node.js 및 음성 인식: 실습 가이드

### 소개

이 기사에서는 음성 인식에 Node.js를 사용하는 방법을 살펴봅니다. 기본 Node.js 프로젝트를 설정하는 방법, 인기 있는 `recognize-speech` 라이브러리를 사용하여 음성을 인식하는 방법 및 Google Cloud Speech-to-Text를 사용하여 음성을 인식하는 방법을 살펴보겠습니다.

또한 이러한 도구를 사용하여 컴퓨터를 제어하는 데 사용할 수 있는 간단한 음성 인식 앱을 빌드하는 방법도 살펴보겠습니다.

### Node.js 프로젝트 설정

음성 인식을 사용하기 전에 Node.js 프로젝트를 설정해야 합니다. 이전에 Node.js를 사용해 본 적이 없더라도 걱정하지 마세요. 시작하기가 매우 쉽습니다.

먼저 Node.js를 설치해야 합니다. Node.js 웹 사이트로 이동하여 운영 체제에 맞는 설치 프로그램을 다운로드하면 됩니다.

Node.js가 설치되면 새 프로젝트를 만들 수 있습니다. 프로젝트의 새 디렉터리를 만든 다음 npm을 사용하여 프로젝트를 초기화합니다.

```
$ mkdir my-project
$ cd my-project
$ npm init
```

그러면 프로젝트에 `package.json` 파일이 생성됩니다. 이 파일에는 프로젝트에 필요한 종속성을 포함하여 프로젝트에 대한 메타데이터가 포함되어 있습니다.

다음으로 `recognize-speech` 라이브러리를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
$ npm install --save recognize-speech
```

이렇게 하면 `recognize-speech` 라이브러리가 설치되고 `package.json` 파일의 `dependencies` 섹션에 추가됩니다.

### `recognize-speech` 라이브러리로 음성 인식하기

이제 기본 Node.js 프로젝트가 설정되었으므로 `recognize-speech` 라이브러리를 사용하여 음성을 인식할 수 있습니다.

`recognize-speech` 라이브러리는 음성 인식을 위한 간단한 API를 제공합니다. 이를 사용하려면 먼저 `recognizer` 개체를 만들어야 합니다.

```javascript
var Recognizer = require('recognize-speech');

var recognizer = new Recognizer();
```

다음으로 `speech` 이벤트에 대한 이벤트 핸들러를 등록해야 합니다.

```javascript
recognizer.on('speech', function(data) {
  // The data object contains the recognized text
  console.log(data.text);
});
```

마지막으로 인식 프로세스를 시작해야 합니다. `recognize` 메서드를 호출하여 이를 수행할 수 있습니다.

```javascript
recognizer.recognize('speech.wav');
```

이렇게 하면 인식 프로세스가 시작되고 인식된 텍스트가 콘솔에 인쇄됩니다.

### Google Cloud Speech-to-Text 사용

Google Cloud Speech-to-Text는 음성 인식에 사용할 수 있는 클라우드 기반 음성 인식 서비스입니다. 이를 사용하려면 먼저 `speech` 개체를 만들어야 합니다.

```javascript
var Speech = require('@google-cloud/speech');

var speech = new Speech();
```

다음으로 `data` 이벤트에 대한 이벤트 핸들러를 등록해야 합니다.

```javascript
speech.on('data', function(data) {
  // The data object contains the recognized text
  console.log(data.text);
});
```

마지막으로 인식 프로세스를 시작해야 합니다. `recognize` 메서드를 호출하여 이를 수행할 수 있습니다.

```javascript
speech.recognize('speech.wav');
```

이렇게 하면 인식 프로세스가 시작되고 인식된 텍스트가 콘솔에 인쇄됩니다.

### 음성 인식 앱 구축

이제 음성 인식에 Node.js를 사용하는 방법을 살펴보았으므로 컴퓨터를 제어하는 데 사용할 수 있는 간단한 음성 인식 앱을 빌드해 보겠습니다.

앱은 `recognize-speech` 라이브러리를 사용하여 음성을 인식하고 `osascript` 라이브러리를 사용하여 컴퓨터를 제어합니다.

먼저 `osascript` 라이브러리를 설치해야 합니다.

```
$ npm install --save osascript
```

다음으로 코드에서 `osascript` 라이브러리를 요구해야 합니다.

```javascript
var osascript = require('osascript');
```

이제 `recognize` 함수를 작성할 수 있습니다.

```javascript
function recognize(speech, callback) {
  // ...
}
```

이 함수는 음성 녹음을 입력으로 사용하고 `recognize-speech` 라이브러리의 `recognize` 메서드를 호출합니다. 인식에 성공하면 인식된 텍스트로 `callback` 함수를 호출합니다.

마지막으로 `main` 함수를 작성해야 합니다.

```javascript
function main() {
  // ...
}
```

이 함수는 앱이 시작될 때 호출됩니다. `recognizer` 객체를 생성하고 `speech` 이벤트에 대한 이벤트 핸들러를 등록합니다.

`speech` 이벤트가 트리거되면 음성 녹음과 함께 `recognize` 기능을 호출합니다. 인식에 성공하면 `osascript` 라이브러리를 사용하여 컴퓨터를 제어합니다.

앱을 실행하려면 다음 명령을 사용할 수 있습니다.

```
$ node app.js
```

### 결론

이 기사에서는 음성 인식에 Node.js를 사용하는 방법을 살펴보았습니다. 기본 Node.js 프로젝트를 설정하는 방법, `recognize-speech` 라이브러리를 사용하여 음성을 인식하는 방법 및 Google Cloud Speech-to-Text를 사용하는 방법을 살펴보았습니다.

또한 이러한 도구를 사용하여 컴퓨터를 제어하는 데 사용할 수 있는 간단한 음성 인식 앱을 빌드하는 방법도 살펴보았습니다.