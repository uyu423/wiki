---
title: 060: Node.js에서 WebRTC와 함께 TensorFlow.js 사용
description: 
published: true
date: 2023-02-02T21:05:32.472Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:05:30.666Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [060: Using TensorFlow.js with WebRTC in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/060-using-tensorflow-js-with-webrtc-in-node-js)
{.links-list}


# Node.js에서 WebRTC와 함께 TensorFlow.js 사용

이 게시물에서는 Node.js에서 WebRTC와 함께 TensorFlow.js를 사용하는 방법을 보여드리겠습니다. 개발 환경을 설정하는 방법, WebRTC와 함께 TensorFlow.js를 사용하는 방법, 애플리케이션을 배포하는 방법을 살펴보겠습니다.

## 개발 환경 설정

시작하기 전에 개발 환경을 설정해야 합니다. Node.js와 TensorFlow.js Node.js 라이브러리를 설치해야 합니다.

### Node.js 설치하기

먼저 Node.js를 설치해야 합니다. [Node.js 웹사이트](https://nodejs.org/en/)에서 Node.js 설치 프로그램을 다운로드할 수 있습니다. 설치 프로그램을 실행하고 프롬프트에 따라 Node.js를 설치합니다.

Node.js가 설치되면 터미널을 열고 다음 명령을 실행하여 작동하는지 확인할 수 있습니다.

```
node -v
```

터미널에 인쇄된 Node.js 버전 번호가 표시되어야 합니다.

### TensorFlow.js Node.js 라이브러리 설치

이제 Node.js가 설치되었으므로 TensorFlow.js Node.js 라이브러리를 설치할 수 있습니다. Node.js 패키지 관리자인 npm을 사용하여 이 작업을 수행할 수 있습니다.

먼저 package.json 파일을 만들어야 합니다. 이 파일에는 설치하려는 종속성을 포함하여 프로젝트에 대한 정보가 포함됩니다. 다음 명령을 사용하여 package.json 파일을 만들 수 있습니다.

```
npm init
```

그러면 프로젝트에 대한 몇 가지 정보를 묻는 메시지가 표시됩니다. Enter 키를 눌러 기본값을 수락할 수 있습니다.

다음으로 TensorFlow.js Node.js 라이브러리를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

그러면 TensorFlow.js Node.js 라이브러리와 필요한 기타 종속 항목이 설치됩니다.

## WebRTC와 함께 TensorFlow.js 사용

이제 개발 환경이 설정되었으므로 WebRTC와 함께 TensorFlow.js를 사용할 수 있습니다.

WebRTC는 브라우저 간의 실시간 통신을 가능하게 하는 기술입니다. TensorFlow.js는 기계 학습을 위한 JavaScript 라이브러리입니다. 이 두 가지 기술을 함께 사용하여 실시간 머신 러닝을 수행할 수 있는 애플리케이션을 구축할 수 있습니다.

### 시작하기

시작하려면 HTML 파일을 만들어야 합니다. [VS Code](https://code.visualstudio.com/)와 같은 텍스트 편집기로 이 작업을 수행할 수 있습니다.

이 파일에 TensorFlow.js 라이브러리를 포함해야 합니다. HTML 파일의 헤드에 다음 스크립트 태그를 추가하여 이를 수행할 수 있습니다.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

WebRTC 어댑터도 포함해야 합니다. 이것은 서로 다른 브라우저의 WebRTC 구현 간에 호환성을 제공하는 JavaScript 라이브러리입니다. 다음 스크립트 태그와 함께 WebRTC 어댑터를 포함할 수 있습니다.

```html
<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
```

TensorFlow.js Node.js 라이브러리도 포함해야 합니다. 스크립트 태그를 사용하여 이 작업을 수행할 수 있습니다.

```html
<script src="./node_modules/@tensorflow/tfjs-node/dist/tfjs-node.js"></script>
```

### WebRTC 연결 만들기

이제 TensorFlow.js 및 WebRTC 라이브러리가 포함되었으므로 이를 사용할 수 있습니다.

먼저 WebRTC 연결을 생성해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // Create an offer
    peerConnection.createOffer()
      .then(function (offer) {
        // Set the offer as the local description
        peerConnection.setLocalDescription(offer);

        // Send the offer to the remote peer
        // ...
      });
  });
```

이 코드에서는 먼저 사용자의 미디어 스트림을 가져옵니다. 이렇게 하면 사용자의 웹캠과 마이크에 액세스할 수 있습니다. 그런 다음 WebRTC 연결을 생성합니다. 이 연결은 사용자의 브라우저를 원격 피어에 연결하는 데 사용됩니다.

다음으로 사용자의 미디어 스트림을 연결에 추가합니다. 이렇게 하면 원격 피어가 사용자를 보고 들을 수 있습니다.

그런 다음 제안을 작성합니다. 이것은 사용자의 미디어 스트림과 사용자 브라우저의 기능에 대한 설명입니다. 이 제안을 지역 설명으로 설정했습니다. 이는 원격 피어에서 사용자에게 연결하는 데 사용됩니다.

마지막으로 원격 피어에 제안을 보냅니다. 원격 피어는 이 제안을 사용하여 사용자에게 연결합니다.

### 오퍼 받기

제안을 만드는 방법을 살펴보았으니 이제 제안을 받는 방법을 살펴보겠습니다.

원격 피어가 제안을 보내면 이를 원격 설명으로 설정해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // When we receive an offer
    peerConnection.on('offer', function (offer) {
      // Set the offer as the remote description
      peerConnection.setRemoteDescription(offer);

      // Create an answer
      peerConnection.createAnswer()
        .then(function (answer) {
          // Set the answer as the local description
          peerConnection.setLocalDescription(answer);

          // Send the answer to the remote peer
          // ...
        });
    });
  });
```

