---
title: 이벤트 루프 (Event Loop)
description: 
published: true
date: 2022-12-26T13:10:10.275Z
tags: nodejs, v8
editor: markdown
dateCreated: 2022-12-26T12:35:42.101Z
---

- [Event Loop***English** version of this document is available*](/en/dev/Nodejs/event-loop)
{.links-list}

> 이 문서는 번역 예정입니다.
{.is-danger}

## 개요

Node.js 이벤트 루프는 Node.js가 비차단(Non-Blocking) I/O 작업을 효율적으로 수행할 수 있도록 하는 런타임의 기본 부분입니다. 이벤트 대기열을 지속적으로 모니터링하고 처리할 준비가 된 이벤트를 실행하는 방식으로 작동합니다.

- 이벤트 루프는 싱글 스레드 이벤트 루프입니다. 즉, 한 번에 하나의 이벤트만 처리할 수 있으며 이벤트는 순서대로 처리됩니다. 그러나 Node.js는 CPU를 많이 사용하는 작업을 수행하거나 시스템 호출을 차단하는 것과 같은 특정 유형의 작업에 여러 스레드를 사용할 수도 있습니다.
- 이벤트 루프는 Node.js 애플리케이션에서 실행되는 대부분의 JavaScript 코드 실행을 담당합니다. 여기에는 사용자 코드와 Node.js 런타임 및 해당 표준 라이브러리에서 제공하는 코드가 모두 포함됩니다.
- 이벤트 루프는 비차단형으로 설계되어 각 이벤트가 완료될 때까지 기다리지 않고 다음 이벤트로 넘어갈 때까지 이벤트를 동시에 처리할 수 있습니다. 이는 비차단 I/O 작업 및 비동기 콜백 함수를 사용하여 달성됩니다.
- 이벤트 루프는 JavaScript와 네이티브 코드의 조합을 사용하여 구현됩니다. 이벤트 루프의 JavaScript 부분은 C++로 작성되어 V8 JavaScript 엔진을 사용, 네이티브 코드로 컴파일되는 반면 네이티브 부분은 플랫폼별 API를 사용하여 구현됩니다.
- 이벤트 루프에는 여러 단계가 있으며 각 단계는 특정 유형의 이벤트 처리를 담당합니다. 단계가 실행되는 순서는 사용 중인 Node.js의 특정 버전에 따라 다를 수 있습니다.

> ### Non-Blocking I/O 작업에 대하여
>
> Node.js에서 비차단 I/O 작업은 작업이 완료되기를 기다리는 동안 프로그램 실행을 차단하지 않는 작업입니다. 이는 I/O 작업이 백그라운드에서 수행되는 동안 프로그램이 계속 실행되고 다른 작업을 수행할 수 있음을 의미합니다.
>
> Node.js는 서버 측에서 JavaScript를 실행하도록 설계된 Chrome V8 JavaScript 엔진 위에 구축됩니다. Node.js의 주요 기능 중 하나는 비차단 I/O를 사용하여 많은 동시 연결을 효율적으로 처리하고 작업을 비동기식(asynchronously)으로 수행할 수 있다는 것입니다.

> ### V8 JsavaScript 엔진에 대하여
>
> Node.js는 Google에서 개발 및 유지 관리하는 V8 JavaScript 엔진 위에 구축됩니다. V8은 JavaScript 코드를 빠르고 효율적으로 실행하도록 설계된 고성능 오픈 소스 JavaScript 엔진입니다. C++로 작성되었으며 Google Chrome 웹 브라우저 및 기타 여러 프로젝트에 전원을 공급하는 데 사용됩니다.
>
> V8은 ECMAScript 버전 6 이상으로 작성된 코드를 포함하여 최신 JavaScript 코드를 실행하도록 설계되었습니다. 여기에는 클래스, 화살표 함수 및 Promise 지원과 같은 기능과 JIT(Just-In-Time) 컴파일이 포함되어 런타임에 코드를 네이티브 머신 코드로 컴파일하여 코드를 더 빠르게 실행할 수 있습니다.
>
> V8은 Node.js 애플리케이션에서 실행되는 JavaScript 코드 실행을 담당하므로 Node.js 런타임의 중요한 구성 요소입니다. 이는 Node.js 런타임과 긴밀하게 통합되며 Node.js를 확장 가능한 네트워크 애플리케이션 구축에 적합하게 만드는 많은 기능을 제공합니다.
>
> 다음은 V8 엔진의 작동 방식을 간략하게 나타낸 것입니다.
>
> 1. V8 엔진은 JavaScript 코드를 입력으로 받습니다.
> 1. 코드가 구문 분석되고 V8 엔진이 이해하기 쉬운 중간 표현(IR)으로 변환됩니다.
> 1. IR은 Constant Folding, Inlining 등 다양한 최적화 기법을 적용하여 빠른 실행이 가능하도록 최적화되어 있습니다.
> 1. 최적화된 IR은 JIT 컴파일러를 사용하여 원시 기계 코드로 컴파일됩니다.
> 1. 네이티브 머신 코드는 CPU에 의해 실행됩니다.

