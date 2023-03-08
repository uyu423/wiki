---
title: IBM Watson 및 Node-RED로 챗봇을 구축하는 방법
description: 
published: true
date: 2023-02-24T07:33:18.047Z
tags: 
editor: markdown
dateCreated: 2023-02-24T07:33:16.672Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Chatbot with IBM Watson and Node-RED***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-chatbot-with-ibm-watson-and-node-red)
{.links-list}


# IBM Watson 및 Node-RED로 챗봇을 구축하는 방법

요즘 챗봇은 고객과 소통하거나 간단한 작업을 수행하는 데 널리 사용되며 그 인기는 점점 높아지고 있습니다. 기업은 챗봇이 지치지 않고 24시간 연중무휴 많은 양의 요청을 처리할 수 있고 휴식이 필요하지 않으며 빠르고 저렴하게 배포할 수 있기 때문에 가치가 있다고 생각합니다.

챗봇을 구축하는 방법에는 여러 가지가 있지만 이 기사에서는 IBM Watson 및 Node-RED를 사용하여 구축하는 방법에 중점을 둘 것입니다. Node-RED는 Node.js에서 실행되는 시각적 프로그래밍 도구이며 팔레트의 광범위한 노드를 사용하여 흐름을 쉽게 연결할 수 있습니다. 또한 Watson을 비롯한 IBM 클라우드 서비스와 상호 작용하기 위한 기본 제공 라이브러리가 있습니다.

## Node-RED 설정

