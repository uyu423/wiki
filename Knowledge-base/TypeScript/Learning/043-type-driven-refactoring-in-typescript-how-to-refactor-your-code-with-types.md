---
title: 043: TypeScript의 유형 기반 리팩토링: 유형을 사용하여 코드를 리팩토링하는 방법
description: 
published: true
date: 2023-03-06T00:32:53.031Z
tags: 
editor: markdown
dateCreated: 2023-03-06T00:32:45.857Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [043: Type-Driven Refactoring in TypeScript: How to Refactor Your Code with Types***English** document is available*](/en/Knowledge-base/TypeScript/Learning/043-type-driven-refactoring-in-typescript-how-to-refactor-your-code-with-types)
{.links-list}



유형 기반 리팩토링은 TypeScript 코드의 품질을 개선하는 데 도움이 되는 강력한 기술입니다. 유형을 사용하여 리팩토링 노력을 안내함으로써 코드를 보다 강력하고 유지 관리하기 쉽고 오류 발생 가능성을 줄일 수 있습니다.

이 게시물에서는 TypeScript에서 유형 기반 리팩토링의 기본 사항을 살펴보겠습니다. 유형을 사용하여 중복 코드, 긴 함수 및 복잡한 조건과 같은 일반적인 코드 냄새를 식별하고 리팩터링하는 방법을 다룰 것입니다. 또한 유형을 사용하여 코드를 보다 모듈화하고 추론하기 쉽게 만들어 코드 디자인을 개선하는 방법도 살펴봅니다.

## 유형 기반 리팩토링이란 무엇입니까?

형식 기반 리팩토링은 프로그래밍 언어의 형식 시스템을 사용하여 프로세스를 안내하는 리팩토링에 대한 접근 방식입니다. TypeScript에서 이는 코드의 유형 주석을 사용하여 개선이 필요한 영역을 식별하고 리팩토링 노력을 안내하는 것을 의미합니다.

예를 들어 `string` 유형의 인수를 사용하는 함수가 있지만 `any` 유형의 값을 전달하는 경우 TypeScript는 이를 잠재적인 오류로 강조 표시합니다. 이 오류를 수정하면 코드를 더 강력하게 만들고 버그에 덜 취약하게 만들 수 있습니다.

유형 기반 리팩토링은 또한 이해하거나 유지하기 어려운 코드 영역을 식별하는 데 도움이 될 수 있습니다. 함수와 변수의 유형을 살펴봄으로써 그들이 하는 일과 코드베이스에서 어떻게 사용되는지 더 잘 이해할 수 있습니다.

## 중복 코드 리팩토링

가장 일반적인 코드 냄새 중 하나는 중복 코드입니다. 중복 코드는 코드베이스를 유지 관리하기 어렵게 만들 수 있으며, 코드의 한 복사본은 변경되고 다른 복사본은 변경되지 않으면 버그로 이어질 수 있습니다.

유형을 사용하면 유사한 유형 서명이 있는 함수나 메서드를 찾아 중복 코드를 식별할 수 있습니다. 예를 들어 `문자열` 인수를 사용하고 `부울`을 반환하는 두 개의 함수가 있는 경우 일반 유형 매개변수를 사용하는 단일 함수로 리팩터링할 수 있습니다.

```typescript
function startsWithA(str: string): boolean {
  return str.startsWith('a');
}

function endsWithA(str: string): boolean {
  return str.endsWith('a');
}
```

이 예제에는 문자열이 문자 'a'로 시작하는지 또는 끝나는지 확인하는 두 가지 함수가 있습니다. 이러한 함수를 다음과 같이 제네릭 형식 매개 변수를 사용하는 단일 함수로 리팩터링할 수 있습니다.

```typescript
function startsOrEndsWith(str: string, letter: string): boolean {
  if (letter === 'a') {
    return str.startsWith(letter) || str.endsWith(letter);
  }
  return false;
}
```

제네릭 형식 매개 변수를 사용하면 논리를 복제하지 않고 다른 형식의 문자열에 대해 동일한 코드를 재사용할 수 있습니다.

## 긴 함수 리팩토링

또 다른 일반적인 코드 냄새는 긴 함수입니다. 긴 함수는 읽고 이해하기 어려울 수 있으며 코드 동작에 대해 추론하기 어렵게 만들 수 있습니다.

유형을 사용하면 긴 유형 서명이 있거나 많은 인수를 사용하는 함수를 찾아 긴 함수를 식별할 수 있습니다. 예를 들어, 서로 다른 유형의 5개 인수를 사용하는 함수가 있는 경우 각각 더 적은 수의 인수를 사용하는 여러 개의 더 작은 함수로 분할할 수 있습니다.

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
  phone: string;
  email: string;
}

