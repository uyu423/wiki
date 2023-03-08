---
title: 006: Handling requests and responses in Nest.js
description: 
published: true
date: 2023-02-14T17:32:35.539Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:32:27.908Z
---

- [006: Manejo de solicitudes y respuestas en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/006-handling-requests-and-responses-in-nest-js)
{.links-list}
- [006: 在 Nest.js 中处理请求和响应***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/006-handling-requests-and-responses-in-nest-js)
{.links-list}
- [006: Nest.js에서 요청 및 응답 처리***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/006-handling-requests-and-responses-in-nest-js)
{.links-list}


## Introduction

In Nest.js, handling requests and responses is a two-step process. First, you need to create a request handler that will receive the incoming request and process it. Second, you need to create a response handler that will send the processed data back to the client.

Creating a request handler is simple. All you need to do is create a function that takes in a request and a response object, and then write your code inside that function.

```javascript
function requestHandler(req, res) {
  // your code here
}
```

The request object contains information about the incoming request, such as the URL, the headers, and the body. The response object is used to send data back to the client.

Creating a response handler is just as simple. All you need to do is create a function that takes in a data object and a response object, and then write your code inside that function.

```javascript
function responseHandler(data, res) {
  // your code here
}
```

The data object contains the data that you want to send back to the client. The response object is used to send the data back to the client.

## Sending a response

Once you have created your request and response handlers, you need to tell Nest.js how to send the response back to the client. This is done using the ```res.send()``` function.

The ```res.send()``` function takes two arguments: the data to be sent, and the HTTP status code. The HTTP status code is optional, but it is generally a good idea to include it.

Here is an example of how to use the ```res.send()``` function:

```javascript
function responseHandler(data, res) {
  res.send(data, 200);
}
```

## Sending a JSON response

If you want to send a JSON response, you can use the ```res.json()``` function. The ```res.json()``` function takes two arguments: the data to be sent, and the HTTP status code.

Here is an example of how to use the ```res.json()``` function:

```javascript
function responseHandler(data, res) {
  res.json(data, 200);
}
```

## Sending an HTML response

If you want to send an HTML response, you can use the ```res.render()``` function. The ```res.render()``` function takes two arguments: the path to the HTML file, and an object containing the data to be passed to the HTML file.

Here is an example of how to use the ```res.render()``` function:

```javascript
function responseHandler(data, res) {
  res.render('index.html', data);
}
```

## Sending a file

If you want to send a file, you can use the ```res.sendFile()``` function. The ```res.sendFile()``` function takes two arguments: the path to the file, and an object containing the options for sending the file.

Here is an example of how to use the ```res.sendFile()``` function:

```javascript
function responseHandler(data, res) {
  res.sendFile('/path/to/file.txt', {
    root: __dirname
  });
}
```

## Sending a redirect

If you want to send a redirect, you can use the ```res.redirect()``` function. The ```res.redirect()``` function takes one argument: the URL to redirect to.

Here is an example of how to use the ```res.redirect()``` function:

```javascript
function responseHandler(data, res) {
  res.redirect('/path/to/new/page');
}
```

## Conclusion

In Nest.js, handling requests and responses is a two-step process. First, you need to create a request handler that will receive the incoming request and process it. Second, you need to create a response handler that will send the processed data back to the client.

Creating a request handler is simple. All you need to do is create a function that takes in a request and a response object, and then write your code inside that function.

Creating a response handler is just as simple. All you need to do is create a function that takes in a data object and a response object, and then write your code inside that function.

Once you have created your request and response handlers, you need to tell Nest.js how to send the response back to the client. This is done using the ```res.send()``` function.

If you want to send a JSON response, you can use the ```res.json()``` function. If you want to send an HTML response, you can use the ```res.render()``` function. If you want to send a file, you can use the ```res.sendFile()``` function. If you want to send a redirect, you can use the ```res.redirect()``` function.