---
title: 用于提高性能的反向代理
description: 
published: true
date: 2023-02-14T23:17:17.191Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:17:14.907Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Reverse Proxy for Improved Performance***English** document is available*](/en/Knowledge-base/Backend/reverse-proxy-for-improved-performance)
{.links-list}


# 反向代理以提高性能

Web 代理服务器充当客户端和其他服务器之间的中介。客户端连接到代理服务器，请求来自不同服务器的某些服务，例如文件、连接、网页或其他资源。代理服务器根据其过滤规则评估请求。例如，它可能会检查所请求的站点在用户所在的国家/地区是否被阻止。如果代理服务器批准请求，它会连接到请求的站点，下载页面并将其存储在自己的缓存中。当用户再次请求同一个页面时，代理服务器返回缓存的页面，从而减少服务器负载并提高响应时间。

反向代理是一种代理服务器，它代表客户端从一个或多个服务器检索资源。反向代理接受来自一个或多个客户端的请求并将它们转发到适当的后端服务器。反向代理可以将负载从单个客户端分配到多个服务器，从而提高性能。

使用反向代理的原因有很多：

* **性能**：通过缓存静态内容和分别处理动态请求，反向代理可以提高 Web 服务器的性能。

* **安全性**：反向代理可以通过过滤请求和阻止恶意请求来提供额外的安全层。

* **兼容性**：反向代理可以在使用不同技术的不同后端服务器之间进行调解，使它们看起来使用单一、统一的技术。

## 设置反向代理

有许多软件包可用于设置反向代理。在本节中，我们将使用 NGINX Web 服务器。

 NGINX 是一个免费、开源、高性能的 HTTP 服务器和反向代理，以及一个 IMAP/POP3 代理服务器。 NGINX 以其高性能、稳定、丰富的功能集、简单的配置和低资源消耗而闻名。

首先，使用包管理器安装 NGINX。例如，在基于 Debian 的发行版上：

```
$ sudo apt-get install nginx
```

接下来，在 NGINX 的配置目录中创建一个文件，`/etc/nginx/conf.d/`，内容如下：

```
server {
    listen 80;
    server_name example.com;
    location / {
        proxy_pass http://localhost:8080;
    }
}
```

此文件将 NGINX 配置为在端口 80 上侦听对“example.com”的请求，并将这些请求转发到“localhost:8080”。

最后，启动 NGINX：

```
$ sudo systemctl start nginx
```

## 结论

反向代理可以通过缓存静态内容和分别处理动态请求来提高 Web 服务器的性能。反向代理还可以通过过滤请求和阻止恶意请求来提供额外的安全层。