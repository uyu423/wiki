---
title: HTTP/2: Understanding the Improvements Over HTTP/1.x
description: 
published: true
date: 2023-03-12T12:32:58.981Z
tags: 
editor: markdown
dateCreated: 2023-03-12T12:32:58.981Z
---

- [HTTP/2: HTTP/1.x에 대한 개선 사항 이해***Korean** document is available*](/ko/Knowledge-base/Network/http2-understanding-the-improvements-over-http1-x)
{.links-list}

HTTP/2: Understanding the Improvements Over HTTP/1.x

HTTP (Hypertext Transfer Protocol) is the protocol used for communication between a web server and a web client. The protocol defines how messages are formatted and transmitted, as well as the actions a web server and a web client should take in response to various commands. The latest version of the protocol, HTTP/2, was released in 2015, and it has several improvements over HTTP/1.x. In this article, we will explore the differences between the two protocols and why HTTP/2 is an improvement over HTTP/1.x.

## HTTP/1.x

HTTP/1.x is the old version of the protocol, and it has been around since the early days of the internet. It is a simple protocol that uses plain text to transmit messages between a web server and a web client. HTTP/1.x has several limitations, including:

- **Head-of-Line Blocking:** HTTP/1.x uses a single connection to transmit all requests and responses between a web server and a web client. If a request is blocked, all subsequent requests are also blocked until the previous request is completed. This is known as head-of-line blocking and can significantly reduce the performance of a website.

- **No Server Push:** In HTTP/1.x, a web server can only respond to a client's request. There is no way for a server to proactively send data to a client. This means that a client has to make multiple requests to a server to retrieve all the necessary resources to render a webpage.

- **Inefficient Resource Usage:** In HTTP/1.x, a separate connection is created for each request, which can lead to inefficient resource usage.

## HTTP/2

HTTP/2 is the latest version of the protocol and has several improvements over HTTP/1.x. It was designed to address the limitations of HTTP/1.x and improve the performance of websites. Some of the key improvements of HTTP/2 are:

- **Multiplexing:** HTTP/2 uses a single connection to transmit multiple requests and responses between a web server and a web client. This means that requests and responses can be sent and received in parallel, which significantly improves the performance of a website.

- **Server Push:** With HTTP/2, a web server can proactively send resources to a client before the client requests them. This means that a client can receive all the necessary resources to render a webpage in a single request, which improves the performance of a website.

- **Header Compression:** HTTP/2 compresses the headers of messages, which reduces the amount of data that needs to be transmitted between a web server and a web client. This improves the performance of a website, especially on slow connections.

- **Binary Protocol:** HTTP/2 uses a binary protocol instead of plain text, which makes it more efficient and faster than HTTP/1.x.

## How to Use HTTP/2

To use HTTP/2, you need a web server that supports it, such as Apache or Nginx. You also need a web browser that supports it, such as Google Chrome, Mozilla Firefox, or Microsoft Edge. You can check if your website is using HTTP/2 by using a HTTP/2 checker tool.

To enable HTTP/2 on Apache, you need to have mod_http2 installed and enabled. You can do this by running the following commands:

```bash
sudo apt-get install libnghttp2-dev
sudo apt-get install libapache2-mod-http2
sudo a2enmod http2
sudo service apache2 restart
```

To enable HTTP/2 on Nginx, you need to have version 1.9.5 or later installed. You can enable HTTP/2 by adding the following lines to your Nginx configuration file:

```nginx
listen 443 ssl http2;
ssl_protocols TLSv1.2;
```

## Conclusion

HTTP/2 is the latest version of the HTTP protocol and has several significant improvements over HTTP/1.x. It addresses the limitations of HTTP/1.x and improves the performance of websites. By using a single connection to transmit multiple requests and responses, enabling server push, compressing headers, and using a binary protocol, HTTP/2 significantly reduces the latency of a website and improves the user experience. To use HTTP/2, you need a web server and a web browser that support it. So, if you're not already using HTTP/2, it's time to make the switch.

## Further Reading

- [HTTP/2 Specification](https://http2.github.io/)
- [HTTP/2 vs HTTP/1: What’s the Difference?](https://www.cloudflare.com/learning/http2/http1.1-vs-http2/)
- [How to Enable HTTP/2 in Apache](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-with-http-2-support-on-ubuntu-18-04)
- [How to Enable HTTP/2 in Nginx](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-with-http-2-support-on-ubuntu-18-04)