function sendEmailToPerson(
  person: Person,
  subject: string,
  body: string,
  cc?: string[],
  bcc?: string[],
): boolean {
  // Send email logic here
  return true;
}
```

이 예에는 제목, 본문, 선택적 CC 및 BCC 필드가 포함된 전자 메일을 사람에게 보내는 기능이 있습니다. 이 함수를 다음과 같이 여러 개의 작은 함수로 나눌 수 있습니다.

```typescript
function getEmailRecipients(person: Person, cc?: string[], bcc?: string[]): string[] {
  const recipients = [person.email];
  if (cc) {
    recipients.push(...cc);
  }
  if (bcc) {
    recipients.push(...bcc);
  }
  return recipients;
}

function sendEmail(recipients: string[], subject: string, body: string): boolean {
  // Send email logic here
  return true;
}

function sendEmailToPerson(person: Person, subject: string, body: string, cc?: string[], bcc?: string[]): boolean {
  const recipients = getEmailRecipients(person, cc, bcc);
  return sendEmail(recipients, subject, body);
}
```

함수를 더 작은 함수로 분할하면 더 쉽게 이해하고 테스트하고 유지 관리할 수 있습니다.

## 복잡한 조건 리팩토링

복잡한 조건문은 코드 복잡성과 잠재적인 버그의 또 다른 원인이 될 수 있습니다. 분기 또는 중첩된 조건이 많은 조건문은 이해하고 추론하기 어려울 수 있습니다.

유형을 사용하면 길거나 복잡한 유형 서명이 있거나 많은 조건을 사용하는 함수를 찾아 복잡한 조건을 식별할 수 있습니다. 예를 들어 나이, 직책 및 성과 등급을 기준으로 사람이 승진 자격이 있는지 확인하는 기능이 있는 경우 사람의 자격을 나타내는 유형을 사용하여 논리를 단순화할 수 있습니다.

```typescript
interface Person {
  name: string;
  age: number;
  jobTitle: string;
  performanceRating: number;
}

function isEligibleForPromotion(person: Person): boolean {
  if (person.age >= 30 && person.jobTitle === 'Manager' && person.performanceRating >= 4) {
    return true;
  }
  if (person.age >= 25 && person.jobTitle === 'Developer' && person.performanceRating >= 3) {
    return true;
  }
  return false;
}
```

이 예에는 나이, 직책 및 성과 등급에 따라 사람이 승진 자격이 있는지 확인하는 기능이 있습니다. 다음과 같이 사람의 자격을 나타내는 유형을 만들어 이 논리를 단순화할 수 있습니다.

```typescript
interface PromotionEligibility {
  age: number;
  jobTitle: 'Manager' | 'Developer';
  performanceRating: number;
}

function isEligibleForPromotion(person: Person, eligibility: PromotionEligibility): boolean {
  return person.age >= eligibility.age
    && person.jobTitle === eligibility.jobTitle
    && person.performanceRating >= eligibility.performanceRating;
}
```

개인의 자격을 나타내는 별도의 유형을 사용하여 함수의 논리를 단순화하고 이해 및 유지 관리를 더 쉽게 만들 수 있습니다.

## 추가 정보

유형 기반 리팩토링은 TypeScript 코드의 품질을 개선하는 강력한 기술이 될 수 있습니다. 그러나 유형이 모든 코드 품질 문제에 대한 만병통치약은 아니라는 점을 기억하는 것이 중요합니다. 유형에만 기반한 리팩터링이 최선의 접근 방식이 아닐 수 있는 경우가 있을 수 있습니다.

또한 유형 기반 리팩토링은 고급 기술일 수 있으며 TypeScript의 유형 시스템에 어느 정도 익숙해야 할 수 있습니다. TypeScript를 처음 사용하는 경우 유형 기반 리팩토링을 시작하기 전에 몇 가지 기본 사항부터 시작하는 것이 도움이 될 수 있습니다.

## 더 읽을거리

- [TypeScript를 사용한 유형 기반 개발](https://www.pluralsight.com/courses/typescript-type-driven-development) - 유형을 사용하여 TypeScript에서 개발을 안내하는 Pluralsight 과정입니다.
- [Refactoring TypeScript Code with Confidence](https://www.sitepen.com/blog/refactoring-typescript-code-with-confidence/) - TypeScript의 유형 시스템을 사용하여 코드 품질을 개선하는 방법에 대한 블로그 게시물입니다.
- [TypeScript 핸드북 - 유형 추론](https://www.typescriptlang.org/docs/handbook/type-inference.html) - 유형 추론에 대한 공식 TypeScript 핸드북 섹션입니다.