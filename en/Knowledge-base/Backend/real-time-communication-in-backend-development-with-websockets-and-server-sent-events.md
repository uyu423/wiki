---
title: Real-time Communication in Backend Development with WebSockets and Server-Sent Events
description: 
published: true
date: 2023-02-17T18:03:08.253Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:32:30.959Z
---

- [WebSocket 및 서버 전송 이벤트를 사용한 백엔드 개발의 실시간 통신***Korean** version of this document is available*](/ko/Knowledge-base/Backend/real-time-communication-in-backend-development-with-websockets-and-server-sent-events)
{.links-list}
- [WebSocket とサーバー送信イベントを使用したバックエンド開発でのリアルタイム通信***Japanese** version of this document is available*](/ja/Knowledge-base/Backend/real-time-communication-in-backend-development-with-websockets-and-server-sent-events)
{.links-list}
- [使用 WebSockets 和服务器发送的事件在后端开发中进行实时通信***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Backend/real-time-communication-in-backend-development-with-websockets-and-server-sent-events)
{.links-list}


# Real-time Communication in Backend Development with WebSockets and Server-Sent Events

In this article, we'll be discussing how to add real-time communication capabilities to your backend applications using two different technologies: WebSockets and Server-Sent Events. We'll go over the basics of each technology and when you might want to use one over the other. Finally, we'll provide some code snippets to get you started.

## WebSockets

WebSockets are a way to keep a connection open between a client and a server so that data can flow back and forth between them in real-time. Once a connection is established, it stays open until one of the parties decides to close it. This makes WebSockets well-suited for applications that need constant communication, such as chat applications or multi-player games.

WebSockets use a protocol that is very similar to HTTP, so they can be used with any library or framework that supports HTTP. To establish a connection, the client sends a request to the server with specific headers that indicate they want to use the WebSocket protocol. The server then responds with its own headers, and the connection is established. After that, any data sent from the client to the server or vice versa goes through the established connection.

One advantage of using WebSockets is that they can be used with multiplexing. This means that a single connection can be used to send and receive data for multiple purposes at the same time. This can be useful if you want to keep the connection open for a long time and don't want to have to establish a new connection every time you need to send or receive data.

Another advantage is that, because the connection is persistent, it can be used to send data at any time, without having to wait for a response from the server. This can be useful for applications that need to send data in real-time, such as chat applications or multiplayer games.

## Server-Sent Events

Server-Sent Events (SSE) is a technology for sending events from a server to a client in real-time. Unlike WebSockets, SSE uses a one-way communication channel from the server to the client. This means that the client can only receive data from the server, and not send data back to the server.

SSE is designed to be used with server-side push notifications. This means that the server can send data to the client even if the client is not actively requesting data. This makes SSE well-suited for applications that need to receive data in real-time, but don't need to send data back to the server, such as stock tickers or sports scores.

SSE is a part of the HTML5 standard, so it can be used with any library or framework that supports HTML5. To establish a connection, the client sends a request to the server with specific headers that indicate they want to use the SSE protocol. The server then responds with its own headers, and the connection is established. After that, any data sent from the server to the client goes through the established connection.

One advantage of using SSE is that it is a part of the HTML5 standard, so it is well-supported by browsers. Another advantage is that, because the connection is persistent, it can be used to send data at any time, without having to wait for a response from the client. This can be useful for applications that need to send data in real-time, such as stock tickers or sports scores.

## When to Use WebSockets or Server-Sent Events

In general, you should use WebSockets if you need two-way communication between the client and server, and you should use SSE if you only need one-way communication from the server to the client.

### WebSockets

- Two-way communication
- Multiplexing
- Can be used with any library or framework that supports HTTP

### Server-Sent Events

- One-way communication
- Part of the HTML5 standard
- Can be used with any library or framework that supports HTML5