---
title: 웹 개발 시작하기: HTML, CSS 및 JavaScript
description: 
published: true
date: 2023-02-15T19:56:07.821Z
tags: 
editor: markdown
dateCreated: 2023-02-15T19:55:59.769Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Getting Started with Web Development: HTML, CSS, and JavaScript***English** document is available*](/en/Knowledge-base/Common/getting-started-with-web-development-html-css-and-javascript)
{.links-list}


# 웹 개발 시작하기: HTML, CSS 및 JavaScript

인터넷은 우리 삶의 필수적인 부분이 되었습니다. 우리는 친구 및 가족과 연락하는 것부터 청구서 지불 및 식료품 구매에 이르기까지 모든 것에 사용합니다. 월드 와이드 웹은 1989년에 처음 발명된 이후 많은 발전을 이루었으며 이제 거의 모든 것을 온라인으로 할 수 있습니다.

자신만의 웹사이트나 웹 애플리케이션을 만들고 싶었다면 운이 좋을 것입니다. 약간의 노하우만 있으면 금방 시작할 수 있습니다. 이 기사에서는 개발 환경 선택에서 첫 번째 코드 작성에 이르기까지 웹 개발의 기본 사항을 안내합니다. 마지막에는 자신의 프로젝트를 시작하는 데 필요한 모든 정보를 갖게 됩니다.

## 웹 개발이란?

웹 개발은 웹사이트를 만들고 유지하는 과정입니다. 처음부터 웹 사이트를 구축하는 것부터 기존 사이트에 새 기능을 추가하는 것까지 모든 것을 포함합니다.

웹 개발은 웹 디자인, 웹 엔지니어링 및 웹 콘텐츠 관리와 같은 다양한 역할을 설명하는 데 사용할 수 있는 광범위한 용어입니다. 일반적으로 웹 개발자는 웹 사이트의 코딩, 디자인 및 레이아웃을 담당합니다. 그들은 또한 웹 서버에서 실행되고 웹 브라우저를 통해 사용자가 액세스하는 프로그램인 웹 응용 프로그램 개발에 관여할 수 있습니다.

## 개발 환경 선택

웹 개발을 시작하는 첫 번째 단계는 개발 환경을 선택하는 것입니다. 코드를 작성하고 프로젝트를 관리하는 데 사용할 소프트웨어입니다.

몇 가지 옵션을 사용할 수 있지만 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 것이 좋습니다. Windows, macOS 및 Linux에서 사용할 수 있는 Microsoft의 무료 오픈 소스 코드 편집기입니다. HTML, CSS 및 JavaScript를 포함한 다양한 프로그래밍 언어를 훌륭하게 지원합니다.

Visual Studio Code를 다운로드하여 설치하면 코딩을 시작할 준비가 된 것입니다.

## 코드의 첫 줄 작성하기

다음 단계는 첫 번째 코드 줄을 작성하는 것입니다. 이를 위해 메모장이나 TextEdit와 같은 간단한 텍스트 편집기를 사용합니다.

텍스트 편집기를 열고 다음을 입력합니다.

```html
<!DOCTYPE html>
<html>
<head>
    <title>My first web page</title>
</head>
<body>
    <h1>Hello, world!</h1>
</body>
</html>
```

이 코드는 제목과 단일 헤더 요소가 있는 기본 웹 페이지를 만듭니다. `<!DOCTYPE html>` 선언은 이것이 HTML 문서임을 웹 브라우저에 알립니다. `<html>`, `<head>` 및 `<body>` 요소는 HTML 페이지의 기본 빌딩 블록입니다. `<head>` 요소는 제목과 같은 페이지에 대한 정보를 포함하고 `<body>` 요소는 페이지의 콘텐츠를 포함합니다.

`<h1>` 요소는 제목 요소이며 페이지에 제목을 만드는 데 사용됩니다. 이 경우 "Hello, world!"라는 제목을 만드는 데 사용했습니다.

파일을 저장하려면 메뉴에서 파일 > 다른 이름으로 저장을 선택하고 파일 유형 드롭다운 메뉴에서 HTML을 선택합니다. 파일 이름을 `index.html`로 지정하고 컴퓨터에 저장합니다.

