---
title: Kotlin 和 CORS：跨源资源共享指南
description: 
published: true
date: 2023-02-12T06:56:06.938Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:56:05.328Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and CORS: A Guide to Cross-Origin Resource Sharing***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-cors-a-guide-to-cross-origin-resource-sharing)
{.links-list}

      
Kotlin 和 CORS：跨源资源共享指南

跨源资源共享 (CORS) 是一种机制，允许从提供第一个资源的域之外的另一个域请求网页上的受限资源。网页可以自由嵌入跨源图像、样式表、脚本、iframe 和视频。

CORS 机制通过向跨域 HTTP 请求和响应添加 HTTP 标头来工作。

## CORS 是如何工作的？

当浏览器向服务器发送请求时，浏览器会包含一个 Origin 标头。此标头指示发出请求的页面的域。

然后服务器可以根据 Origin 标头的值选择允许或拒绝请求。

如果服务器允许该请求，它将在响应中包含以下标头：
- Access-Control-Allow-Origin：此标头表示服务器允许跨域请求。
- Access-Control-Allow-Methods：此标头指示允许客户端使用的方法（例如 GET、POST 等）。
- Access-Control-Allow-Headers：此标头表示允许客户端使用的标头。
- Access-Control-Expose-Headers：此标头指示允许客户端访问哪些标头。

如果服务器不允许该请求，它将返回一个错误。

## 为什么 CORS 很重要？

CORS 机制为基于浏览器的应用程序提供了一种方式来发出跨源请求，同时仍然遵守同源策略。

同源策略是一种旨在防止跨源请求的安全措施。但是，跨源请求有许多合法用途，例如向不同的域发出请求以检索数据或使用第三方服务。

CORS 提供了一种允许这些类型的跨源请求的方法，同时仍然提供一些针对恶意请求的保护。

## 有哪些 CORS 示例？

以下是如何使用 CORS 的一些示例：

- 发出跨源请求以从第三方服务检索数据的网页。
- 发出跨源请求以从不同域加载脚本的网页。
- 向页面上嵌入的 iframe 发出跨源请求的网页。

## CORS 有哪些限制？

CORS 并不是一个完美的解决方案。最大的限制是并非所有浏览器都支持它。

此外，恶意请求可以绕过 CORS。例如，恶意请求可以使用 XMLHttpRequest 对象发出没有 CORS 标头的跨源请求。

## 如何使用 CORS？

如果要使用 CORS，则需要设置支持 CORS 的服务器。

 设置服务器超出了本文的范围，但您可以在下面的参考资料部分找到更多信息。

拥有支持 CORS 的服务器后，您可以使用 XMLHttpRequest 或 Fetch API 发出跨域请求。

## 什么是预检请求？

预检请求是在跨源请求之前发送的 HTTP 请求。预检请求用于确定跨源请求是否可以安全发送。

预检请求与以下标头一起发送：
- 来源：发出请求的页面的域。
- Access-Control-Request-Method：将用于跨源请求的方法（例如 GET、POST 等）。
- Access-Control-Request-Headers：将用于跨源请求的标头。

然后服务器可以根据这些标头的值选择允许或拒绝请求。

如果服务器允许该请求，它将在响应中包含以下标头：
- Access-Control-Allow-Origin：此标头表示服务器允许跨域请求。
- Access-Control-Allow-Methods：此标头指示允许客户端使用的方法（例如 GET、POST 等）。
- Access-Control-Allow-Headers：此标头表示允许客户端使用的标头。
- Access-Control-Max-Age：此标头指示响应可以缓存多长时间。

如果服务器不允许该请求，它将返回一个错误。

## 什么是预检请求？

预检请求是在跨源请求之前发送的 HTTP 请求。预检请求用于确定跨源请求是否可以安全发送。

预检请求与以下标头一起发送：
- 来源：发出请求的页面的域。
- Access-Control-Request-Method：将用于跨源请求的方法（例如 GET、POST 等）。
- Access-Control-Request-Headers：将用于跨源请求的标头。