> ### Appendix: About Non-Blocking I/O Operation
> 
> In Node.js, a non-blocking I/O operation is an operation that does not block the execution of the program while it is waiting for the operation to complete. This means that the program can continue to run and perform other tasks while the I/O operation is being performed in the background.
> 
> Node.js is built on top of the Chrome V8 JavaScript engine, which is designed to run JavaScript on the server side. One of the key features of Node.js is its use of non-blocking I/O, which allows it to efficiently handle many concurrent connections and perform tasks asynchronously.

> ### Appendix: About V8 JavaScript Engine
> 
> Node.js is built on top of the V8 JavaScript engine, which is developed and maintained by Google. V8 is a high-performance open-source JavaScript engine that is designed to execute JavaScript code quickly and efficiently. It is written in C++ and is used to power the Google Chrome web browser, as well as several other projects.
> 
> V8 is designed to execute modern JavaScript code, including code written in ECMAScript versions 6 and later. It includes features such as support for classes, arrow functions, and Promises, as well as just-in-time (JIT) compilation, which allows it to execute code faster by compiling it to native machine code at runtime.
> 
> V8 is an important component of the Node.js runtime, as it is responsible for executing the JavaScript code that runs in a Node.js application. It is tightly integrated with the Node.js runtime and provides many of the features that make Node.js well-suited for building scalable network applications.
> 
> Here is a simplified illustration of how the V8 engine works:
> 
> 1. The V8 engine receives JavaScript code as input.
> 1. The code is parsed and transformed into an intermediate representation (IR) that is easier for the V8 engine to understand.
> 1. The IR is optimized for faster execution by applying various optimization techniques such as constant folding and inlining.
> 1. The optimized IR is compiled into native machine code using a JIT compiler.
> 1. The native machine code is executed by the CPU.

The event loop has several phases, including:

![nodejs-eventloop.png](/nodejs-eventloop.png =700x){.align-center}

- **Timers**: This phase executes callback functions scheduled by `setTimeout()` and `setInterval()`.
- **Pending callbacks**: This phase executes I/O callbacks that have completed a blocking operation.
- **Idle, prepare**: These are internal phases used by the event loop.
- **Poll**: This phase retrieves new I/O events and executes their callbacks. If there are no I/O events to process, the event loop will block in this phase and wait for new events to arrive.
- **Check**: This phase executes callbacks scheduled by `setImmediate()`.
- **Close callbacks**: This phase executes close callbacks, such as those scheduled by `socket.on('close', ...)`.

In each iteration of the event loop, the event loop processes events in the order specified by the phases described above. When an event is processed, the associated callback function is executed, and the event is removed from the queue.

The event loop is an important concept in Node.js because it allows the runtime to perform many tasks concurrently, instead of blocking and waiting for each task to complete before moving on to the next one. This makes it possible to build high-performance, scalable applications with Node.js.

## More detailed explanation of each phase


### Timers

This phase executes callback functions that have been scheduled using `setTimeout()` and `setInterval()`. When a timer is scheduled, it is added to the timer queue, and the event loop will execute its callback when the specified time has elapsed. If multiple timers are scheduled to expire at the same time, their callbacks will be executed in the order in which they were added to the queue.

