---
title: CSS 그리드와 Flexbox로 반응형 웹사이트를 구축하는 방법
description: 
published: true
date: 2023-02-24T13:33:06.677Z
tags: 
editor: markdown
dateCreated: 2023-02-24T13:32:59.858Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Responsive Website with CSS Grid and Flexbox***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-responsive-website-with-css-grid-and-flexbox)
{.links-list}


# CSS 그리드와 Flexbox로 반응형 웹사이트를 구축하는 방법

모바일 장치가 널리 보급됨에 따라 모든 화면 크기에서 최적의 시청 경험을 제공하도록 웹 사이트를 설계하는 것이 중요합니다. CSS Grid와 Flexbox는 반응형 웹 사이트를 만드는 데 사용할 수 있는 두 가지 기술입니다.

CSS Grid는 웹 페이지에서 열과 행으로 요소를 배치할 수 있는 2차원 레이아웃 시스템입니다. Flexbox는 단일 행 또는 열에 요소를 배치하는 데 사용할 수 있는 1차원 레이아웃 시스템입니다.

이 기사에서는 CSS Grid 및 Flexbox를 사용하여 반응형 웹 사이트를 만드는 방법을 보여줍니다. 또한 미디어 쿼리를 사용하여 웹사이트의 응답성을 더욱 높일 수 있는 몇 가지 팁을 제공합니다.

## CSS 그리드 사용

CSS Grid는 반응형 웹 사이트를 만들기 위한 강력한 도구입니다. CSS 그리드를 사용하려면 그리드 레이아웃을 정의해야 합니다. 이것은 CSS ```display``` 속성을 사용하여 수행할 수 있습니다.

```css
.container {
  display: grid;
}
```

그리드 레이아웃을 정의하고 나면 여기에 요소를 추가할 수 있습니다. 그리드에 요소를 추가하려면 ```grid-column``` 및 ```grid-row``` 속성을 지정해야 합니다.

```css
.container {
  display: grid;
}

.item {
  grid-column: 1;
  grid-row: 1;
}
```

```css
.container {
  display: grid;
  grid-template-columns: 200px 200px;
  grid-template-rows: 200px 200px;
}

.item {
  grid-column: 1;
  grid-row: 1;
}
```css
.컨테이너 {
  디스플레이: 그리드;
  그리드-템플릿-열: 200px 200px;
  그리드 템플릿 행: 200px 200px;
}

.안건 {
  그리드 열: 1;
  그리드 행: 1;
}
```css
.container {
  display: flex;
}
```display``` 속성을 사용하여 수행할 수 있습니다.

```css
.container {
  display: flex;
}

.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 200px;
}
```

플렉스 컨테이너를 정의하고 나면 여기에 요소를 추가할 수 있습니다. 플렉스 컨테이너에 요소를 추가하려면 ```flex-grow```, ```flex-shrink``` 및 ```flex-basis``` 속성을 지정해야 합니다.

```css
.container {
  display: flex;
  flex-direction: column;
}

.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 200px;
}
```

```css
@media (max-width: 768px) {
  .container {
    display: flex;
    flex-direction: column;
  }

  .item {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 200px;
  }
}
```css
.컨테이너 {
  디스플레이: 플렉스;
  플렉스 방향: 열;
}

.안건 {
  플렉스 성장: 1;
  플렉스-수축: 1;
  플렉스 기준: 200px;
}
```css
@media (orientation: landscape) {
  .container {
    display: grid;
    grid-template-columns: 200px 200px;
    grid-template-rows: 200px 200px;
  }

  .item {
    grid-column: 1;
    grid-row: 1;
  }
}
```css
@media (최대 너비: 768px) {
  .컨테이너 {
    디스플레이: 플렉스;
    플렉스 방향: 열;
  }

  .안건 {
    플렉스 성장: 1;
    플렉스-수축: 1;
    플렉스 기준: 200px;
  }
}
```

미디어 쿼리를 사용하여 장치 방향에 따라 웹 사이트에 적용되는 CSS 규칙을 변경할 수도 있습니다. 예를 들어 미디어 쿼리를 사용하여 가로 모드로 유지되는 태블릿에서 웹 사이트의 레이아웃을 변경할 수 있습니다.

```css
@media (방향: 가로) {
  .컨테이너 {
    디스플레이: 그리드;
    그리드-템플릿-열: 200px 200px;
    그리드 템플릿 행: 200px 200px;
  }

  .안건 {
    그리드 열: 1;
    그리드 행: 1;
  }
}
```

미디어 쿼리 사용에 대해 자세히 알아보려면 [A Beginner's Guide to Responsive Web Design](https://www.sitepoint.com/beginners-guide-responsive-web-design/) 문서를 읽어보는 것이 좋습니다.

## 결론

이 기사에서는 CSS Grid 및 Flexbox를 사용하여 반응형 웹 사이트를 만드는 방법을 설명했습니다. 또한 미디어 쿼리를 사용하여 웹사이트의 반응성을 더욱 높일 수 있는 몇 가지 팁을 제공했습니다.

반응형 웹 디자인에 대해 자세히 알아보려면 [반응형 웹 디자인 기초](https://developers.google.com/web/fundamentals/design-and-ux/responsive/) 문서를 읽어 보시기 바랍니다.