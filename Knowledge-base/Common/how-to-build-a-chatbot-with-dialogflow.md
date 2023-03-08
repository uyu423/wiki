---
title: Dialogflow로 챗봇을 구축하는 방법
description: 
published: true
date: 2023-03-04T03:32:40.573Z
tags: 
editor: markdown
dateCreated: 2023-03-04T03:32:39.202Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Chatbot with Dialogflow***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-chatbot-with-dialogflow)
{.links-list}
Dialogflow로 챗봇을 구축하는 방법

오늘날의 디지털 커뮤니케이션 시대에 챗봇은 기업이 고객 서비스 및 지원을 자동화하는 데 널리 사용되는 도구가 되었습니다. 이전에 API.ai로 알려졌던 Dialogflow는 개발자가 다양한 플랫폼을 위한 강력한 챗봇을 구축할 수 있게 해주는 자연어 처리(NLP) 플랫폼입니다.

이 튜토리얼에서는 Dialogflow로 챗봇을 구축하는 과정을 안내합니다. 다음 주제를 다룰 것입니다.

- Dialogflow 에이전트 만들기
- 에이전트에 인텐트 추가
- 에이전트에 엔터티 추가
- 이행 이행
- 웹 애플리케이션과 챗봇 통합

## Dialogflow 에이전트 만들기

Dialogflow 에이전트는 챗봇의 핵심 구성요소입니다. 여기에는 대화형 인터페이스를 구축하는 데 필요한 모든 의도, 엔터티 및 이행 논리가 포함됩니다. Dialogflow 에이전트를 만들려면 다음 단계를 따르세요.

1. Dialogflow 콘솔에 로그인합니다.
2. 에이전트 만들기 버튼을 클릭합니다.
3. 상담원 이름을 입력하고 기본 언어와 시간대를 선택합니다.
4. 만들기 버튼을 클릭합니다.

