---
title: 002: JavaScript의 기능적 구성의 기본 이해
description: 
published: true
date: 2023-02-17T07:32:16.993Z
tags: 
editor: markdown
dateCreated: 2023-02-17T07:32:15.673Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [002: Understanding the basics of functional composition in JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/002-understanding-the-basics-of-functional-composition-in-javascript)
{.links-list}


기능적 구성은 보다 간결하고 유지 관리 가능한 코드를 작성하는 데 도움이 되는 강력한 기술입니다. 이 게시물에서는 기능적 구성이 무엇인지, JavaScript 코드에서 어떻게 사용할 수 있는지 살펴보겠습니다.

기능 합성은 두 개 이상의 기능을 결합하여 새로운 기능을 만드는 방법입니다. 결과 함수는 입력 함수의 합성입니다. 이것은 각 함수가 이전 함수의 결과에서 호출되는 함수 연결과 다릅니다.

구성은 함수형 프로그래밍의 기본 원칙입니다. 간단한 기능을 결합하여 복잡한 기능을 구축할 수 있습니다. 컴포지션은 종종 고차 함수를 만드는 데 사용됩니다.

구성이 어떻게 작동하는지 이해하기 위해 간단한 예를 살펴보겠습니다. 문자열을 대문자로 변환하는 함수가 있다고 가정해 보겠습니다.

```javascript
function toUpperCase(str) {
  return str.toUpperCase();
}
```

이 함수를 사용하여 문자열을 소문자로 변환하는 새 함수를 만들 수 있습니다.

```javascript
function toLowerCase(str) {
  return str.toLowerCase();
}
```

이제 반대 작업을 수행하는 두 가지 기능이 있습니다. 구성을 사용하여 문자열을 제목 케이스로 변환하는 새 함수를 만들 수 있습니다.

```javascript
function toTitleCase(str) {
  return toUpperCase(toLowerCase(str));
}
```

이 예제에서는 구성을 사용하여 두 개의 기존 함수를 결합하여 새 함수를 만들었습니다. 결과 함수는 입력 함수의 합성입니다.

구성은 보다 간결하고 유지 관리 가능한 코드를 작성하는 데 도움이 되는 강력한 기술입니다. 이번 포스트에서는 함수형 구성이 무엇인지, JavaScript 코드에서 어떻게 사용할 수 있는지 살펴보았습니다.