---
title: Reverse Proxy for Improved Performance
description: 
published: true
date: 2023-02-14T23:17:22.628Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:17:14.912Z
---

- [Proxy inverso para mejorar el rendimiento***Spanish** document is available*](/es/Knowledge-base/Backend/reverse-proxy-for-improved-performance)
{.links-list}
- [用于提高性能的反向代理***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/reverse-proxy-for-improved-performance)
{.links-list}
- [성능 향상을 위한 리버스 프록시***Korean** document is available*](/ko/Knowledge-base/Backend/reverse-proxy-for-improved-performance)
{.links-list}


# Reverse Proxy for Improved Performance

Web proxy servers act as intermediaries between clients and other servers. A client connects to the proxy server, requesting some service, such as a file, connection, web page, or other resource, available from a different server. The proxy server evaluates the request according to its filtering rules. For example, it may check whether the requested site is blocked in the user's country. If the proxy server approves the request, it connects to the requested site, downloads the page and stores it in its own cache. When the user requests the same page again, the proxy server returns the cached page, which reduces server load and improves response time. 

A reverse proxy is a type of proxy server that retrieves resources on behalf of a client from one or more servers. A reverse proxy accepts requests from one or more clients and forwards them to the appropriate backend server. A reverse proxy can distribute the load from a single client to multiple servers, improving performance.

There are a number of reasons to use a reverse proxy:

* **Performance**: By caching static content and handling dynamic requests separately, a reverse proxy can improve the performance of a web server.

* **Security**: A reverse proxy can offer an additional layer of security by filtering requests and blocking malicious ones.

* **Compatibility**: A reverse proxy can mediate between different backend servers that use different technologies, making them appear to use a single, unified technology.

## Setting up a Reverse Proxy

There are a number of software packages that can be used to set up a reverse proxy. In this section, we will use the NGINX web server.

 NGINX is a free, open-source, high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server. NGINX is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

First, install NGINX using your package manager. For example, on Debian-based distributions:

```
$ sudo apt-get install nginx
```

Next, create a file in NGINX's configuration directory, `/etc/nginx/conf.d/`, with the following contents:

```
server {
    listen 80;
    server_name example.com;
    location / {
        proxy_pass http://localhost:8080;
    }
}
```

This file configures NGINX to listen on port 80 for requests to `example.com` and to forward those requests to `localhost:8080`.

Finally, start NGINX:

```
$ sudo systemctl start nginx
```

## Conclusion

A reverse proxy can improve the performance of a web server by caching static content and handling dynamic requests separately. A reverse proxy can also offer an additional layer of security by filtering requests and blocking malicious ones.