### Pending callbacks

This phase executes callbacks that have completed a blocking operation, such as reading from a file or making an HTTP request. These callbacks are added to the "pending callback" queue by the Node.js runtime when the blocking operation is initiated, and they are executed in the order in which they were added to the queue.

### Idle, prepare

These are internal phases of the event loop that are used to perform various tasks such as updating the list of watchers for file system events, and cleaning up internal data structures.


### Poll

This phase retrieves new I/O events and executes their callbacks. The event loop will block in this phase if there are no events to process, and it will wait for new events to arrive. The length of time that the event loop will block in this phase is determined by the `poll` phase timeout, which is a configurable value. When the event loop is unblocked, it will execute the callbacks for any new events that have arrived, and then return to the poll phase to check for more events.

### Check

This phase executes callbacks that have been scheduled using `setImmediate()`. These callbacks are added to the "check" queue and are executed in the order in which they were added to the queue.

### Close callbacks

This phase executes close callbacks, such as those scheduled using `socket.on('close', ...)`. These callbacks are executed when a socket or other resource is closed, and they are typically used to clean up resources or perform other tasks related to closing the resource.

## Event Loop Examples

```js
setTimeout(function() {
  console.log('Timeout callback');
}, 1000);

console.log('Start');

// Output: "Start", followed by "Timeout callback" after 1 second
```

In this example, we schedule a callback function using `setTimeout()` to be executed after 1 second (1000 milliseconds). The event loop will enter the "timers" phase after 1 second has elapsed, and it will execute the callback function.

---


```js
const fs = require('fs');

fs.readFile('file.txt', function(err, data) {
  console.log('File read callback');
});

console.log('Start');

// Output: "Start", followed by "File read callback" when the file has been read
```

In this example, we initiate a blocking I/O operation by reading a file using the fs module. When the file read operation is completed, the callback function is added to the "pending callbacks" queue, and it will be executed by the event loop in the next iteration.

---

```js
setImmediate(function() {
  console.log('Immediate callback');
});

console.log('Start');

// Output: "Start", followed by "Immediate callback"
```

In this example, we schedule a callback function using setImmediate() to be executed as soon as possible. The event loop will enter the "check" phase on the next iteration and execute the callback function.

## Deep dive with pseudo code

```js
const fs = require('fs');

// Pending callbacks
const pendingCallbacks = [];

// Timers
const timers = [];

// SetImmediate callbacks
const immediateCallbacks = [];

// A map of file descriptor to event handlers
const fdHandlers = new Map();

// A queue of file descriptor events to process
const fdEvents = [];

// Add a callback to the pending callbacks queue
function addPendingCallback(callback) {
  pendingCallbacks.push(callback);
}

// Add a timer to the timer queue
function addTimer(callback, timeout) {
  const expiration = Date.now() + timeout;
  timers.push({ callback, expiration });
  timers.sort((a, b) => a.expiration - b.expiration);
}

// Add a SetImmediate callback to the queue
function addImmediateCallback(callback) {
  immediateCallbacks.push(callback);
}

// Add an event handler for a file descriptor
function addFdHandler(fd, handler) {
  fdHandlers.set(fd, handler);
}

// Add a file descriptor event to the queue
function addFdEvent(fd, eventType) {
  fdEvents.push({ fd, eventType });
}

// The main event loop
function eventLoop() {
  // Execute any pending callbacks
  while (pendingCallbacks.length > 0) {
    const callback = pendingCallbacks.shift();
    callback();
  }

  // Execute any timers that have expired
  const now = Date.now();
  while (timers.length > 0 && timers[0].expiration <= now) {
    const timer = timers.shift();
    timer.callback();
  }

  // Execute any SetImmediate callbacks
  while (immediateCallbacks.length > 0) {
    const callback = immediateCallbacks.shift();
    callback();
  }

  // Process any file descriptor events
  while (fdEvents.length > 0) {
    const { fd, eventType } = fdEvents.shift();
    const handler = fdHandlers.get(fd);
    if (handler) {
      handler(fd, eventType);
    }
  }

  // Wait for new events to arrive
  waitForEvents();
}

// Wait for new events to arrive
function waitForEvents() {
  // Use a blocking system call like epoll() or select() to wait for new events
  // When events are available, add them to the appropriate queue (pending callbacks, timers, etc.)
  // and schedule the event loop to run again using process.nextTick()
}

// Run the event loop
function run() {
  process.nextTick(eventLoop);
}

run();

// Example usage
fs.readFile('file.txt', function(err, data) {
  addPendingCallback(function() {
    console.log('File read callback');
  });
});

addTimer(function() {
  console.log('Timeout callback');
}, 1000);

setImmediate(function() {
  console.log('Immediate callback');
});
```

