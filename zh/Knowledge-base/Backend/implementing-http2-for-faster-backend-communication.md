---
title: 实现 HTTP/2 以实现更快的后端通信
description: 
published: true
date: 2023-02-15T02:17:18.060Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:17:16.211Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Implementing HTTP/2 for Faster Backend Communication***English** document is available*](/en/Knowledge-base/Backend/implementing-http2-for-faster-backend-communication)
{.links-list}


HTTP/2 是万维网使用的 HTTP 网络协议的重大修订版。它源自较早的实验性 SPDY 协议，最初由 Google 开发。 HTTP/2 于 2015 年 5 月作为 RFC 7540 发布。

HTTP/2 不向后兼容 HTTP/1.x，并且需要 HTTPS。

HTTP/2 的主要目标是通过启用完整的请求和响应多路复用来减少延迟，通过紧凑的标头最小化协议开销，并添加对请求优先级和服务器推送的支持。

HTTP/2 是二进制的，而不是文本的。它通过单个连接多路复用多个请求和响应，而不是让每个请求等待前一个请求完成。这允许客户端和服务器之间更快、更有效的通信。

HTTP/2 还使用标头压缩来减小标头的大小，与 HTTP/1.x 相比最多可减少 80%。这会减少通过网络发送的数据，从而减少延迟。

HTTP/2 还引入了对请求优先级的支持，它允许客户端指定服务器处理请求的顺序。这可用于提高页面加载的性能，例如，通过首先加载关键资源。

最后，HTTP/2 引入了对服务器推送的支持，它允许服务器主动向客户端发送它预期客户端需要的资源，甚至在客户端请求它们之前。这可用于提高页面加载的性能，因为客户端无需多次往返服务器以获取所有必要的资源。

 实施 HTTP/2

要利用 HTTP/2，您需要确保您的服务器和客户端都支持 HTTP/2。

在服务器端，您需要使用支持 HTTP/2 的 Web 服务器。例如，Apache HTTP Server 从 2015 年 12 月发布的 2.4.17 版本开始支持 HTTP/2。

在客户端，您需要使用支持 HTTP/2 的 Web 浏览器。例如，目前所有主要的网络浏览器都支持 HTTP/2，包括 Google Chrome、Mozilla Firefox、Microsoft Edge 和 Apple Safari。

确保您的服务器和客户端都支持 HTTP/2 后，您可以在访问您的网站时通过简单地使用 https:// 协议而不是 http:// 来开始使用 HTTP/2。您的服务器将自动与客户端协商 HTTP/2，并且所有通信都将通过 HTTP/2 进行。

如果您想在不使用 HTTPS 的情况下使用 HTTP/2，您可以将服务器配置为通过明文 TCP 连接使用 HTTP/2。但是，通常不推荐这样做，因为它抵消了 HTTP/2 的许多好处，并且并非所有客户端都支持。

结论

HTTP/2 是 HTTP 网络协议的重大修订版，与 HTTP/1.x 相比提供了显着的性能改进。要利用 HTTP/2，您需要确保您的服务器和客户端都支持 HTTP/2。完成后，您可以在访问您的网站时通过简单地使用 https:// 协议而不是 http:// 来开始使用 HTTP/2。