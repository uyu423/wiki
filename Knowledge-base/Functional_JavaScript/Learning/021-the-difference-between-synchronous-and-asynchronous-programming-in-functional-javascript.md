---
title: 021: 기능적 JavaScript에서 동기 프로그래밍과 비동기 프로그래밍의 차이점
description: 
published: true
date: 2023-02-17T17:06:41.507Z
tags: 
editor: markdown
dateCreated: 2023-02-17T17:06:40.170Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [021: The difference between synchronous and asynchronous programming in functional JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/021-the-difference-between-synchronous-and-asynchronous-programming-in-functional-javascript)
{.links-list}


# 함수형 JavaScript에서 동기 프로그래밍과 비동기 프로그래밍의 차이점

함수형 프로그래밍은 함수를 사용하여 데이터 구조에서 작동하는 프로그래밍 패러다임입니다. 함수형 프로그래밍에서 데이터는 변경할 수 없습니다. 즉 변경할 수 없습니다. 함수는 인수를 취하고 값을 반환하도록 작성됩니다.

자바스크립트는 함수형 프로그래밍 언어입니다. 그것은 함수가 다른 함수에 인수로 전달되고 함수에서 반환될 수 있음을 의미하는 일급 함수를 가지고 있습니다.

프로그래밍에는 동기식과 비동기식의 두 가지 유형이 있습니다. 동기식 프로그래밍에서는 코드가 순서대로 실행됩니다. 비동기 프로그래밍에서 코드는 병렬로 실행됩니다.

동기식 프로그래밍은 코드가 예측 가능한 순서로 실행되기 때문에 추론하기가 더 쉽습니다. 비동기 프로그래밍은 리소스를 더 잘 사용할 수 있기 때문에 더 효율적입니다.

JavaScript에서 모든 코드는 동기식으로 실행됩니다. 그러나 JavaScript에는 코드를 비동기적으로 실행할 수 있는 이벤트 기반 모델이 있습니다.

이벤트는 사용자가 버튼을 클릭하는 것과 같이 브라우저에서 발생하는 동작입니다. 이벤트가 발생하면 이벤트 리스너 함수가 호출됩니다. 이벤트 리스너 함수는 코드를 비동기적으로 실행할 수 있습니다.

JavaScript의 비동기 프로그래밍은 종종 사용자 입력을 처리하거나 서버와 통신하거나 리소스를 로드하는 데 사용됩니다.

다음은 JavaScript에서 비동기 프로그래밍의 예입니다. 아래 코드는 "Hello, world!"를 기록합니다. 버튼을 클릭했을 때 콘솔에:

```javascript
function onClick() {
  console.log("Hello, world!");
}

document.getElementById("button").addEventListener("click", onClick);
```

위의 코드에서 버튼을 클릭하면 onClick 함수가 비동기적으로 실행됩니다.

비동기 프로그래밍은 코드가 순서대로 실행되지 않기 때문에 혼란스러울 수 있습니다. 비동기 코드를 올바르게 작성하려면 JavaScript 이벤트 루프가 작동하는 방식을 이해하는 것이 중요합니다.

이벤트 루프는 이벤트를 확인하고 이벤트 핸들러를 실행하는 메커니즘입니다. 이벤트 루프는 단일 스레드이므로 한 번에 하나의 이벤트만 처리할 수 있습니다.

이벤트가 발생하면 이벤트 핸들러가 이벤트 큐에 추가됩니다. 이벤트 큐는 순서대로 처리되며 이벤트 핸들러는 한 번에 하나씩 실행됩니다.

즉, 이벤트 핸들러를 실행하는 데 시간이 오래 걸리면 이벤트 루프가 다른 이벤트를 처리할 수 없기 때문에 브라우저가 응답하지 않습니다.

이벤트 루프가 다른 이벤트를 계속 처리할 수 있도록 이벤트 핸들러를 짧게 유지하는 것이 중요합니다. 이벤트 처리기가 네트워크 요청과 같은 장기 실행 작업을 수행해야 하는 경우 비동기 함수를 사용해야 합니다.