然后服务器可以根据这些标头的值选择允许或拒绝请求。

如果服务器允许该请求，它将在响应中包含以下标头：
- Access-Control-Allow-Origin：此标头表示服务器允许跨域请求。
- Access-Control-Allow-Methods：此标头指示允许客户端使用的方法（例如 GET、POST 等）。
- Access-Control-Allow-Headers：此标头表示允许客户端使用的标头。
- Access-Control-Max-Age：此标头指示响应可以缓存多长时间。

如果服务器不允许该请求，它将返回一个错误。

## 使用 CORS 有哪些技巧？

以下是使用 CORS 的一些提示：

- 使用 XMLHttpRequest 或 Fetch API 进行跨域请求。
- 将 Origin 标头设置为发出请求的页面的域。
- 将 Access-Control-Request-Method 标头设置为将用于跨源请求的方法（例如 GET、POST 等）。
- 将 Access-Control-Request-Headers 标头设置为将用于跨域请求的标头。
- 如果服务器允许请求，它将在响应中包含以下标头：Access-Control-Allow-Origin、Access-Control-Allow-Methods、Access-Control-Allow-Headers 和 Access-Control-Max-Age .
- 如果服务器不允许该请求，它将返回一个错误。

## 结论

CORS 是一种机制，允许从提供第一个资源的域之外的另一个域请求网页上的受限资源。网页可以自由嵌入跨源图像、样式表、脚本、iframe 和视频。

CORS 机制通过向跨域 HTTP 请求和响应添加 HTTP 标头来工作。

当浏览器向服务器发送请求时，浏览器会包含一个 Origin 标头。此标头指示发出请求的页面的域。

然后服务器可以根据 Origin 标头的值选择允许或拒绝请求。

如果服务器允许请求，它将在响应中包含以下标头：Access-Control-Allow-Origin、Access-Control-Allow-Methods、Access-Control-Allow-Headers 和 Access-Control-Expose-Headers。

如果服务器不允许该请求，它将返回一个错误。

CORS 机制为基于浏览器的应用程序提供了一种方式来发出跨源请求，同时仍然遵守同源策略。

同源策略是一种旨在防止跨源请求的安全措施。但是，跨源请求有许多合法用途，例如向不同的域发出请求以检索数据或使用第三方服务。

CORS 提供了一种允许这些类型的跨源请求的方法，同时仍然提供一些针对恶意请求的保护。

如果要使用 CORS，则需要设置支持 CORS 的服务器。设置服务器超出了本文的范围，但您可以在下面的参考资料部分找到更多信息。

拥有支持 CORS 的服务器后，您可以使用 XMLHttpRequest 或 Fetch API 发出跨域请求。

预检请求是在跨源请求之前发送的 HTTP 请求。预检请求用于确定跨源请求是否可以安全发送。

预检请求与以下标头一起发送：Origin、Access-Control-Request-Method 和 Access-Control-Request-Headers。

然后服务器可以根据这些标头的值选择允许或拒绝请求。

如果服务器允许请求，它将在响应中包含以下标头：Access-Control-Allow-Origin、Access-Control-Allow-Methods、Access-Control-Allow-Headers 和 Access-Control-Max-Age。

如果服务器不允许该请求，它将返回一个错误。

以下是使用 CORS 的一些提示：

- 使用 XMLHttpRequest 或 Fetch API 进行跨域请求。
- 将 Origin 标头设置为发出请求的页面的域。
- 将 Access-Control-Request-Method 标头设置为将用于跨源请求的方法（例如 GET、POST 等）。
- 将 Access-Control-Request-Headers 标头设置为将用于跨源请求的标头。
- 如果服务器允许请求，它将在响应中包含以下标头：Access-Control-Allow-Origin、Access-Control-Allow-Methods、Access-Control-Allow-Headers 和 Access-Control-Max-Age .
- 如果服务器不允许该请求，它将返回一个错误。