가장 먼저 해야 할 일은 Node-RED를 설정하는 것입니다. Node.js가 아직 설치되어 있지 않다면 [Node.js 웹사이트](https://nodejs.org/en/)에서 다운로드할 수 있습니다.

Node.js가 설치되면 다음 명령을 사용하여 Node-RED를 설치할 수 있습니다.

```
npm install -g node-red
```

Node-RED가 설치되면 다음 명령을 실행하여 시작할 수 있습니다.

```
node-red
```

이렇게 하면 Node-RED 서버가 시작되고 브라우저에서 Node-RED 웹 인터페이스가 열립니다.

## 왓슨 설정하기

이제 Node-RED를 설치하고 실행했으므로 IBM Watson 서비스를 설정해야 합니다. [IBM Cloud 카탈로그](https://catalog.cloud.ibm.com/)로 이동하고 다음 서비스의 새 인스턴스를 작성하여 이를 수행할 수 있습니다.

- 왓슨 어시스턴트
- 텍스트 음성
- 텍스트 음성 변환

Watson 서비스를 생성한 후에는 각 서비스에 대한 **Service Credentials** 탭으로 이동하여 새로운 자격 증명 세트를 생성해야 합니다. 나중에 필요하므로 이러한 자격 증명을 안전한 곳에 복사하십시오.

## 흐름 만들기

이제 Node-RED와 Watson이 설정되었으므로 챗봇 흐름 생성을 시작할 수 있습니다. 이렇게 하려면 Node-RED 웹 인터페이스로 이동하여 **Create new flow** 버튼을 클릭합니다.

![새 흐름 만들기 버튼](https://i.imgur.com/lU4kbjN.png)

그러면 Node-RED 흐름 편집기가 열립니다. 가장 먼저 해야 할 일은 팔레트에서 **http in** 노드를 드래그하여 캔버스에 놓는 것입니다.

![노드의 http](https://i.imgur.com/mUJygcT.png)

그런 다음 http in 노드를 두 번 클릭하여 노드 구성을 엽니다. **URL** 필드에 `/chatbot`을 입력합니다. 챗봇에 액세스할 수 있는 URL입니다. **방법** 필드에서 'POST'를 선택합니다. **이름** 필드를 비워두고 **완료** 버튼을 클릭합니다.

![노드 구성의 http](https://i.imgur.com/pzMgASN.png)

이제 팔레트에서 **IBM Watson** 노드를 끌어서 캔버스에 놓습니다. **http in** 노드를 **IBM Watson** 노드에 연결합니다.

![IBM Watson 노드](https://i.imgur.com/JjlbTGi.png)

**IBM Watson** 노드를 두 번 클릭하여 노드 구성을 엽니다. **Service** 필드에서 이전에 생성한 **Assistant** 서비스를 선택합니다. **어시스턴트 ID** 필드에 서비스의 **어시스턴트 ID**를 입력합니다. 이것은 서비스의 **Service Credentials** 탭에서 찾을 수 있습니다. **API 키** 필드에 서비스의 **API 키**를 입력합니다. 이는 서비스의 **Service Credentials** 탭에서도 찾을 수 있습니다.

![IBM Watson 노드 구성](https://i.imgur.com/vALDKJs.png)

다음으로 팔레트에서 **http 응답** 노드를 드래그하여 캔버스에 놓습니다. **IBM Watson** 노드를 **http 응답** 노드에 연결합니다.

![http 응답 노드](https://i.imgur.com/Wql4v1B.png)

이제 사용자 입력을 Watson Assistant로 보내도록 **IBM Watson** 노드를 구성해야 합니다. 이렇게 하려면 **IBM Watson** 노드를 두 번 클릭하여 노드 구성을 엽니다. **Input** 필드에 `{ "text": "$input.body" }`를 입력합니다. 이렇게 하면 사용자 입력이 `{ "text": "user input" }` 형식의 JSON으로 Watson Assistant에 전송됩니다. **Output** 필드에서 `$output.intents[0].intent`의 기본값을 그대로 둡니다. 이렇게 하면 노드가 Watson Assistant가 감지한 첫 번째 인텐트를 출력하게 됩니다.

![IBM Watson 노드 구성](https://i.imgur.com/FtWfZoG.png)

이제 **IBM Watson** 노드의 출력을 다시 사용자에게 보내도록 **http 응답** 노드를 구성해야 합니다. 이렇게 하려면 **http 응답** 노드를 두 번 클릭하여 노드 구성을 엽니다. **상태 코드** 필드에 `200`을 입력합니다. 이렇게 하면 성공적인 HTTP 응답이 사용자에게 다시 전송됩니다. **메시지** 필드에 `$output.text`를 입력합니다. 그러면 **IBM Watson** 노드의 출력 텍스트가 사용자에게 다시 전송됩니다.

![http 응답 노드 구성](https://i.imgur.com/eLKcnpz.png)

이제 챗봇 흐름을 배포해야 합니다. 이렇게 하려면 화면 오른쪽 상단에 있는 **배포** 버튼을 클릭합니다.

![배포 버튼](https://i.imgur.com/pzMgASN.png)

이렇게 하면 챗봇 흐름이 배포되고 이전에 지정한 URL에서 액세스할 수 있습니다.

## 챗봇 테스트

챗봇을 테스트하려면 이전에 `{ "text": "user input" }` 형식의 JSON 본문을 사용하여 지정한 URL로 POST 요청을 보낼 수 있습니다.

예를 들어 다음 JSON 본문을 챗봇 URL로 전송하는 경우:

```
{
  "text": "Hello"
}
```

챗봇은 다음 JSON 본문으로 응답합니다.

```
{
  "text": "Hello, how are you?"
}
```

[cURL](https://curl.haxx.se/) 명령줄 도구를 사용하여 챗봇을 테스트할 수도 있습니다. 이렇게 하려면 다음 명령을 사용할 수 있습니다.

```
curl -X POST -H "Content-Type: application/json" -d '{"text": "Hello"}' <chatbot URL>
```

`<chatbot URL>`을 챗봇의 URL로 바꿉니다.

## 결론

이 기사에서는 IBM Watson 및 Node-RED를 사용하여 챗봇을 구축하는 방법을 보여주었습니다. 또한 cURL 명령줄 도구를 사용하여 챗봇을 테스트하는 방법도 보여 드렸습니다.

챗봇 구축에 대해 자세히 알아보려면 다음 리소스를 권장합니다.

- [왓슨 어시스턴트로 챗봇 만들기](https://www.ibm.com/cloud/garage/content/course/building-chatbots-with-watson-assistant/)
- [왓슨 어시스턴트로 챗봇 만들기](https://developer.ibm.com/patterns/build-a-chatbot-with-watson-assistant/)
- [챗봇 만드는 방법](https://chatbotsmagazine.com/how-to-build-a-chatbot-4bca7aa8e4d0)