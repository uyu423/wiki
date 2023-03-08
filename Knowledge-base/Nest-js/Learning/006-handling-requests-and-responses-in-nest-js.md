---
title: 006: Nest.js에서 요청 및 응답 처리
description: 
published: true
date: 2023-02-14T17:32:29.857Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:32:27.903Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [006: Handling requests and responses in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/006-handling-requests-and-responses-in-nest-js)
{.links-list}


## 소개

Nest.js에서 요청 및 응답 처리는 2단계 프로세스입니다. 먼저 들어오는 요청을 받고 처리할 요청 처리기를 만들어야 합니다. 둘째, 처리된 데이터를 다시 클라이언트로 보낼 응답 핸들러를 만들어야 합니다.

요청 핸들러를 만드는 것은 간단합니다. 요청 및 응답 개체를 받는 함수를 만든 다음 해당 함수 내에 코드를 작성하기만 하면 됩니다.

```javascript
function requestHandler(req, res) {
  // your code here
}
```

요청 개체에는 URL, 헤더 및 본문과 같은 들어오는 요청에 대한 정보가 포함되어 있습니다. 응답 개체는 데이터를 클라이언트로 다시 보내는 데 사용됩니다.

응답 핸들러를 만드는 것도 마찬가지로 간단합니다. 데이터 개체와 응답 개체를 받는 함수를 만든 다음 해당 함수 내에 코드를 작성하기만 하면 됩니다.

```javascript
function responseHandler(data, res) {
  // your code here
}
```

데이터 개체에는 클라이언트에 다시 보내려는 데이터가 포함되어 있습니다. 응답 개체는 데이터를 다시 클라이언트로 보내는 데 사용됩니다.

## 응답 보내기

요청 및 응답 처리기를 만든 후에는 응답을 클라이언트에 다시 보내는 방법을 Nest.js에 알려야 합니다. 이것은 ```res.send()``` 함수를 사용하여 수행됩니다.

```javascript
function responseHandler(data, res) {
  res.send(data, 200);
}
```res.send()``` 함수를 사용하는 방법의 예입니다.

```javascript
function responseHandler(data, res) {
  res.json(data, 200);
}
```

## JSON 응답 보내기

JSON 응답을 보내려면 ```res.json()``` 함수를 사용할 수 있습니다. ```res.json()``` 함수는 보낼 데이터와 HTTP 상태 코드라는 두 가지 인수를 취합니다.

다음은 ```res.json()``` 함수를 사용하는 방법의 예입니다.

```javascript
function responseHandler(data, res) {
  res.render('index.html', data);
}
```

## HTML 응답 보내기

HTML 응답을 보내려면 ```res.render()``` 기능을 사용할 수 있습니다. ```res.render()``` 함수는 HTML 파일의 경로와 HTML 파일에 전달할 데이터를 포함하는 객체라는 두 가지 인수를 취합니다.

다음은 ```res.render()``` 함수를 사용하는 방법의 예입니다.

```javascript
function responseHandler(data, res) {
  res.sendFile('/path/to/file.txt', {
    root: __dirname
  });
}
```

## 파일 보내기

파일을 보내려면 ```res.sendFile()``` 기능을 사용할 수 있습니다. ```res.sendFile()``` 함수는 파일 경로와 파일 전송 옵션을 포함하는 객체라는 두 가지 인수를 취합니다.

다음은 ```res.sendFile()``` 함수를 사용하는 방법의 예입니다.

```javascript
function responseHandler(data, res) {
  res.redirect('/path/to/new/page');
}
```

## 리디렉션 보내기

리디렉션을 보내려면 ```res.redirect()``` 기능을 사용할 수 있습니다. ```res.redirect()``` 함수는 리디렉션할 URL이라는 하나의 인수를 사용합니다.

다음은 ```res.redirect()``` 함수를 사용하는 방법의 예입니다.

```자바스크립트
함수 responseHandler(데이터, 입술) {
  res.redirect('/path/to/new/page');
}
```

## 결론

Nest.js에서 요청 및 응답 처리는 2단계 프로세스입니다. 먼저 들어오는 요청을 받고 처리할 요청 처리기를 만들어야 합니다. 둘째, 처리된 데이터를 다시 클라이언트로 보낼 응답 핸들러를 만들어야 합니다.

요청 핸들러를 만드는 것은 간단합니다. 요청 및 응답 개체를 받는 함수를 만든 다음 해당 함수 내에 코드를 작성하기만 하면 됩니다.

응답 핸들러를 만드는 것도 마찬가지로 간단합니다. 데이터 개체와 응답 개체를 받는 함수를 만든 다음 해당 함수 내에 코드를 작성하기만 하면 됩니다.

요청 및 응답 처리기를 만든 후에는 응답을 클라이언트에 다시 보내는 방법을 Nest.js에 알려야 합니다. 이것은 ```res.send()``` 함수를 사용하여 수행됩니다.

JSON 응답을 보내려면 ```res.json()``` 함수를 사용할 수 있습니다. HTML 응답을 보내려면 ```res.render()``` 기능을 사용할 수 있습니다. 파일을 보내려면 ```res.sendFile()``` 기능을 사용할 수 있습니다. 리디렉션을 보내려면 ```res.redirect()``` 기능을 사용할 수 있습니다.