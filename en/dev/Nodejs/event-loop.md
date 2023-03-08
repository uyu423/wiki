---
title: Event Loop
description: 
published: true
date: 2023-02-17T18:00:37.104Z
tags: nodejs, english, v8
editor: markdown
dateCreated: 2022-12-26T12:34:04.672Z
---

- [이벤트 루프 (Event Loop)***Korean** version of this document is available*](/ko/dev/Nodejs/event-loop)
{.links-list}

## Overview

The Node.js event loop is a fundamental part of the runtime that allows Node.js to perform non-blocking I/O operations efficiently. It works by continuously monitoring the event queue and executing any events that are ready to be processed.

- The event loop is a single-threaded event loop. This means that only one event can be processed at a time, and events are processed in the order in which they are received. However, Node.js can use multiple threads for certain types of operations, such as performing CPU-intensive tasks or making blocking system calls.
- The event loop is responsible for executing most of the JavaScript code that runs in a Node.js application. This includes both user code and code provided by the Node.js runtime and its standard library.
- The event loop is designed to be non-blocking, which means that it can process events concurrently without waiting for each event to complete before moving on to the next one. This is achieved through the use of non-blocking I/O operations and asynchronous callback functions.
- The event loop is implemented using a combination of JavaScript and native code. The JavaScript portion of the event loop is written in C++ and compiled to native code using the V8 JavaScript engine, while the native portion is implemented using platform-specific APIs.
- The event loop has several phases, each of which is responsible for processing a specific type of event. The order in which the phases are executed can vary depending on the specific version of Node.js being used.

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

> **Q. Does the timer in the event loop guarantee an exact execution time?**
> 
> No, the event loop's `tick` in Node.js does not guarantee an exact execution time, just like the timer functions `setTimeout()` and `setInterval()`.
> 
> The `tick` in the Node.js event loop is a unit of time that represents the smallest possible delay between two successive iterations of the event loop. It is typically much shorter than the time units used by the timer functions, such as milliseconds or seconds.
> 
> However, the actual execution time of a callback function scheduled using the event loop's `tick` may vary due to factors such as system load and the presence of other tasks in the event queue. Therefore, it is not possible to guarantee an exact execution time for tasks scheduled using the event loop's `tick`.
> 
> In general, the error will be relatively small for most applications, and may not be noticeable in most cases. However, if you need to execute a task at a specific time or with a specific level of accuracy, it is important to be aware that the timer functions in the event loop and the event loop's `tick` function may not be suitable for your needs.
> 
> In these cases, you may need to use a different approach, such as using a hardware timer or implementing your own timing mechanism. It is also important to carefully consider the requirements of your application and the level of accuracy that is needed, and to choose an appropriate approach based on those requirements.

### Pending callbacks

This phase executes callbacks that have completed a blocking operation, such as reading from a file or making an HTTP request. These callbacks are added to the "pending callback" queue by the Node.js runtime when the blocking operation is initiated, and they are executed in the order in which they were added to the queue.

### Idle, prepare

These are internal phases of the event loop that are used to perform various tasks such as updating the list of watchers for file system events, and cleaning up internal data structures.

> **Q. What happens in the "Idle, prepare" phase of the event loop?**
> 
> In the "Idle, prepare" phase of the Node.js event loop, the event loop checks for any tasks that need to be scheduled for the next iteration of the loop.
> 
> The event loop in Node.js consists of a series of phases, each of which processes a specific type of task. The "Idle, prepare" phase is the first phase in the event loop, and it is followed by the "Poll" phase, the "Check" phase, and the "Close callbacks" phase.
> 
> During the "Idle, prepare" phase, the event loop performs the following tasks:
> 
> - It checks for any tasks that have been scheduled using the `process.nextTick()` function, and adds them to the event queue to be executed on the next iteration of the event loop.
> - It checks for any `Promise` objects that have been rejected and have no error handler, and schedules their rejection handling to be performed on the next iteration of the event loop.
> - It checks for any timers that have expired (such as those set using `setTimeout()` or `setInterval()`), and adds their callback functions to the event queue to be executed on the next iteration of the event loop.
> 
> Once these tasks have been completed, the event loop moves on to the next phase, the "Poll" phase, where it waits for new events to arrive or for previously scheduled tasks to be ready for execution.

### Poll

It waits for new events to arrive or for previously scheduled tasks to be ready for execution. The event loop uses an internal mechanism, such as `poll()`, `epoll()`, or `kqueue()`, to monitor the file descriptor sources that have been registered with it, and to receive notifications when events occur.

If a new event or task is available, the event loop retrieves it from the event queue and adds it to the "Check" phase queue to be processed on the next iteration of the event loop.

If the event queue is empty and there are no more events or tasks to process, the event loop goes into a "waiting" state, where it waits for new events or tasks to arrive.

Once the event loop has finished processing all available events and tasks in the "Poll" phase, it moves on to the next phase, the "Check" phase, where it processes any tasks that have been scheduled for the current iteration of the event loop.

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
>
> MacOS/BSD has a `kqueue()` that does the same thing as `epoll`, and Windows has `IOCP`(Input/Output Completion Ports).

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