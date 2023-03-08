---
title: 使用 TypeScript 和 RxJS 构建响应式应用程序
description: 
published: true
date: 2023-02-13T11:18:10.296Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:18:08.595Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building Reactive Applications with TypeScript and RxJS***English** document is available*](/en/Knowledge-base/TypeScript/building-reactive-applications-with-typescript-and-rxjs)
{.links-list}


# 使用 TypeScript 和 RxJS 构建响应式应用程序

反应式编程是一种处理数据流和变化传播的编程范式。它是一种异步编程技术，使用可观察对象来检测数据变化并对其做出反应。

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。 RxJS 是一个用于响应式编程的库，它提供了可观察模式的实现。

在本文中，我们将看到如何使用 TypeScript 和 RxJS 构建响应式应用程序。我们将从创建一个简单的可观察对象开始，然后了解如何使用运算符来转换和组合可观察对象。最后，我们将看到如何将 RxJS 与 Angular 一起使用来构建真实世界的应用程序。

## 创建一个可观察对象

让我们从创建一个简单的可观察对象开始，它发出数字 1 到 10。

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
});
```

`create` 运算符接受一个函数，该函数在订阅可观察对象时执行。该函数被赋予一个用于发出值的观察者对象。在此示例中，我们使用 `next` 方法发出数字 1 到 10。我们还调用 `complete` 方法来指示可观察对象已完成发出值。

我们可以订阅可观察对象以开始接收值。

```typescript
observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

`subscribe` 方法接受三个参数：一个在发出值时执行的函数，一个在抛出错误时执行的函数，以及一个在可观察对象完成时执行的函数。

## 转换可观察对象

运算符用于转换和组合可观察量。 RxJS 为不同的目的提供了各种各样的运算符。

### 映射

映射运算符用于转换可观察对象发出的值。

例如，我们可以使用 `map` 运算符将我们的 observable 发出的数字转换为字符串。

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

`map` 运算符采用一个函数，该函数应用于可观察对象发出的每个值。在此示例中，我们使用此函数将每个数字转换为字符串。

我们还可以使用 `map` 运算符将 observable 发出的值转换为不同的类型。

例如，我们可以使用 `map` 运算符将我们的 observable 发出的字符串转换为数字。

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

在此示例中，我们使用 `map` 运算符将我们的可观察对象发出的字符串转换为数字。

### 过滤

过滤运算符用于选择可观察对象发出的值的子集。

例如，我们可以使用 `filter` 运算符只选择我们的 observable 发出的偶数。

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

`filter` 运算符采用一个函数，该函数用于测试可观察对象发出的每个值。在本例中，我们使用此函数来测试每个值是否为偶数。

### 合并

组合运算符用于组合多个可观察对象发出的值。

例如，我们可以使用 `merge` 操作符来组合两个 observable 发出的值。

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

在此示例中，我们使用 merge 运算符组合 observable1 和 observable2 发出的值。

## RxJS 和 Angular

RxJS 可以与 Angular 一起使用来构建响应式应用程序。 Angular 提供了一个用于执行 HTTP 请求的 HttpClient 服务。 `HttpClient` 服务是一种基于可观察对象的 API，它使用可观察对象返回 HTTP 请求的结果。

让我们看看如何使用 `HttpClient` 服务来执行 GET 请求。

```typescript
@Injectable()
export class HttpService {
  constructor(private http: HttpClient) {}

  get(url: string) {
    return this.http.get(url);
  }
}
```

在此示例中，我们将 `HttpClient` 服务注入到我们的 `HttpService` 中，并创建一个 `get` 方法，该方法使用 `http.get` 方法来执行 GET 请求。

我们可以订阅 `get` 方法来接收 GET 请求的结果。

```typescript
this.httpService.get('/api/users').subscribe(
  (res: any) => console.log(res),
  (err: any) => console.log(err)
);
```

在这个例子中，我们订阅了 `get` 方法来接收 GET 请求的结果。 `subscribe` 方法有两个参数：请求成功时执行的函数和请求失败时执行的函数。

我们还可以使用运算符来转换 get 方法返回的可观察对象。

例如，我们可以使用 `map` 运算符将 JSON 响应转换为 `User` 对象数组。

```typescript
this.httpService.get('/api/users').pipe(
  map((res: any) => res.json())
).subscribe(
  (users: User[]) => console.log(users),
  (err: any) => console.log(err)
);
```

在此示例中，我们使用 `map` 运算符将 JSON 响应转换为 `User` 对象数组。然后我们可以订阅可观察对象以接收 User 对象数组。

## 结论

在本文中，我们了解了如何使用 TypeScript 和 RxJS 构建响应式应用程序。我们已经了解了如何创建可观察对象以及如何使用运算符来转换和组合可观察对象。我们还看到了如何将 RxJS 与 Angular 结合使用来构建真实世界的应用程序。