---
title: 013: 기능적 JavaScript에서 오류 처리 전략 구현
description: 
published: true
date: 2023-02-17T13:06:34.834Z
tags: 
editor: markdown
dateCreated: 2023-02-17T13:06:28.153Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [013: Implementing error handling strategies in functional JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/013-implementing-error-handling-strategies-in-functional-javascript)
{.links-list}


## 기능적 JavaScript에서 오류 처리 전략 구현

함수형 프로그래밍은 함수의 평가를 강조하는 프로그래밍 패러다임입니다. 보다 간결하고 유지 관리 가능한 코드를 작성하는 데 자주 사용되는 선언적 프로그래밍 스타일입니다.

함수형 프로그래밍의 이점 중 하나는 추론하고 디버깅하기 쉬운 코드를 작성하는 데 도움이 된다는 것입니다. 이 게시물에서는 기능적 JavaScript에서 오류 처리를 구현하기 위한 몇 가지 전략을 살펴보겠습니다.

### 시도/잡기

우리가 살펴볼 첫 번째 전략은 `try/catch` 문을 사용하는 것입니다. `try/catch` 문을 사용하면 코드에서 발생하는 오류를 잡을 수 있습니다.

예를 들어, 두 숫자를 나누는 함수가 있다고 합시다. 제수로 `0`을 전달하면 오류가 발생합니다.

우리는 `try/catch` 문을 사용하여 이 오류를 포착하고 정상적으로 처리할 수 있습니다.

```javascript
function divide(x, y) {
    try {
        return x / y;
    } catch (e) {
        console.log("Error: Cannot divide by zero.");
    }
}
```

위의 코드에서는 `x`를 `y`로 나누려고 할 때 발생하는 모든 오류를 잡기 위해 `try/catch` 문을 사용하고 있습니다. 오류가 발생하면 콘솔에 메시지를 출력합니다.

### 일찍 귀가

오류를 처리하는 또 다른 전략은 오류가 발생할 때 함수에서 일찍 반환하는 것입니다. 이것은 `throw` 키워드를 사용하여 수행할 수 있습니다.

예를 들어 주어진 숫자가 양수인지 확인하는 함수가 있다고 가정해 보겠습니다. 숫자가 양수가 아닌 경우 오류를 '던지고' 싶습니다.

```javascript
function checkPositive(x) {
    if (x <= 0) {
        throw "Error: x must be positive.";
    }
    // ...
}
```

위의 코드에서 `x`가 양수가 아닌 경우 `throw` 키워드를 사용하여 오류를 발생시킵니다.

### 옵셔널 체이닝 사용

오류를 처리하는 또 다른 전략은 선택적 연결을 사용하는 것입니다. 옵셔널 체이닝은 객체가 먼저 존재하는지 확인하지 않고 객체의 속성에 접근할 수 있게 해주는 JavaScript의 기능입니다.

예를 들어 사용자에 대한 정보가 포함된 개체가 있다고 가정해 보겠습니다.

```javascript
const user = {
    id: 1,
    name: "John"
};
```

`user` 개체의 `age` 속성에 액세스하려고 하면 `age` 속성이 존재하지 않기 때문에 오류가 발생합니다.

```javascript
console.log(user.age); // Error: age does not exist
```

선택적 연결을 사용하여 `age` 속성에 안전하게 액세스할 수 있습니다.

```javascript
console.log(user?.age); // undefined
```

위의 코드에서 `age` 속성에 액세스하기 위해 선택적 연결을 사용하고 있습니다. `age` 속성이 존재하지 않으면 오류 대신 `undefined`가 표시됩니다.

### 결론

이 게시물에서는 기능적 JavaScript에서 오류 처리를 구현하기 위한 몇 가지 전략을 살펴보았습니다. 우리는 `try/catch` 문을 사용하는 방법, 오류가 발생했을 때 함수에서 조기에 반환하는 방법 및 선택적 연결을 사용하는 방법을 살펴보았습니다.

사용하는 전략은 특정 요구 사항에 따라 다릅니다. 그러나 이러한 모든 전략을 사용하여 보다 강력하고 유지 관리 가능한 코드를 작성할 수 있습니다.