이 코드에서는 먼저 사용자의 미디어 스트림을 가져옵니다. 이렇게 하면 사용자의 웹캠과 마이크에 액세스할 수 있습니다. 그런 다음 WebRTC 연결을 생성합니다. 이 연결은 사용자의 브라우저를 원격 피어에 연결하는 데 사용됩니다.

다음으로 사용자의 미디어 스트림을 연결에 추가합니다. 이렇게 하면 원격 피어가 사용자를 보고 들을 수 있습니다.

그런 다음 제안을 받을 때 이벤트 리스너를 설정합니다. 제안을 받으면 원격 설명으로 설정합니다.

마지막으로 답을 만듭니다. 이것은 사용자의 미디어 스트림과 사용자 브라우저의 기능에 대한 설명입니다. 이 답변을 로컬 설명으로 설정했습니다. 이는 원격 피어에서 사용자에게 연결하는 데 사용됩니다.

### 답변 보내기

답변을 만드는 방법을 살펴보았으니 이제 답변을 보내는 방법을 살펴보겠습니다.

원격 피어가 응답을 보내면 이를 원격 설명으로 설정해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
// Get the user's media stream
navigator.mediaDevices.getUserMedia({ video: true, audio: true })
  .then(function (mediaStream) {
    // Create a WebRTC connection
    const peerConnection = new RTCPeerConnection();

    // Add the media stream to the connection
    peerConnection.addStream(mediaStream);

    // When we receive an answer
    peerConnection.on('answer', function (answer) {
      // Set the answer as the remote description
      peerConnection.setRemoteDescription(answer);
    });

    // Create an offer
    peerConnection.createOffer()
      .then(function (offer) {
        // Set the offer as the local description
        peerConnection.setLocalDescription(offer);

        // Send the offer to the remote peer
        // ...
      });
  });
```

이 코드에서는 먼저 사용자의 미디어 스트림을 가져옵니다. 이렇게 하면 사용자의 웹캠과 마이크에 액세스할 수 있습니다. 그런 다음 WebRTC 연결을 생성합니다. 이 연결은 사용자의 브라우저를 원격 피어에 연결하는 데 사용됩니다.

다음으로 사용자의 미디어 스트림을 연결에 추가합니다. 이렇게 하면 원격 피어가 사용자를 보고 들을 수 있습니다.

그런 다음 응답을 받을 때 이벤트 리스너를 설정합니다. 답변을 받으면 원격 설명으로 설정합니다.

마지막으로 제안을 작성합니다. 이것은 사용자의 미디어 스트림과 사용자 브라우저의 기능에 대한 설명입니다. 이 제안을 지역 설명으로 설정했습니다. 이는 원격 피어에서 사용자에게 연결하는 데 사용됩니다.

## 애플리케이션 배포

WebRTC와 함께 TensorFlow.js를 사용하는 방법을 살펴보았으니 이제 애플리케이션을 배포하는 방법을 살펴보겠습니다.

HTML 파일을 제공하려면 웹 서버를 사용해야 합니다. [Node.js HTTP 모듈](https://nodejs.org/api/http.html)로 이를 수행할 수 있습니다.

먼저 `server.js`라는 파일을 만들어야 합니다. 이 파일에서 `http` 모듈이 필요하고 HTTP 서버를 생성합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const http = require('http');

const server = http.createServer(function (request, response) {
  // Serve the HTML file
  // ...
});

server.listen(8080);
```

이 코드에서는 `http` 모듈이 필요합니다. 이 모듈은 HTTP 서버와 클라이언트에 대한 액세스를 제공합니다. 그런 다음 HTTP 서버를 만듭니다. 이 서버는 HTML 파일을 제공하는 데 사용됩니다.

다음으로 서버에 제공할 파일을 알려야 합니다. `createServer` 콜백에 다음 코드를 추가하여 이를 수행할 수 있습니다.

```javascript
const fs = require('fs');

const index = fs.readFileSync('./index.html');

response.writeHead(200, { 'Content-Type': 'text/html' });
response.end(index);
```

이 코드에서는 `fs` 모듈이 필요합니다. 이 모듈은 파일 시스템에 대한 액세스를 제공합니다. 그런 다음 HTML 파일의 내용을 변수로 읽습니다.

마지막으로 HTML 파일의 내용을 응답에 작성합니다. 또한 `Content-Type` 헤더를 `text/html`로 설정합니다. 이렇게 하면 파일이 HTML 파일임을 브라우저에 알릴 수 있습니다.

## 결론

이 게시물에서는 Node.js에서 WebRTC와 함께 TensorFlow.js를 사용하는 방법을 보여주었습니다. 개발 환경을 설정하는 방법, WebRTC와 함께 TensorFlow.js를 사용하는 방법, 애플리케이션을 배포하는 방법을 살펴보았습니다.