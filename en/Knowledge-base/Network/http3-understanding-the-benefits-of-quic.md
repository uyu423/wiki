---
title: HTTP/3: Understanding the Benefits of QUIC
description: 
published: true
date: 2023-03-03T03:32:27.965Z
tags: 
editor: markdown
dateCreated: 2023-03-03T03:32:20.512Z
---

- [HTTP/3: QUIC의 이점 이해***Korean** document is available*](/ko/Knowledge-base/Network/http3-understanding-the-benefits-of-quic)
{.links-list}
HTTP/3: Understanding the Benefits of QUIC

HTTP (Hypertext Transfer Protocol) is the primary protocol used to transfer data over the internet. The current version of HTTP, HTTP/2, was introduced in 2015 and brought significant improvements in performance over its predecessor, HTTP/1.1. However, the Internet Engineering Task Force (IETF), the organization responsible for managing HTTP, has been working on a new version of the protocol, HTTP/3, which incorporates a new transport protocol called QUIC. 

QUIC (Quick UDP Internet Connections) is a transport layer protocol developed by Google, initially as a way to improve the performance of their Chrome browser. It is now an open standard and has been adopted by other major players, such as Mozilla and Cloudflare. The goal of QUIC is to reduce latency and improve security for internet communications. In this article, we will explore the benefits of QUIC and how they are incorporated into HTTP/3.

## The Need for QUIC

TCP (Transmission Control Protocol) is the transport protocol used by HTTP/1.1 and HTTP/2. It provides a reliable and ordered delivery of data over the internet, but it has some limitations. TCP requires a three-way handshake to establish a connection, which adds latency to the communication. Also, TCP is susceptible to head-of-line blocking, which means that a packet lost in transit holds up delivery of subsequent packets until it is retransmitted. This can lead to slow page load times and poor user experiences.

UDP (User Datagram Protocol), on the other hand, is a connectionless protocol that does not provide reliability or ordering guarantees. However, it has lower overhead and can be faster than TCP. QUIC is based on UDP but includes improvements to address its limitations. QUIC provides a reliable and ordered delivery of data, like TCP, but without the latency introduced by the three-way handshake. It also uses packet-level error correction to reduce the impact of packet loss and avoid head-of-line blocking.

## Benefits of QUIC

### Faster Page Load Times

QUIC's use of UDP allows for faster connections, reducing latency and improving page load times. QUIC's connection setup uses a zero-round-trip-time handshake, meaning that it does not require a three-way handshake, which can add significant delay to the connection. This makes QUIC particularly advantageous for mobile devices and users with high-latency connections.

### Improved Security

QUIC includes built-in encryption, making it more secure than TCP. Encryption is applied to all data in transit, including the connection setup, headers, and payloads. This reduces the likelihood of man-in-the-middle attacks and eavesdropping.

### Reduced Packet Loss

Packet loss is a common occurrence on the internet, and TCP's reliance on acknowledgment packets can slow down communication when packets are lost. QUIC uses packet-level error correction, which means that it can recover from lost packets more quickly than TCP. This reduces the impact of packet loss on page load times and improves overall performance.

### Multiplexing

QUIC supports multiplexing, which allows for multiple independent streams of data to be sent over a single connection. This means that multiple requests can be sent simultaneously, and responses can be received out-of-order. This can improve page load times by reducing the amount of time it takes to download multiple resources.

## Implementing HTTP/3 with QUIC

HTTP/3 uses QUIC as its underlying transport protocol. The primary difference between HTTP/2 and HTTP/3 is the way that data is transmitted. HTTP/2 uses TCP, which requires a three-way handshake to establish the connection. HTTP/3 uses QUIC, which uses a zero-round-trip-time handshake. This means that HTTP/3 can establish connections more quickly than HTTP/2.

Implementing HTTP/3 with QUIC requires server and client support. Many major web servers, such as NGINX and Apache, already support HTTP/3. Client support is less widespread, but major browsers, such as Chrome and Firefox, have experimental support for HTTP/3.

Here is an example of how to implement an HTTP/3 server using NGINX:

```nginx
http {
  listen 443 quic reuseport;
  listen [::]:443 quic reuseport;

  ssl_certificate /path/to/cert.pem;
  ssl_certificate_key /path/to/key.pem;

  location / {
    root /var/www/html;
  }
}
```

This NGINX configuration sets up an HTTP/3 server on port 443 using QUIC. The `ssl_certificate` and `ssl_certificate_key` directives specify the SSL certificate and key for the server. The `location` directive specifies the location of the server's files.

## Conclusion

QUIC is a new transport protocol developed to improve the performance and security of internet communications. It provides faster connections, improved security, reduced packet loss, and multiplexing. HTTP/3 incorporates QUIC as its underlying transport protocol and offers significant improvements over HTTP/2. Implementing HTTP/3 with QUIC requires server and client support, but major players in the industry are already adopting it. As HTTP continues to evolve, it is important for developers to stay up-to-date with the latest protocols and standards to ensure the best possible user experience for their applications.

## External Resources

- [QUIC Homepage](https://www.chromium.org/quic)
- [HTTP/3 Explained](https://http3-explained.haxx.se/)
- [NGINX HTTP/3 and QUIC](https://www.nginx.com/blog/nginx-1-19-0-released/)
- [Mozilla's Implementation of QUIC](https://blog.mozilla.org/press-uk/2021/07/29/mozilla-partners-with-cloudflare-to-improve-privacy-and-security-on-the-web/)