---
title: Linux Sockets and Network Programming
description: 
published: true
date: 2023-02-12T00:32:20.497Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:32:18.744Z
---

- [Linux Sockets y Programación de Redes***Spanish** document is available*](/es/Knowledge-base/Linux/linux-sockets-and-network-programming)
{.links-list}
- [Linux套接字和网络编程***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-sockets-and-network-programming)
{.links-list}
- [Linux 소켓 및 네트워크 프로그래밍***Korean** document is available*](/ko/Knowledge-base/Linux/linux-sockets-and-network-programming)
{.links-list}


# Linux Sockets and Network Programming

In this article, we'll be discussing Linux sockets and network programming. We'll cover what they are, how they work, and some common use cases. We'll also provide some code examples in C to illustrate how to use them.

## What are sockets?

In computer networking, a socket is an endpoint of a bidirectional or unidirectional data communication channel. Sockets can be used to establish a connection between two computers, which can then be used to exchange data.

Sockets can be either stream-oriented or datagram-oriented. Stream-oriented sockets provide a reliable, ordered, and error-checked connection between two computers. Datagram-oriented sockets, on the other hand, are connectionless and do not guarantee that the data will be delivered in the same order that it was sent.

## How do they work?

Sockets work by creating a socket object on one computer, which is bound to a port number. This socket object can then be used to connect to a socket on another computer, which is also bound to a port number. Once a connection is established, data can be exchanged between the two computers.

## Common use cases

There are many reasons why you might want to use sockets in your applications. Some common use cases include:

- Creating a chat application
- Creating a multiplayer game
- Sending data from one computer to another
- Creating a web server

## Code examples

Here are some code examples in C to illustrate how to use sockets.

### Creating a socket

To create a socket, you need to use the `socket()` function. This function takes three arguments:

- The address family of the socket (e.g. `AF_INET` for IPv4 or `AF_INET6` for IPv6)
- The type of the socket (e.g. `SOCK_STREAM` for a stream-oriented socket or `SOCK_DGRAM` for a datagram-oriented socket)
- The protocol of the socket (e.g. `IPPROTO_TCP` for TCP or `IPPROTO_UDP` for UDP)

```c
int sockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
```

### Connecting to a socket

To connect to a socket, you need to use the `connect()` function. This function takes three arguments:

- The socket file descriptor
- The address of the socket to connect to (cast to a `struct sockaddr *`)
- The size of the address

```c
struct sockaddr_in addr;
addr.sin_family = AF_INET;
addr.sin_port = htons(80);
addr.sin_addr.s_addr = inet_addr("127.0.0.1");

connect(sockfd, (struct sockaddr *)&addr, sizeof(addr));
```

### Sending data

To send data, you need to use the `send()` function. This function takes three arguments:

- The socket file descriptor
- The data to send (cast to a `void *`)
- The size of the data

```c
char buf[1024];

send(sockfd, buf, sizeof(buf), 0);
```

### Receiving data

To receive data, you need to use the `recv()` function. This function takes four arguments:

- The socket file descriptor
- The buffer to store the data in (cast to a `void *`)
- The size of the buffer
- The flags (e.g. `MSG_WAITALL` to wait for all the data to arrive)

```c
char buf[1024];

recv(sockfd, buf, sizeof(buf), MSG_WAITALL);
```

## Closing a socket

To close a socket, you need to use the `close()` function. This function takes a single argument:

- The socket file descriptor

```c
close(sockfd);
```

## External resources

- [ Beej's Guide to Network Programming](https://beej.us/guide/bgnet/)
- [Linux Socket Programming by Example](https://www.amazon.com/Linux-Socket-Programming-Example-Addison-Wesley/dp/0321524713)
- [The Linux Socket Programming Book](https://www.amazon.com/Linux-Socket-Programming-Mark-Twain/dp/188477749X)