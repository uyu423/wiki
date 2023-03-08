---
title: TypeScript 및 RxJS로 반응형 애플리케이션 구축
description: 
published: true
date: 2023-02-13T11:18:10.235Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:18:08.595Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Reactive Applications with TypeScript and RxJS***English** document is available*](/en/Knowledge-base/TypeScript/building-reactive-applications-with-typescript-and-rxjs)
{.links-list}


# TypeScript와 RxJS로 반응형 애플리케이션 만들기

리액티브 프로그래밍은 데이터 스트림과 변경 전파를 다루는 프로그래밍 패러다임입니다. 관찰 가능 항목을 사용하여 데이터의 변경 사항을 감지하고 대응하는 비동기 프로그래밍 기술입니다.

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. RxJS는 관찰 가능 패턴의 구현을 제공하는 반응형 프로그래밍용 라이브러리입니다.

이 기사에서는 TypeScript 및 RxJS를 사용하여 반응형 애플리케이션을 빌드하는 방법을 살펴봅니다. 간단한 관찰 가능 항목을 생성하는 것으로 시작한 다음 연산자를 사용하여 관찰 가능 항목을 변환하고 결합하는 방법을 살펴봅니다. 마지막으로 RxJS를 Angular와 함께 사용하여 실제 애플리케이션을 구축하는 방법을 살펴보겠습니다.

## 옵저버블 생성

1에서 10까지의 숫자를 방출하는 간단한 관찰 가능 항목을 만드는 것으로 시작하겠습니다.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
});
```

`create` 연산자는 observable이 구독될 때 실행되는 함수를 사용합니다. 이 함수에는 값을 내보내는 데 사용되는 관찰자 개체가 제공됩니다. 이 예제에서는 `next` 메소드를 사용하여 1부터 10까지의 숫자를 방출합니다. 또한 Observable이 값 방출을 완료했음을 나타내기 위해 `complete` 메소드를 호출합니다.

Observable을 구독하여 값 수신을 시작할 수 있습니다.

```typescript
observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

`subscribe` 메서드는 값이 방출될 때 실행할 함수, 오류가 발생할 때 실행할 함수, Observable이 완료될 때 실행할 함수의 세 가지 인수를 사용합니다.

## 옵저버블 변환

연산자는 관찰 가능 항목을 변환하고 결합하는 데 사용됩니다. RxJS는 다양한 목적을 위해 다양한 연산자를 제공합니다.

### 매핑

매핑 연산자는 관찰 가능 항목에서 내보낸 값을 변환하는 데 사용됩니다.

예를 들어, `map` 연산자를 사용하여 observable이 내보낸 숫자를 문자열로 변환할 수 있습니다.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
}).pipe(
  map((value: number) => value.toString())
);

observable.subscribe(
  (value: string) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

`map` 연산자는 observable이 방출하는 각 값에 적용되는 함수를 사용합니다. 이 예에서는 이 함수를 사용하여 각 숫자를 문자열로 변환합니다.

또한 `map` 연산자를 사용하여 Observable이 내보낸 값을 다른 유형으로 변환할 수 있습니다.

예를 들어, `map` 연산자를 사용하여 observable이 내보낸 문자열을 숫자로 변환할 수 있습니다.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<string>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i.toString());
  }
  observer.complete();
}).pipe(
  map((value: string) => parseInt(value))
);

observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

이 예제에서는 `map` 연산자를 사용하여 observable이 내보낸 문자열을 숫자로 변환합니다.

### 필터링

필터링 연산자는 관찰 가능 항목에서 내보낸 값의 하위 집합을 선택하는 데 사용됩니다.

예를 들어, `filter` 연산자를 사용하여 observable에서 내보낸 짝수만 선택할 수 있습니다.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
}).pipe(
  filter((value: number) => value % 2 === 0)
);

observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

`filter` 연산자는 observable이 내보낸 각 값을 테스트하는 데 사용되는 함수를 사용합니다. 이 예제에서는 이 함수를 사용하여 각 값이 짝수인지 테스트합니다.

### 결합

결합 연산자는 여러 관찰 가능 항목에서 내보낸 값을 결합하는 데 사용됩니다.

예를 들어 `merge` 연산자를 사용하여 두 관찰 가능 항목에서 방출된 값을 결합할 수 있습니다.

```typescript
const observable1 = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
});

const observable2 = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 11; i <= 20; i++) {
    observer.next(i);
  }
  observer.complete();
});

const observable = Rx.Observable.merge(observable1, observable2);

observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

이 예에서는 `merge` 연산자를 사용하여 `observable1` 및 `observable2`에서 내보낸 값을 결합합니다.

## RxJS 및 각도

RxJS는 Angular와 함께 사용하여 반응형 애플리케이션을 구축할 수 있습니다. Angular는 HTTP 요청을 수행하는 데 사용되는 `HttpClient` 서비스를 제공합니다. `HttpClient` 서비스는 observable을 사용하여 HTTP 요청의 결과를 반환하는 observable 기반 API입니다.

`HttpClient` 서비스를 사용하여 GET 요청을 수행하는 방법을 살펴보겠습니다.

```typescript
@Injectable()
export class HttpService {
  constructor(private http: HttpClient) {}

  get(url: string) {
    return this.http.get(url);
  }
}
```

이 예제에서는 `HttpClient` 서비스를 `HttpService`에 삽입하고 `http.get` 메서드를 사용하여 GET 요청을 수행하는 `get` 메서드를 만듭니다.

GET 요청의 결과를 수신하기 위해 `get` 메소드를 구독할 수 있습니다.

```typescript
this.httpService.get('/api/users').subscribe(
  (res: any) => console.log(res),
  (err: any) => console.log(err)
);
```

이 예제에서는 GET 요청의 결과를 수신하기 위해 `get` 메서드를 구독합니다. `subscribe` 메서드는 요청이 성공할 때 실행할 함수와 요청이 실패할 때 실행할 함수의 두 가지 인수를 사용합니다.

연산자를 사용하여 `get` 메서드에서 반환된 관찰 가능 항목을 변환할 수도 있습니다.

예를 들어 `map` 연산자를 사용하여 JSON 응답을 `User` 개체의 배열로 변환할 수 있습니다.

```typescript
this.httpService.get('/api/users').pipe(
  map((res: any) => res.json())
).subscribe(
  (users: User[]) => console.log(users),
  (err: any) => console.log(err)
);
```

이 예에서는 `map` 연산자를 사용하여 JSON 응답을 `User` 개체의 배열로 변환합니다. 그런 다음 Observable을 구독하여 `User` 개체의 배열을 받을 수 있습니다.

## 결론

이 기사에서는 TypeScript 및 RxJS를 사용하여 반응형 애플리케이션을 빌드하는 방법을 살펴보았습니다. Observable을 생성하는 방법과 연산자를 사용하여 Observable을 변환하고 결합하는 방법을 살펴보았습니다. 또한 RxJS를 Angular와 함께 사용하여 실제 애플리케이션을 구축하는 방법도 살펴보았습니다.