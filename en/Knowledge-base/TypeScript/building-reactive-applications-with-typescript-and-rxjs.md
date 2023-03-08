---
title: Building Reactive Applications with TypeScript and RxJS
description: 
published: true
date: 2023-02-13T11:18:15.567Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:18:08.599Z
---

- [Creación de aplicaciones reactivas con TypeScript y RxJS***Spanish** document is available*](/es/Knowledge-base/TypeScript/building-reactive-applications-with-typescript-and-rxjs)
{.links-list}
- [使用 TypeScript 和 RxJS 构建响应式应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/building-reactive-applications-with-typescript-and-rxjs)
{.links-list}
- [TypeScript 및 RxJS로 반응형 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-reactive-applications-with-typescript-and-rxjs)
{.links-list}


# Building Reactive Applications with TypeScript and RxJS

Reactive programming is a programming paradigm that deals with data streams and the propagation of change. It is an asynchronous programming technique that uses observables to detect and react to changes in data.

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. RxJS is a library for reactive programming that provides an implementation of the observables pattern.

In this article, we will see how to use TypeScript and RxJS to build reactive applications. We will start by creating a simple observable and then see how to use operators to transform and combine observables. Finally, we will see how to use RxJS with Angular to build a real-world application.

## Creating an observable

Let's start by creating a simple observable that emits the numbers 1 to 10.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
});
```

The `create` operator takes a function that is executed when the observable is subscribed to. This function is given an observer object that is used to emit values. In this example, we use the `next` method to emit the numbers 1 to 10. We also call the `complete` method to indicate that the observable has finished emitting values.

We can subscribe to the observable to start receiving values.

```typescript
observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

The `subscribe` method takes three arguments: a function to execute when a value is emitted, a function to execute when an error is thrown, and a function to execute when the observable completes.

## Transforming observables

Operators are used to transform and combine observables. RxJS provides a wide variety of operators for different purposes.

### Mapping

Mapping operators are used to transform the values emitted by an observable.

For example, we can use the `map` operator to transform the numbers emitted by our observable into strings.

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

The `map` operator takes a function that is applied to each value emitted by the observable. In this example, we use this function to transform each number into a string.

We can also use the `map` operator to transform the values emitted by an observable into a different type.

For example, we can use the `map` operator to transform the strings emitted by our observable into numbers.

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

In this example, we use the `map` operator to transform the strings emitted by our observable into numbers.

### Filtering

Filtering operators are used to select a subset of values emitted by an observable.

For example, we can use the `filter` operator to select only the even numbers emitted by our observable.

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

The `filter` operator takes a function that is used to test each value emitted by the observable. In this example, we use this function to test if each value is an even number.

### Combining

Combining operators are used to combine the values emitted by multiple observables.

For example, we can use the `merge` operator to combine the values emitted by two observables.

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

In this example, we use the `merge` operator to combine the values emitted by `observable1` and `observable2`.

## RxJS and Angular

RxJS can be used with Angular to build reactive applications. Angular provides a `HttpClient` service that is used to perform HTTP requests. The `HttpClient` service is an observable-based API that uses observables to return the results of HTTP requests.

Let's see how to use the `HttpClient` service to perform a GET request.

```typescript
@Injectable()
export class HttpService {
  constructor(private http: HttpClient) {}

  get(url: string) {
    return this.http.get(url);
  }
}
```

In this example, we inject the `HttpClient` service into our `HttpService` and create a `get` method that uses the `http.get` method to perform a GET request.

We can subscribe to the `get` method to receive the results of the GET request.

```typescript
this.httpService.get('/api/users').subscribe(
  (res: any) => console.log(res),
  (err: any) => console.log(err)
);
```

In this example, we subscribe to the `get` method to receive the results of the GET request. The `subscribe` method takes two arguments: a function to execute when the request succeeds, and a function to execute when the request fails.

We can also use operators to transform the observable returned by the `get` method.

For example, we can use the `map` operator to transform the JSON response into an array of `User` objects.

```typescript
this.httpService.get('/api/users').pipe(
  map((res: any) => res.json())
).subscribe(
  (users: User[]) => console.log(users),
  (err: any) => console.log(err)
);
```

In this example, we use the `map` operator to transform the JSON response into an array of `User` objects. We can then subscribe to the observable to receive the array of `User` objects.

##Conclusion

In this article, we have seen how to use TypeScript and RxJS to build reactive applications. We have seen how to create observables and how to use operators to transform and combine observables. We have also seen how to use RxJS with Angular to build a real-world application.