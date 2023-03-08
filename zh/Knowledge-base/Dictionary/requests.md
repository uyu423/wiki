---
title: Requests
description: 
published: true
date: 2023-02-08T02:18:03.145Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:18:00.927Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Requests***English** document is available*](/en/Knowledge-base/Dictionary/requests)
{.links-list}


# 概述

Requests 是一个 Apache2 许可的 HTTP 库，用 Python 编写，供人类使用。 Requests 允许用户轻松地向指定的 URL 发出 HTTP 请求，例如 GET、POST、PUT 和 DELETE。它还支持身份验证、cookie 和其他功能。

# 描述

Requests 是一个流行的 Python 库，用于发出 HTTP 请求。它旨在让开发人员使用起来简单直观，重点是简化 HTTP 请求的过程。 Requests 支持广泛的 HTTP 请求，例如 GET、POST、PUT 和 DELETE。它还提供对身份验证、cookie 和其他功能的支持。

Requests 建立在流行的 urllib3 库之上，它提供了一个用于发出 HTTP 请求的低级接口。 Requests 使用 urllib3 提供更高级的 API 来发出 HTTP 请求，使其更易于使用。

Requests 还提供了许多方便的功能，例如指定要随请求发送的数据的能力，以及指定请求超时的能力。

# 历史

Requests 最初由 Kenneth Reitz 于 2011 年创建。它最初作为开源项目发布在 GitHub 上，并迅速受到开发人员的欢迎。自首次发布以来，Requests 已成为最受欢迎的 Python 库之一，下载量超过 1000 万次。

# 特征

Requests 提供了许多功能，使开发人员可以更轻松地发出 HTTP 请求。

- Requests 支持广泛的 HTTP 请求，包括 GET、POST、PUT 和 DELETE。
- Requests 支持身份验证，允许开发人员轻松地使用 Web 服务进行身份验证。
- Requests支持cookies，让开发者可以轻松处理请求中的cookies。
- Requests 支持数据，允许开发人员轻松指定要随请求发送的数据。
- Requests 支持超时，允许开发人员为请求指定超时时间。

# 例子

以下是使用 Requests 向 Web 服务发出 GET 请求的示例：

```python
import requests

response = requests.get('http://example.com/api/v1/data')

if response.status_code == 200:
    data = response.json()
    print(data)
```

# 优点和缺点

优点：

- 易于使用：Requests 提供了一个简单直观的 API 来发出 HTTP 请求。
- 广泛的请求：Requests 支持广泛的 HTTP 请求，例如 GET、POST、PUT 和 DELETE。
- 身份验证：Requests 支持身份验证，可以更轻松地使用 Web 服务进行身份验证。
- Cookies：Requests支持cookies，方便处理requests中的cookies。
- 数据：请求支持数据，可以更轻松地指定要随请求发送的数据。
- 超时：请求支持超时，可以更轻松地为请求指定超时。

缺点：

- 对非 HTTP 请求的支持有限：Requests 仅支持 HTTP 请求，因此不能用于发出非 HTTP 请求。
- 不支持流式传输：请求不支持流式传输，因此不能用于流式传输数据。

# 争议

由于使用了 urllib3，Requests 一直是一些争议的主题，urllib3 是一个用于发出 HTTP 请求的低级库。一些开发人员认为，由于 urllib3 带来的潜在安全风险，不应在生产中使用 Requests。

# 相关技术

- urllib3：urllib3 是一个用于发出 HTTP 请求的低级库。 Requests 建立在 urllib3 之上。
- Requests-toolbelt：Requests-toolbelt 是一个使用 Requests 进行 HTTP 请求的库。
- Requests-mock：Requests-mock 是一个用 Requests 模拟 HTTP 请求的库。

# 题外话

Requests 是一个流行的库，用于在 Python 中发出 HTTP 请求。它旨在易于使用，并提供广泛的功能，使发出 HTTP 请求变得更加容易。

# 其他的

Requests 是一个开源项目，在 Apache2 许可证下发布。它得到积极维护，并被开发人员广泛使用。