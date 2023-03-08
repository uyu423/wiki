---
title: 012: Reactive programming with RxJS in JavaScript
description: 
published: true
date: 2023-02-17T12:32:56.177Z
tags: 
editor: markdown
dateCreated: 2023-02-17T12:32:49.478Z
---

- [012: JavaScript에서 RxJS를 사용한 반응형 프로그래밍***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/012-reactive-programming-with-rxjs-in-javascript)
{.links-list}


# Reactive programming with RxJS in JavaScript

Reactive programming is a programming paradigm that deals with data streams and the propagation of change. This can be used to build asynchronous and event-based applications.

RxJS is a library for reactive programming using observables that makes it easy to work with asynchronous data streams.

In this post, we will learn about reactive programming with RxJS in JavaScript. We will cover the following topics:

- What is reactive programming?
- What is RxJS?
- Setting up RxJS
- Creating observables
- Subscribing to observables
- Hot and cold observables
- Subjects
- Operators
- Error handling

## What is reactive programming?

Reactive programming is a programming paradigm that deals with data streams and the propagation of change.

In reactive programming, data is represented as a stream of values that can be processed over time. These values can be emitted by a source, such as a user input or a server response.

The stream of values can be transformed, combined, and filtered using operators. The output of the stream can be subscribed to and will be updated as the values in the stream change.

Reactive programming can be used to build asynchronous and event-based applications.

## What is RxJS?

RxJS is a library for reactive programming using observables that makes it easy to work with asynchronous data streams.

RxJS provides an implementation of the Observer pattern. This pattern is used to subscribe to and receive notifications from a data source.

RxJS also provides a number of operators that can be used to transform, combine, and filter streams of values.

## Setting up RxJS

RxJS can be used in a number of ways. It can be used in the browser using a script tag, or it can be used in Node.js using the require() function.

It can also be used with a number of different module loaders, such as RequireJS, SystemJS, and Webpack.

## Creating observables

RxJS observables can be created from a variety of data sources, such as arrays, Promises, and event emitters.

Observables can be created from scratch using the create() operator. This operator takes a function that is used to emit values from the observable.

```javascript
const observable = Rx.Observable.create(function (observer) {
  observer.next(1);
  observer.next(2);
  observer.next(3);
  observer.complete();
});
```

## Subscribing to observables

Observables can be subscribed to using the subscribe() method. This method takes an observer object that defines the handlers for the next, error, and complete events.

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

## Hot and cold observables

Observables can be either hot or cold.

Hot observables are those that begin emitting values as soon as they are created. Cold observables are those that do not begin emitting values until they are subscribed to.

## Subjects

Subjects are a type of observable that can multicast to multiple observers. This means that a subject can be used to broadcast values to multiple observers.

Subjects can be created using the Subject class.

```javascript
const subject = new Rx.Subject();
```

Subjects can be subscribed to in the same way as regular observables.

```javascript
subject.subscribe({
  next: function (value) {
    console.log(value);
  }
});
```

Subjects can also be used to emit values.

```javascript
subject.next(1);
subject.next(2);
subject.next(3);
```

## Operators

RxJS provides a number of operators that can be used to transform, combine, and filter streams of values.

Operators can be used with observables using the pipe() method.

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

## Error handling

Errors can be handled using the catchError() operator. This operator takes a function that is used to handle errors.

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

# Additional Information

This post only scratched the surface of what RxJS and reactive programming can do. For more information, check out the resources below.

## Resources

- [Reactive programming](https://en.wikipedia.org/wiki/Reactive_programming)
- [RxJS](https://rxjs-dev.firebaseapp.com/)
- [RxJS Documentation](https://rxjs-dev.firebaseapp.com/guide/overview)
- [RxJS API Reference](https://rxjs-dev.firebaseapp.com/api)
- [ReactiveX](http://reactivex.io/)