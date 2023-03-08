---
title: 012: JavaScript에서 RxJS를 사용한 반응형 프로그래밍
description: 
published: true
date: 2023-02-17T12:32:50.864Z
tags: 
editor: markdown
dateCreated: 2023-02-17T12:32:49.474Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [012: Reactive programming with RxJS in JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/012-reactive-programming-with-rxjs-in-javascript)
{.links-list}


# JavaScript에서 RxJS를 사용한 반응형 프로그래밍

리액티브 프로그래밍은 데이터 스트림과 변경 전파를 다루는 프로그래밍 패러다임입니다. 이는 비동기 및 이벤트 기반 애플리케이션을 구축하는 데 사용할 수 있습니다.

RxJS는 비동기 데이터 스트림 작업을 쉽게 해주는 관찰 가능 항목을 사용하는 반응형 프로그래밍용 라이브러리입니다.

이번 포스트에서는 자바스크립트에서 RxJS를 이용한 리액티브 프로그래밍에 대해 알아보겠습니다. 다음 주제를 다룰 것입니다.

- 리액티브 프로그래밍이란?
- RxJS란?
- RxJS 설정
- 옵저버블 생성
- 관찰 가능 항목 구독
- 핫 및 콜드 옵저버블
- 과목
- 운영자
- 오류 처리

## 리액티브 프로그래밍이란?

리액티브 프로그래밍은 데이터 스트림과 변경 전파를 다루는 프로그래밍 패러다임입니다.

반응형 프로그래밍에서 데이터는 시간이 지남에 따라 처리할 수 있는 값의 흐름으로 표현됩니다. 이러한 값은 사용자 입력 또는 서버 응답과 같은 소스에서 내보낼 수 있습니다.

값 스트림은 연산자를 사용하여 변환, 결합 및 필터링할 수 있습니다. 스트림의 출력은 구독할 수 있으며 스트림 변경의 값으로 업데이트됩니다.

리액티브 프로그래밍은 비동기 및 이벤트 기반 애플리케이션을 구축하는 데 사용할 수 있습니다.

## RxJS란?

RxJS는 비동기 데이터 스트림 작업을 쉽게 해주는 관찰 가능 항목을 사용하는 반응형 프로그래밍용 라이브러리입니다.

RxJS는 Observer 패턴 구현을 제공합니다. 이 패턴은 데이터 소스를 구독하고 알림을 받는 데 사용됩니다.

RxJS는 또한 값의 스트림을 변환, 결합 및 필터링하는 데 사용할 수 있는 여러 연산자를 제공합니다.

## RxJS 설정

RxJS는 여러 가지 방법으로 사용할 수 있습니다. 스크립트 태그를 사용하여 브라우저에서 사용하거나 require() 함수를 사용하여 Node.js에서 사용할 수 있습니다.

RequireJS, SystemJS 및 Webpack과 같은 다양한 모듈 로더와 함께 사용할 수도 있습니다.

## 관찰 가능 항목 만들기

RxJS 관찰 가능 항목은 배열, 약속 및 이벤트 이미터와 같은 다양한 데이터 소스에서 생성할 수 있습니다.

Observable은 create() 연산자를 사용하여 처음부터 만들 수 있습니다. 이 연산자는 관찰 가능 항목에서 값을 내보내는 데 사용되는 함수를 사용합니다.

```javascript
const observable = Rx.Observable.create(function (observer) {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.complete();
});
```

## 관찰 가능 항목 구독

Observable은 subscribe() 메서드를 사용하여 구독할 수 있습니다. 이 메서드는 다음, 오류 및 완료 이벤트에 대한 처리기를 정의하는 관찰자 개체를 사용합니다.

```javascript
observable.subscribe({
  next: function (value) {
    console.log(value);
  },
  error: function (error) {
    console.log(error);
  },
  complete: function () {
    console.log('complete');
  }
});
```

## 핫 및 콜드 옵저버블

Observable은 뜨겁거나 차가울 수 있습니다.

핫 옵저버블은 생성되자마자 값을 방출하기 시작하는 옵저버블입니다. 콜드 관찰 가능 항목은 구독할 때까지 값 방출을 시작하지 않는 항목입니다.

## 주제

주제는 여러 옵저버에게 멀티캐스트할 수 있는 옵저버블 유형입니다. 이것은 주제가 여러 관찰자에게 값을 브로드캐스트하는 데 사용될 수 있음을 의미합니다.

주제는 주제 클래스를 사용하여 만들 수 있습니다.

```javascript
const subject = new Rx.Subject();
```

주제는 일반 관찰 가능 항목과 동일한 방식으로 구독할 수 있습니다.

```javascript
subject.subscribe({
  next: function (value) {
    console.log(value);
  }
});
```

주제를 사용하여 값을 내보낼 수도 있습니다.

```javascript
subject.next(1);
subject.next(2);
subject.next(3);
```

## 연산자

RxJS는 값 스트림을 변환, 결합 및 필터링하는 데 사용할 수 있는 여러 연산자를 제공합니다.

연산자는 pipe() 메서드를 사용하여 관찰 가능 항목과 함께 사용할 수 있습니다.

```javascript
const observable = Rx.Observable.create(function (observer) {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.complete();
}).pipe(
  map(function (value) {
    return value * 2;
  }),
  filter(function (value) {
    return value > 2;
  })
);
```

## 오류 처리

오류는 catchError() 연산자를 사용하여 처리할 수 있습니다. 이 연산자는 오류를 처리하는 데 사용되는 함수를 사용합니다.

```javascript
const observable = Rx.Observable.create(function (observer) {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  throw new Error('error');
}).pipe(
  catchError(function (error) {
    console.log(error);
  })
);
```

# 추가 정보

이 포스트는 RxJS와 리액티브 프로그래밍이 할 수 있는 일의 겉핥기만 했습니다. 자세한 내용은 아래 리소스를 확인하세요.

## 자원

- [리액티브 프로그래밍](https://en.wikipedia.org/wiki/Reactive_programming)
- [RxJS](https://rxjs-dev.firebaseapp.com/)
- [RxJS 문서](https://rxjs-dev.firebaseapp.com/guide/overview)
- [RxJS API 레퍼런스](https://rxjs-dev.firebaseapp.com/api)
- [리액티브X](http://reactivex.io/)