![Dialogflow 에이전트 만들기](https://i.imgur.com/vy8uSed.png)

## 에이전트에 인텐트 추가

의도는 챗봇의 빌딩 블록입니다. 대화 뒤에 있는 사용자의 의도 또는 목표를 나타냅니다. 에이전트에 인텐트를 추가하려면 다음 단계를 따르세요.

1. 왼쪽 메뉴에서 인텐트 탭을 클릭합니다.
2. 인텐트 생성 버튼을 클릭합니다.
3. 의도의 이름을 입력하고 사용자가 의도를 트리거하기 위해 말할 수 있는 몇 가지 샘플 문구를 제공합니다.
4. 훈련 문구 추가 버튼을 클릭하고 문구를 입력하여 인텐트에 훈련 문구를 추가합니다.
5. 응답 또는 처리 웹후크를 추가하여 의도가 트리거될 때 수행해야 하는 작업을 지정합니다.

![에이전트에 인텐트 추가하기](https://i.imgur.com/fyFhLwB.png)

## 에이전트에 엔티티 추가

엔터티는 사용자 입력에서 특정 정보를 추출하는 데 사용됩니다. 예를 들어 사용자가 날씨 업데이트를 요청하면 엔터티는 날씨가 요청된 위치를 추출합니다. 에이전트에 엔티티를 추가하려면 다음 단계를 따르십시오.

1. 왼쪽 메뉴에서 엔티티 탭을 클릭합니다.
2. 엔티티 생성 버튼을 클릭합니다.
3. 엔터티 이름을 입력하고 엔터티 값에 대한 동의어 및 예를 추가합니다.
4. 엔터티를 저장합니다.

![에이전트에 엔티티 추가](https://i.imgur.com/m5y5W5y.png)

## 이행 구현

처리는 인텐트가 트리거될 때 실행되는 논리입니다. 사용자에게 응답을 제공하거나 외부 API를 호출하거나 기타 사용자 지정 논리를 수행하는 데 사용할 수 있습니다. Dialogflow는 두 가지 유형의 이행을 지원합니다.

- 인라인 편집기: Dialogflow 콘솔 내에서 직접 Node.js에 처리 논리를 작성할 수 있습니다.
- Webhook: 이행을 처리하기 위해 외부 서비스를 사용할 수 있습니다.

인라인 편집기를 사용하여 이행을 구현하려면 다음 단계를 따르십시오.

1. 왼쪽 메뉴에서 처리 탭을 클릭합니다.
2. 스위치를 전환하여 인라인 편집기를 활성화합니다.
3. 편집기 내의 index.js 파일에 이행 로직을 작성합니다.

```javascript
function weatherHandler(agent) {
  const city = agent.parameters.city;
  const apiKey = "YOUR_API_KEY";
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}`;
  return axios.get(url)
    .then((response) => {
      const weather = response.data.weather[0].description;
      const temperature = response.data.main.temp;
      agent.add(`The weather in ${city} is ${weather} with a temperature of ${temperature} degrees.`);
    })
    .catch((error) => {
      console.log(error);
      agent.add(`I'm sorry, I couldn't find the weather for ${city}.`);
    });
}

let intentMap = new Map();
intentMap.set('Get Weather', weatherHandler);
agent.handleRequest(intentMap);
```

웹후크를 사용하여 fulfillment를 구현하려면 다음 단계를 따르세요.

1. 왼쪽 메뉴에서 처리 탭을 클릭합니다.
2. Webhook URL 필드에 Webhook 서비스의 URL을 입력합니다.
3. 변경 사항을 저장합니다.

## 웹 애플리케이션과 챗봇 통합

챗봇을 만든 후 Dialogflow Messenger 통합 또는 Dialogflow API를 사용하여 웹 애플리케이션과 통합할 수 있습니다. Dialogflow Messenger 통합을 통해 코드를 변경할 필요 없이 웹사이트에 챗봇을 쉽게 추가할 수 있습니다. Dialogflow Messenger 통합을 사용하여 챗봇을 통합하려면 다음 단계를 따르세요.

1. 왼쪽 메뉴에서 통합 탭을 클릭합니다.
2. Dialogflow 메신저 타일을 클릭합니다.
3. 챗봇의 모양과 동작을 구성합니다.
4. 통합 코드를 복사하여 웹 애플리케이션에 붙여넣습니다.

또는 Dialogflow API를 사용하여 챗봇을 웹 애플리케이션과 통합할 수 있습니다. 이를 위해서는 클라이언트 라이브러리 또는 Axios와 같은 HTTP 클라이언트를 사용하여 API에 HTTP 요청을 해야 합니다. Dialogflow API를 사용하여 챗봇을 통합하려면 다음 단계를 따르세요.

1. Google Cloud Console에서 새 서비스 계정을 만듭니다.
2. 서비스 계정 키를 다운로드하고 JSON 파일로 저장합니다.
3. npm을 사용하여 Dialogflow 클라이언트 라이브러리를 설치합니다.

```bash
npm install dialogflow
```

4. 클라이언트 라이브러리를 사용하여 Dialogflow API에 요청합니다.

```javascript
const dialogflow = require('dialogflow');
const uuid = require('uuid');

const sessionId = uuid.v4();
const sessionClient = new dialogflow.SessionsClient({
  keyFilename: 'path/to/service-account-key.json'
});
const sessionPath = sessionClient.sessionPath('PROJECT_ID', sessionId);

async function sendMessageToDialogFlow(message) {
  const request = {
    session: sessionPath,
    queryInput: {
      text: {
        text: message,
        languageCode: 'en-US'
      }
    }
  };

  const responses = await sessionClient.detectIntent(request);
  const result = responses[0].queryResult;
  return result.fulfillmentText;
}
```

## 결론

이 튜토리얼에서는 Dialogflow로 챗봇을 구축하는 방법을 배웠습니다. Dialogflow 에이전트 생성, 에이전트에 인텐트 및 항목 추가, 이행 논리 구현, 챗봇을 웹 애플리케이션과 통합하는 프로세스를 다루었습니다. 이 가이드에서 얻은 지식을 사용하여 이제 Dialogflow로 나만의 챗봇을 구축하고 사용자에게 원활한 대화 환경을 제공할 수 있습니다.

## 외부 리소스

- [Dialogflow 문서](https://cloud.google.com/dialogflow/docs/)
- [Dialogflow 필수 YouTube 시리즈](https://www.youtube.com/playlist?list=PLIivdWyY5sqJxnwJhe3etaK7utrBiPBQ2)
- [Dialogflow Node.js 클라이언트 라이브러리](https://www.npmjs.com/package/dialogflow)