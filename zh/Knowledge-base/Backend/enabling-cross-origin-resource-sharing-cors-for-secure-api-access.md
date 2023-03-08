---
title: 为安全 API 访问启用跨源资源共享 (CORS)
description: 
published: true
date: 2023-02-05T01:17:32.815Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:17:31.135Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Enabling Cross-Origin Resource Sharing (CORS) for Secure API Access***English** document is available*](/en/Knowledge-base/Backend/enabling-cross-origin-resource-sharing-cors-for-secure-api-access)
{.links-list}


# 为安全 API 访问启用跨源资源共享 (CORS)

## 介绍

简而言之，跨源资源共享 (CORS) 是一种机制，允许从提供第一个资源的域之外的另一个域请求网页上的受限资源。网页可以自由嵌入跨源图像、样式表、脚本、iframe 和视频。

为了让浏览器发出跨源请求，Web 应用程序必须首先启用 CORS。同源请求不需要启用 CORS，即向与页面本身相同的域、协议和端口号发出的请求。

## CORS 是如何工作的

当浏览器发出跨源请求时，浏览器会向服务器发送带有“Origin”标头的请求。 `Origin` 标头指示请求的来源，即发出请求的域、协议和端口号。

然后，服务器可以根据“Origin”标头选择允许或阻止请求。如果服务器允许该请求，它将在响应中设置一个“Access-Control-Allow-Origin”标头。 `Access-Control-Allow-Origin` 标头的值可以是特定来源（例如 `https://example.com`）、通配符 (`*`) 或 `null`。

如果响应中不存在“Access-Control-Allow-Origin”标头，或者其值不是有效来源，则浏览器将阻止响应。

## 为什么 CORS 很重要

如果没有 CORS，跨域请求将被浏览器阻止。这很重要，因为它可以防止恶意脚本向您的 API 发出未经授权的请求。

## 启用 CORS

### 设置 `Access-Control-Allow-Origin` 标头

`Access-Control-Allow-Origin` 标头告诉浏览器它是否应该允许来自请求来源的跨域请求。

您可以在服务器的 HTTP 响应中设置“Access-Control-Allow-Origin”标头。标头的值可以是特定来源（例如 `https://example.com`）、通配符 (`*`) 或 `null`。

如果你想允许来自任何来源的跨域请求，你可以将 `Access-Control-Allow-Origin` 标头设置为 `*`。

```
Access-Control-Allow-Origin: *
```

如果要允许来自特定来源的跨域请求，可以将 Access-Control-Allow-Origin 标头设置为请求的来源。

```
Access-Control-Allow-Origin: https://example.com
```

如果您想允许来自多个来源的跨域请求，您可以将“Access-Control-Allow-Origin”标头设置为以逗号分隔的来源列表。

```
Access-Control-Allow-Origin: https://example.com,https://example.org
```

如果要允许来自除特定来源之外的所有来源的跨域请求，可以将 `Access-Control-Allow-Origin` 标头设置为 `*` 并将 `Access-Control-Expose-Headers` 标头设置为 `Origin `。

```
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: Origin
```

### 设置 `Access-Control-Allow-Credentials` 标头

`Access-Control-Allow-Credentials` 标头告诉浏览器它是否应该发送带有跨源请求的 cookie。

如果你想允许 cookie 与跨源请求一起发送，你可以将 `Access-Control-Allow-Credentials` 标头设置为 `true`。

```
Access-Control-Allow-Credentials: true
```

如果你想允许来自特定来源的跨域请求发送 cookie，你可以将 `Access-Control-Allow-Origin` 标头设置为请求的来源和 `Access-Control-Allow-Credentials`标题为“真”。

```
Access-Control-Allow-Origin: https://example.com
Access-Control-Allow-Credentials: true
```

### 设置 `Access-Control-Expose-Headers` 标头

`Access-Control-Expose-Headers` 标头告诉浏览器它应该允许向客户端公开哪些标头。

如果要允许跨域请求公开所有标头，可以将 `Access-Control-Expose-Headers` 标头设置为 `*`。

```
Access-Control-Expose-Headers: *
```

如果要允许跨域请求公开特定标头，可以将 `Access-Control-Expose-Headers` 标头设置为您要允许的标头。

```
Access-Control-Expose-Headers: Content-Type
```

如果要允许跨域请求公开多个标头，可以将 `Access-Control-Expose-Headers` 标头设置为以逗号分隔的标头列表。

```
Access-Control-Expose-Headers: Content-Type,X-Custom-Header
```

## 预检请求

一些跨源请求是预检的。预检请求是使用“OPTIONS”HTTP 方法发出并具有“Origin”标头的请求。

浏览器向服务器发送预检请求，检查服务器是否允许跨域请求。服务器可以选择允许或阻止预检请求。

如果服务器允许预检请求，它将在响应中设置一个“Access-Control-Allow-Methods”标头。 “Access-Control-Allow-Methods”标头的值是服务器允许的以逗号分隔的 HTTP 方法列表。

如果服务器允许预检请求并且请求方法是“GET”、“HEAD”或“POST”，则服务器将在响应中设置一个“Access-Control-Allow-Headers”标头。 `Access-Control-Allow-Headers` 标头的值是服务器允许的 HTTP 标头的逗号分隔列表。

## CORS 和安全性

CORS 是一种安全机制，可用于保护您的 API 免受恶意请求的侵害。通过启用 CORS，您可以指定允许哪些源向您的 API 发出跨源请求。

## 结论

在本文中，我们介绍了 CORS 是什么、它如何工作以及为什么它很重要。我们还展示了如何在您的服务器上启用 CORS。