The code defines several arrays and maps to store various types of events:

- `pendingCallbacks`: An array of callbacks that have completed a blocking operation and are ready to be executed.
- `timers`: An array of timers that have been scheduled using `setTimeout()` or `setInterval()`.
- `immediateCallbacks`: An array of callbacks that have been scheduled using setImmediate() and are ready to be executed.
- `fdHandlers`: A map of file descriptor to event handlers.
- `fdEvents`: An array of file descriptor events that are ready to be processed.

The code also defines several functions to add events to these arrays and maps:

- `addPendingCallback(callback)`: Adds a callback to the `pendingCallbacks` array.
- `addTimer(callback, timeout)`: Adds a timer to the `timers` array.
- `addImmediateCallback(callback)`: Adds a callback to the `immediateCallbacks` array.
- `addFdHandler(fd, handler)`: Adds an event handler for a file descriptor to the `fdHandlers` map.
- `addFdEvent(fd, eventType)`: Adds a file descriptor event to the `fdEvents` array.

The main event loop is defined in the eventLoop() function. This function processes events in the following order:

- **Pending callbacks**: Callbacks in the `pendingCallbacks` array are executed in the order in which they were added.
- **Timers**: Timers in the `timers` array that have expired are executed in the order in which they were added.
- **SetImmediate callbacks**: Callbacks in the `immediateCallbacks` array are executed in the order in which they were added.
- **File descriptor events**: Events in the `fdEvents` array are processed by executing the corresponding event handler from the `fdHandlers` map.

Finally, the `waitForEvents()` function is called to wait for new events to arrive. This function could be implemented using a variety of techniques such as using `setTimeout()` or using a blocking system call like `epoll() `on Linux.

> ### Appendix: About epoll() on Linux
> 
> `epoll` is a Linux kernel system call that provides a scalable I/O event notification mechanism. It is used to monitor a set of file descriptors for events such as data availability or connection readiness, and it can be used to implement efficient I/O multiplexing in networked applications.
> 
> `epoll` operates in one of two modes: edge-triggered or level-triggered. In edge-triggered mode, an event is generated only when the state of a file descriptor changes. In level-triggered mode, an event is generated whenever the file descriptor is in a particular state, such as when data is available to be read.
> 
> `epoll` is often used in conjunction with the `select()` system call, which allows a program to monitor multiple file descriptors for events. `epoll` provides a more efficient way to monitor large numbers of file descriptors and is especially useful for high-concurrency servers.
> 
> `libuv`, the cross-platform library used by Node.js, provides a wrapper around `epoll` and other platform-specific APIs to provide a consistent interface for asynchronous I/O operations. This allows Node.js applications to take advantage of the scalability and efficiency of `epoll` on Linux without having to directly use the `epoll` system call.

> ### About libuv
> 
> libuv is a cross-platform library that provides support for asynchronous I/O and other utility functions. It is used as the underlying platform layer for Node.js and is responsible for implementing the event loop and other asynchronous mechanisms in the Node.js runtime.
> 
> libuv is written in C and provides a consistent API for various types of asynchronous operations such as file I/O, network operations, timers, and process management. It abstracts away the differences between various platform-specific APIs, such as epoll on Linux and kqueue on macOS, making it easier to write cross-platform code that works on multiple operating systems.
> 
> libuv is an important component of the Node.js runtime and is responsible for providing many of the features that make Node.js well-suited for building scalable network applications.

## More

- [The Node.js Event Loop, Timers, and process.nextTick()*nodejs.org*](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)
{.links-list}