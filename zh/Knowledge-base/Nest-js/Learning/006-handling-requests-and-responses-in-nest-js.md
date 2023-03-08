---
title: 006: 在 Nest.js 中处理请求和响应
description: 
published: true
date: 2023-02-14T17:32:29.574Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:32:27.899Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [006: Handling requests and responses in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/006-handling-requests-and-responses-in-nest-js)
{.links-list}


## 介绍

在 Nest.js 中，处理请求和响应是一个两步过程。首先，您需要创建一个请求处理程序来接收传入的请求并对其进行处理。其次，您需要创建一个响应处理程序，将处理后的数据发送回客户端。

创建请求处理程序很简单。您需要做的就是创建一个接受请求和响应对象的函数，然后在该函数中编写代码。

```javascript
function requestHandler(req, res) {
  // your code here
}
```

请求对象包含有关传入请求的信息，例如 URL、标头和正文。响应对象用于将数据发送回客户端。

创建响应处理程序同样简单。您需要做的就是创建一个接收数据对象和响应对象的函数，然后在该函数中编写代码。

```javascript
function responseHandler(data, res) {
  // your code here
}
```

数据对象包含您要发送回客户端的数据。响应对象用于将数据发送回客户端。

## 发送响应

创建请求和响应处理程序后，您需要告诉 Nest.js 如何将响应发送回客户端。这是使用 ```res.send()``` 函数完成的。

```javascript
function responseHandler(data, res) {
  res.send(data, 200);
}
```res.send()``` 函数的示例：

```javascript
function responseHandler(data, res) {
  res.json(data, 200);
}
```

## 发送一个 JSON 响应

如果你想发送一个 JSON 响应，你可以使用 ```res.json()``` 函数。 ```res.json()``` 函数有两个参数：要发送的数据和 HTTP 状态代码。

以下是如何使用 ```res.json()``` 函数的示例：

```javascript
function responseHandler(data, res) {
  res.render('index.html', data);
}
```

## 发送 HTML 响应

如果你想发送一个 HTML 响应，你可以使用 ```res.render()``` 函数。 ```res.render()``` 函数有两个参数：HTML 文件的路径，以及包含要传递给 HTML 文件的数据的对象。

下面是一个如何使用 ```res.render()``` 函数的例子：

```javascript
function responseHandler(data, res) {
  res.sendFile('/path/to/file.txt', {
    root: __dirname
  });
}
```

## 发送文件

如果你想发送一个文件，你可以使用```res.sendFile()```函数。 ```res.sendFile()``` 函数有两个参数：文件的路径和一个包含发送文件选项的对象。

以下是如何使用 ```res.sendFile()``` 函数的示例：

```javascript
function responseHandler(data, res) {
  res.redirect('/path/to/new/page');
}
```

## 发送重定向

如果你想发送一个重定向，你可以使用 ```res.redirect()``` 函数。 ```res.redirect()``` 函数接受一个参数：要重定向到的 URL。

以下是如何使用 ```res.redirect()``` 函数的示例：

```javascript
函数响应处理程序（数据，资源）{
  res.redirect('/path/to/new/page');
}
```

## 结论

在 Nest.js 中，处理请求和响应是一个两步过程。首先，您需要创建一个请求处理程序来接收传入的请求并对其进行处理。其次，您需要创建一个响应处理程序，将处理后的数据发送回客户端。

创建请求处理程序很简单。您需要做的就是创建一个接受请求和响应对象的函数，然后在该函数中编写代码。

创建响应处理程序同样简单。您需要做的就是创建一个接收数据对象和响应对象的函数，然后在该函数中编写代码。

创建请求和响应处理程序后，您需要告诉 Nest.js 如何将响应发送回客户端。这是使用 ```res.send()``` 函数完成的。

如果你想发送一个 JSON 响应，你可以使用 ```res.json()``` 函数。如果你想发送一个 HTML 响应，你可以使用 ```res.render()``` 函数。如果你想发送一个文件，你可以使用```res.sendFile()```函数。如果你想发送一个重定向，你可以使用 ```res.redirect()``` 函数。