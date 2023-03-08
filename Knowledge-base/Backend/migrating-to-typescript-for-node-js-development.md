---
title: Node.js 개발을 위해 TypeScript로 마이그레이션
description: 
published: true
date: 2023-02-17T18:01:00.738Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:25:08.834Z
---

- [Migrating to TypeScript for Node.js Development***English** version of this document is available*](/en/Knowledge-base/Backend/migrating-to-typescript-for-node-js-development)
{.links-list}


# Node.js 개발을 위해 TypeScript로 마이그레이션

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 컴파일 타임에 코드를 유형 검사하여 코드에 안전 수준을 추가합니다. 이렇게 하면 버그를 조기에 발견하고 장기적으로 코드를 더 유지 관리할 수 있습니다.

TypeScript를 사용하면 많은 이점이 있지만 이 기사에서는 세 가지 주요 이점에 중점을 둘 것입니다.

1. TypeScript를 사용하면 버그를 조기에 발견할 수 있습니다.
2. TypeScript는 코드를 더 유지하기 쉽게 만들 수 있습니다.
3. TypeScript는 개발 워크플로를 개선할 수 있습니다.

## TypeScript는 버그를 조기에 발견하도록 도와줍니다.

TypeScript의 이점 중 하나는 버그를 조기에 발견할 수 있다는 것입니다. 컴파일 타임에 코드를 유형 검사함으로써 TypeScript는 다른 방법으로는 찾기 어려운 버그를 찾는 데 도움을 줄 수 있습니다.

예를 들어 다음 코드를 고려하십시오.

```javascript
function add(a, b) {
    return a + b;
}

add(1, 2); // returns 3
add("1", "2"); // returns "12"
```

위의 'add' 함수는 두 개의 숫자를 더하는 간단한 함수입니다. 그러나 JavaScript의 느슨한 타이핑으로 인해 `add` 함수를 사용하여 두 개의 문자열을 추가할 수도 있습니다. 이것은 위의 `add`에 대한 두 번째 호출에서와 같이 예기치 않은 결과로 이어질 수 있습니다.

TypeScript를 사용하면 `add` 함수에 유형을 추가하여 이러한 유형의 버그를 잡을 수 있습니다.

```typescript
function add(a: number, b: number) {
    return a + b;
}

add(1, 2); // returns 3
add("1", "2"); // compile-time error!
```

이제 두 개의 문자열로 `add` 함수를 호출하려고 하면 컴파일 타임 오류가 발생합니다. 이렇게 하면 버그가 생산에 들어가기 전에 버그를 조기에 발견할 수 있습니다.

## TypeScript는 코드를 유지보수하기 쉽게 만들 수 있습니다.

TypeScript의 또 다른 이점은 코드를 유지 관리하기 쉽게 만들 수 있다는 것입니다. 코드에 유형을 추가하면 코드를 이해하기 쉽고 변경하기 쉽게 만들 수 있습니다.

예를 들어 다음 코드를 고려하십시오.

```javascript
function getUser(id) {
    // ...
}

getUser(1);
getUser("1"); // oops!
```

위의 `getUser` 함수는 사용자 ID를 취해야 하지만 JavaScript의 느슨한 타이핑으로 인해 문자열을 취할 수도 있습니다. 이는 위의 `getUser`에 대한 두 번째 호출에서와 같이 예기치 않은 결과로 이어질 수 있습니다.

TypeScript를 사용하면 의도를 명확하게 하기 위해 `getUser` 함수에 유형을 추가할 수 있습니다.

```typescript
function getUser(id: number) {
    // ...
}

getUser(1);
getUser("1"); // compile-time error!
```

이제 `getUser` 함수가 숫자를 예상하고 문자열을 전달하려고 하면 컴파일 타임 오류가 발생한다는 것이 분명합니다. 이렇게 하면 코드를 보다 유지 관리하기 쉽게 만들고 버그를 방지할 수 있습니다.

## TypeScript는 개발 워크플로를 개선할 수 있습니다.

마지막으로 TypeScript는 개발 워크플로를 개선할 수 있습니다. TypeScript를 사용하면 JavaScript의 유연성을 희생하지 않고도 유형 검사의 이점을 얻을 수 있습니다.

예를 들어 Babel 및 webpack과 같은 도구와 함께 TypeScript를 사용하여 코드를 JavaScript로 변환하고 TypeScript를 React 및 Angular와 같은 도구와 함께 사용하여 프런트 엔드 애플리케이션을 구축할 수 있습니다.

또한 Node.js 런타임과 함께 TypeScript를 사용하여 서버 측 코드를 작성할 수 있습니다. 그리고 TypeScript 컴파일러와 함께 TypeScript를 사용하여 코드의 유형을 확인할 수 있습니다.

전반적으로 TypeScript는 더 나은 코드를 작성하고 개발 워크플로를 개선하는 데 도움이 될 수 있습니다. TypeScript를 사용하지 않는 경우 시도해 볼 것을 권장합니다.