비동기 함수는 즉시 반환되는 함수입니다. 아래 코드는 비동기 네트워크 요청을 만들고 응답을 콘솔에 기록합니다.

```javascript
function makeRequest() {
  console.log("Making a request...");

  setTimeout(function() {
    console.log("Request made.");
  }, 1000);
}

makeRequest();
```

위의 코드에서 makeRequest 함수는 즉시 반환됩니다. setTimeout 함수는 함수 내부의 코드 실행을 지연시키는 데 사용됩니다.

setTimeout 함수는 실행할 함수와 밀리초 단위의 지연이라는 두 가지 인수를 사용합니다. 이 기능은 지연 후에 실행됩니다.

위의 코드에서 함수는 1000밀리초 또는 1초의 지연 후에 실행됩니다.

비동기 프로그래밍은 코드가 순서대로 실행되지 않기 때문에 추론하기 어려울 수 있습니다. 디버거 문 및 console.log와 같은 도구를 사용하여 코드에서 발생하는 상황을 이해하는 것이 중요합니다.

디버거 문을 사용하여 코드 실행을 일시 중지할 수 있습니다. 아래 코드는 디버거 문을 사용하는 방법을 보여줍니다.

```javascript
function makeRequest() {
  debugger;

  console.log("Making a request...");

  setTimeout(function() {
    console.log("Request made.");
  }, 1000);
}

makeRequest();
```

위의 코드에서 debugger 문은 코드 실행을 일시 중지합니다. 실행을 재개하려면 디버거에서 "재개" 버튼을 사용하십시오.

Console.log는 값을 콘솔에 출력하는 데 사용할 수 있습니다. 아래 코드는 console.log를 사용하는 방법을 보여줍니다.

```javascript
function makeRequest() {
  console.log("Making a request...");

  setTimeout(function() {
    console.log("Request made.");
  }, 1000);
}

makeRequest();
```

위의 코드에서 console.log 문은 "Making a request..." 문자열을 콘솔에 출력합니다.

비동기 프로그래밍은 제대로 하기 어려울 수 있습니다. 디버거 문 및 console.log와 같은 도구를 사용하여 코드에서 발생하는 상황을 이해하는 것이 중요합니다.

비동기 코드를 올바르게 처리하는 라이브러리와 프레임워크를 사용하는 것도 중요합니다. 예를 들어 React는 React Async라는 라이브러리를 사용하여 비동기 코드를 처리합니다.

React Async는 비동기 코드 작업을 위한 일련의 React 구성 요소를 제공하는 라이브러리입니다. React Async는 또한 데이터 로드를 위한 상위 구성 요소를 제공합니다.

아래 코드는 React Async를 사용하여 데이터를 로드하는 방법을 보여줍니다.

```javascript
import React from "react";
import { render } from "react-dom";
import { loadData } from "react-async";

function App() {
  return (
    <div>
      <h1>Hello, world!</h1>
    </div>
  );
}

const AppWithData = loadData(App, {
  loadData: () => fetch("/data.json").then(response => response.json())
});

render(<AppWithData />, document.getElementById("root"));
```

위 코드에서 AppWithData 구성 요소는 데이터를 로드하는 상위 구성 요소입니다. 데이터는 "/data.json" 끝점에서 로드됩니다.

AppWithData 구성 요소는 데이터와 함께 App 구성 요소를 렌더링합니다. 앱 구성 요소는 데이터로 제목을 렌더링합니다.

React Async는 React에서 비동기 코드로 작업하기 쉽게 해주는 라이브러리입니다. 비동기 코드를 올바르게 처리하는 라이브러리와 프레임워크를 사용하는 것이 중요합니다.

# 추가 정보

주제에 대한 추가 정보는 여기에서 찾을 수 있습니다.

- [MDN: 동기 및 비동기 프로그래밍](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts)
- [YouTube: 이벤트 루프란 무엇인가요?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
- [리액트 비동기](https://github.com/react-async/react-async)