---
title: 소프트웨어 개발 007: HTML, CSS 및 JavaScript
description: 
published: true
date: 2023-02-10T03:17:47.913Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:17:41.585Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Software Development 007: HTML, CSS and JavaScript***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-007-html-css-and-javascript)
{.links-list}


# 소프트웨어 개발 007: HTML, CSS 및 JavaScript

웹 개발의 기본은 HTML, CSS 및 JavaScript의 세 가지 기술로 구성됩니다. 이 게시물에서는 각 기술의 기본 사항을 다룰 것입니다.

## HTML

HTML(HyperText Markup Language)은 World Wide Web 문서의 표준 마크업 언어입니다. HTML 요소는 HTML 페이지의 빌딩 블록입니다.

### 기본 HTML 구문

HTML 요소는 시작 태그, 내용 및 종료 태그로 구성됩니다. 시작 태그는 꺾쇠 괄호로 묶여 있고 종료 태그도 꺾쇠 괄호로 묶여 있지만 요소 이름 앞에 슬래시가 포함되어 있습니다.

예를 들어 `<p>` 요소는 텍스트 단락을 나타냅니다. `<p>` 시작 태그는 포함된 콘텐츠가 단락임을 웹 브라우저에 알리고 `</p>` 종료 태그는 단락이 종료되었음을 웹 브라우저에 알립니다.

다음은 단락 요소의 예입니다.

```html
<p>This is a paragraph of text.</p>
```

대부분의 HTML 요소에는 요소에 대한 추가 정보를 제공하는 데 사용되는 속성이 있을 수 있습니다. 속성은 시작 태그에 지정되며 일반적으로 등호로 구분된 이름과 값으로 구성됩니다.

예를 들어 하이퍼링크를 나타내는 `<a>` 요소에는 링크가 연결되는 페이지의 URL을 지정하는 `href` 속성이 있습니다.

다음은 하이퍼링크 요소의 예입니다.

```html
<a href="https://www.example.com/">This is a link to an external website.</a>
```

### `<head>` 요소

`<head>` 요소는 문서 제목과 같은 문서에 대한 정보를 포함하며 CSS 스타일시트 및 JavaScript 파일과 같은 외부 리소스를 로드하는 데 사용됩니다.

다음은 `<head>` 요소의 예입니다.

```html
<head>
    <title>This is the document's title</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js"></script>
</head>
```

### `<body>` 요소

`<body>` 요소는 웹 브라우저에 표시되는 문서의 내용을 포함합니다.

다음은 `<body>` 요소의 예입니다.

```html
<body>
    <!-- This is a comment -->
    <h1>This is a heading</h1>
    <p>This is a paragraph of text.</p>
    <ul>
        <li>This is a list item</li>
        <li>This is another list item</li>
    </ul>
</body>
```

## CSS

CSS(Cascading Style Sheets)는 마크업 언어로 작성된 문서의 표현을 설명하는 데 사용되는 스타일 시트 언어입니다. CSS는 문서의 `<body>`, `<head>` 및 `<html>` 요소를 포함하여 모든 HTML 태그의 스타일을 지정하는 데 사용됩니다.

CSS 규칙은 선택자와 선언으로 구성됩니다. 선택기는 CSS 규칙이 적용되는 HTML 요소를 지정하는 데 사용됩니다. 선언은 선택기에 의해 지정된 HTML 요소에 적용되는 CSS 속성 및 값을 지정하는 데 사용됩니다.

CSS 선언은 속성과 값으로 구성되며 콜론으로 구분됩니다. 여러 선언은 세미콜론으로 구분할 수 있습니다.

다음은 CSS 규칙의 예입니다.

```css
p {
    color: red;
    font-size: 16px;
}
```

이 CSS 규칙은 모든 `<p>` 요소를 빨간색으로 만들고 글꼴 크기를 16px로 만듭니다.

CSS 규칙은 HTML 문서의 `<head>` 요소, 별도의 CSS 파일 또는 HTML 요소 내의 인라인에 배치할 수 있습니다.

다음은 인라인 CSS 규칙이 있는 HTML 문서의 예입니다.

```html
<html>
<head>
    <title>This is the document's title</title>
</head>
<body>
    <h1 style="color: red;">This is a heading</h1>
    <p>This is a paragraph of text.</p>
</body>
</html>
```

## 자바스크립트

JavaScript는 웹 페이지를 대화식으로 만드는 데 사용되는 프로그래밍 언어입니다. JavaScript 코드는 HTML 문서의 `<head>` 요소, 별도의 JavaScript 파일 또는 HTML 요소 내의 인라인에 배치할 수 있습니다.

다음은 인라인 JavaScript가 포함된 HTML 문서의 예입니다.

```html
<html>
<head>
    <title>This is the document's title</title>
</head>
<body>
    <button onclick="alert('This is an alert')">Click me!</button>
</body>
</html>
```

이 예에서 버튼을 클릭하면 "This is an alert"라는 텍스트가 있는 경고 상자가 나타납니다.

JavaScript 코드를 사용하여 HTML 문서의 내용과 스타일을 동적으로 변경할 수도 있습니다.

다음은 `<h1>` 요소의 텍스트를 변경하는 JavaScript의 예입니다.

```html
<html>
<head>
    <title>This is the document's title</title>
</head>
<body>
    <h1 id="heading">This is a heading</h1>
    <script>
    document.getElementById("heading").innerHTML = "This is a new heading";
    </script>
</body>
</html>
```

이 예에서 `<h1>` 요소의 텍스트는 페이지가 로드될 때 "This is a heading"에서 "This is a new heading"으로 변경됩니다.

## 추가 정보

- HTML, CSS 및 JavaScript에 대한 자세한 내용은 다음 리소스를 확인하십시오.

    - [W3C의 HTML 사양](https://www.w3.org/TR/html/)
    - [W3C의 CSS 사양](https://www.w3.org/TR/CSS/)
    - [W3C의 JavaScript 사양](https://www.w3.org/TR/javascript/)
    - [Mozilla 개발자 네트워크의 HTML 문서](https://developer.mozilla.org/en-US/docs/Web/HTML)
    - [Mozilla Developer Network의 CSS 문서](https://developer.mozilla.org/en-US/docs/Web/CSS)
    - [Mozilla Developer Network의 JavaScript 설명서](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## 경고

- `<script>` 요소를 사용하여 외부 JavaScript 파일을 로드하지 마십시오. JavaScript 코드를 인라인할 때만 `<script>` 요소를 사용하십시오.

## 위험

- HTML, CSS 또는 JavaScript를 사용하여 외부 파일을 로드하지 마십시오.