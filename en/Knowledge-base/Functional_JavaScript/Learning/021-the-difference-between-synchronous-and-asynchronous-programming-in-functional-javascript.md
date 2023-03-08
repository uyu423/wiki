---
title: 021: The difference between synchronous and asynchronous programming in functional JavaScript
description: 
published: true
date: 2023-02-17T17:06:46.944Z
tags: 
editor: markdown
dateCreated: 2023-02-17T17:06:40.173Z
---

- [021: 기능적 JavaScript에서 동기 프로그래밍과 비동기 프로그래밍의 차이점***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/021-the-difference-between-synchronous-and-asynchronous-programming-in-functional-javascript)
{.links-list}


# The difference between synchronous and asynchronous programming in functional JavaScript

Functional programming is a programming paradigm that uses functions to operate on data structures. In functional programming, data is immutable, meaning that it can't be changed. Functions are written to take arguments and return a value.

JavaScript is a functional programming language. It has first-class functions, meaning that functions can be passed as arguments to other functions and returned from functions.

There are two types of programming: synchronous and asynchronous. In synchronous programming, code is executed in order. In asynchronous programming, code is executed in parallel.

Synchronous programming is easier to reason about because the code executes in a predictable order. Asynchronous programming is more efficient because it can make better use of resources.

In JavaScript, all code is executed synchronously. However, JavaScript has an event-based model that allows code to be executed asynchronously.

Events are actions that happen in the browser, such as a user clicking a button. When an event happens, an event listener function is called. The event listener function can execute code asynchronously.

Asynchronous programming in JavaScript is often used to handle user input, communicate with a server, or load resources.

Here's an example of asynchronous programming in JavaScript. The code below logs "Hello, world!" to the console when the button is clicked:

```javascript
function onClick() {
  console.log("Hello, world!");
}

document.getElementById("button").addEventListener("click", onClick);
```

In the code above, the onClick function is executed asynchronously when the button is clicked.

Asynchronous programming can be confusing because the code doesn't execute in order. It's important to understand how the JavaScript event loop works in order to write asynchronous code correctly.

The event loop is a mechanism that checks for events and executes the event handlers. The event loop is single-threaded, meaning that only one event can be processed at a time.

When an event happens, the event handler is added to the event queue. The event queue is processed in order, and the event handlers are executed one at a time.

This means that if an event handler takes a long time to execute, the browser will be unresponsive because the event loop can't process other events.

It's important to keep event handlers short so that the event loop can continue to process other events. If an event handler needs to do a long-running task, such as making a network request, it should use an asynchronous function.

Asynchronous functions are functions that return immediately. The code below makes an asynchronous network request and logs the response to the console:

```javascript
function makeRequest() {
  console.log("Making a request...");

  setTimeout(function() {
    console.log("Request made.");
  }, 1000);
}

makeRequest();
```

In the code above, the makeRequest function returns immediately. The setTimeout function is used to delay the execution of the code inside the function.

The setTimeout function takes two arguments: a function to execute and a delay in milliseconds. The function is executed after the delay.

In the code above, the function is executed after a delay of 1000 milliseconds, or 1 second.

Asynchronous programming can be difficult to reason about because the code doesn't execute in order. It's important to use tools like debugger statements and console.log to understand what's happening in your code.

Debugger statements can be used to pause the execution of code. The code below shows how to use a debugger statement:

```javascript
function makeRequest() {
  debugger;

  console.log("Making a request...");

  setTimeout(function() {
    console.log("Request made.");
  }, 1000);
}

makeRequest();
```

In the code above, the debugger statement pauses the execution of code. To resume execution, use the "resume" button in the debugger.

Console.log can be used to print values to the console. The code below shows how to use console.log:

```javascript
function makeRequest() {
  console.log("Making a request...");

  setTimeout(function() {
    console.log("Request made.");
  }, 1000);
}

makeRequest();
```

In the code above, the console.log statement prints the string "Making a request..." to the console.

Asynchronous programming can be difficult to get right. It's important to use tools like debugger statements and console.log to understand what's happening in your code.

It's also important to use libraries and frameworks that handle asynchronous code correctly. For example, React uses a library called React Async to handle asynchronous code.

React Async is a library that provides a set of React components for working with asynchronous code. React Async also provides a higher-order component for loading data.

The code below shows how to use React Async to load data:

```javascript
import React from "react";
import { render } from "react-dom";
import { loadData } from "react-async";

function App() {
  return (
    <div>
      <h1>Hello, world!</h1>
    </div>
  );
}

const AppWithData = loadData(App, {
  loadData: () => fetch("/data.json").then(response => response.json())
});

render(<AppWithData />, document.getElementById("root"));
```

In the code above, the AppWithData component is a higher-order component that loads data. The data is loaded from the "/data.json" endpoint.

The AppWithData component renders the App component with the data. The App component renders a heading with the data.

React Async is a library that makes it easier to work with asynchronous code in React. It's important to use libraries and frameworks that handle asynchronous code correctly.

# Additional Information

Additional information about the topic can be found here:

- [MDN: Synchronous and Asynchronous Programming](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts)
- [YouTube: What is the Event Loop?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
- [React Async](https://github.com/react-async/react-async)