## 웹페이지 보기

코드의 첫 줄을 작성했으므로 이제 웹 브라우저에서 웹 페이지를 볼 차례입니다.

이렇게 하려면 웹 브라우저에서 방금 만든 index.html 파일을 엽니다. Chrome을 사용하는 경우 메뉴에서 파일 > 파일 열기를 선택하여 이 작업을 수행할 수 있습니다.

다음과 같은 페이지가 표시됩니다.

![](https://i.imgur.com/JD7iK7I.png)

축하해요! 첫 번째 웹 페이지를 만들었습니다.

## CSS로 스타일 추가하기

이제 기본 웹 페이지를 만들었으므로 스타일을 추가할 차례입니다. CSS(Cascading Style Sheets)는 HTML 문서의 스타일을 지정하는 데 사용되는 언어입니다. CSS를 사용하면 웹 페이지의 색상, 글꼴 및 레이아웃을 제어할 수 있습니다.

페이지에 약간의 색상을 추가하여 시작하겠습니다. 페이지에 CSS 규칙을 추가하여 이를 수행할 수 있습니다.

HTML 문서의 `<head>` 요소에 다음 코드를 추가합니다.

```css
<style>
    body {
        background-color: lightblue;
    }
</style>
```

이 코드는 `<body>` 요소의 배경색을 연한 파란색으로 설정하는 CSS 규칙을 추가합니다.

파일을 저장하고 웹 브라우저에서 페이지를 새로 고칩니다. 다음과 같은 페이지가 표시됩니다.

![](https://i.imgur.com/eAoR3zJ.png)

보시다시피 페이지의 배경은 이제 하늘색입니다.

## 자바스크립트로 동작 추가하기

CSS는 HTML 문서의 스타일을 지정하는 데 사용되지만 페이지에 동작을 추가하지는 않습니다. 이를 위해서는 JavaScript를 사용해야 합니다.

JavaScript는 웹 페이지에 상호 작용을 추가하는 데 사용되는 프로그래밍 언어입니다. JavaScript를 사용하면 드롭다운 메뉴, 양식 유효성 검사 및 애니메이션 효과와 같은 항목을 만들 수 있습니다.

페이지에 간단한 JavaScript 함수를 추가해 보겠습니다. HTML 문서의 `<body>` 요소에 다음 코드를 추가합니다.

```javascript
<script>
    function sayHello() {
        alert("Hello, world!");
    }
</script>
```

이 코드는 "Hello, world!"라는 경고 상자를 표시하는 `sayHello()`라는 함수를 정의합니다.

이제 클릭할 때 이 함수를 호출할 요소를 페이지에 추가해야 합니다. HTML 문서의 `<body>` 요소에 다음 코드를 추가합니다.

```html
<button onclick="sayHello()">Click me!</button>
```

이 코드는 클릭 시 `sayHello()` 함수를 호출하는 버튼을 페이지에 추가합니다.

파일을 저장하고 웹 브라우저에서 페이지를 새로 고칩니다. 다음과 같은 버튼이 표시됩니다.

![](https://i.imgur.com/B6iU4TJ.png)

버튼을 클릭하면 다음과 같은 경고 상자가 표시됩니다.

![](https://i.imgur.com/cCk4Afe.png)

축하해요! 웹 페이지에 첫 번째 상호 작용을 추가했습니다.

## 여기서 어디로 갈까

이제 HTML, CSS 및 JavaScript의 기본 사항을 배웠으므로 고유한 웹 페이지 및 웹 응용 프로그램을 만들 준비가 되었습니다. 자세히 알아보려면 아래 리소스 중 일부를 확인하는 것이 좋습니다.

- [W3Schools](https://www.w3schools.com/) - 웹 개발 기술에 대한 자습서 및 참고 자료가 있는 웹 사이트
- [Mozilla 개발자 네트워크](https://developer.mozilla.org/) - 웹 개발 기술에 대한 자습서 및 참고 자료가 있는 웹 사이트
- [코드 아카데미](https://www.codecademy.com/) - 코딩 학습을 위한 온라인 양방향 플랫폼