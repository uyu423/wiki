---
title: React.js 시작하기
description: 
published: true
date: 2023-01-29T19:51:20.080Z
tags: 
editor: markdown
dateCreated: 2023-01-29T19:51:20.080Z
---


React는 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리입니다. 코드를 쉽게 읽고 유지 관리할 수 있도록 재사용 가능한 구성 요소를 만들 수 있습니다. React를 시작할 때 가장 먼저 해야 할 일은 개발 환경을 설정하는 것입니다.

다음 두 가지 방법이 있습니다.

가장 빠른 방법은 create-react-app으로 새로운 React 앱을 만드는 것입니다. 이렇게 하면 시작하는 데 필요한 모든 종속성이 있는 기본 React 개발 환경이 제공됩니다.

자신만의 환경을 설정하는 데 더 관심이 있다면 그렇게 할 수도 있습니다. React 및 ReactDOM은 물론 Babel과 같은 JavaScript 트랜스파일러를 설치해야 합니다. 그런 다음 index.jsx라는 파일을 만들고 다음 코드를 넣을 수 있습니다.

ReactDOM.render(
  <h1>안녕하세요!</h1>,
  document.getElementById('루트')
);

이제 브라우저에서 index.html을 열 수 있으며 "Hello, world!"가 표시되어야 합니다.

이제 기본 React 개발 환경을 설정했습니다. 여기에서 React 학습을 시작하고 자신만의 애플리케이션을 구축할 수 있습니다.