---
title: The TCP Three-Way Handshake: How TCP Connections Are Established
description: 
published: true
date: 2023-03-06T11:32:40.441Z
tags: 
editor: markdown
dateCreated: 2023-03-06T11:32:33.136Z
---

- [TCP 3방향 핸드셰이크: TCP 연결 설정 방법***Korean** document is available*](/ko/Knowledge-base/Network/the-tcp-three-way-handshake-how-tcp-connections-are-established)
{.links-list}

# The TCP Three-Way Handshake: How TCP Connections Are Established

Transmission Control Protocol (TCP) is the most widely used protocol in the Internet Protocol (IP) infrastructure. TCP is a reliable, connection-oriented protocol that provides end-to-end communication between applications running on different hosts. A TCP connection is established using a process called the three-way handshake. 

## What Is a TCP Connection?
A TCP connection is a logical connection established between two hosts over a network. The connection provides a reliable, ordered, byte-stream communication channel between the two hosts. 

TCP connections are established using a three-way handshake, which is a process of exchanging three packets between the two hosts to establish the connection. 

## Understanding the TCP Three-Way Handshake
The three-way handshake is a process of exchanging three packets between the two hosts to establish a TCP connection. 

1. In the first step of the handshake, the client sends a SYN (synchronize) packet to the server. The SYN packet contains a random sequence number and the TCP flags set to SYN. 

2. In the second step of the handshake, the server responds with a SYN-ACK (synchronize-acknowledge) packet. The SYN-ACK packet contains an acknowledgement number that is one greater than the sequence number received from the client, a random sequence number, and the TCP flags set to SYN and ACK.

3. In the third step of the handshake, the client responds with an ACK (acknowledge) packet. The ACK packet contains an acknowledgement number that is one greater than the sequence number received from the server, and the TCP flags set to ACK.

Once the three-way handshake is complete, a TCP connection is established between the client and the server, and data can be transferred between the two hosts.

## TCP Three-Way Handshake Code Example
Here is an example of the TCP three-way handshake using Python:

```python
import socket

# create a socket object
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# set the server address and port
server_address = ('localhost', 8888)

# connect to the server
client_socket.connect(server_address)

# send the SYN packet
client_socket.send(b'\x00\x01\x00\x00\x00\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')

# receive the SYN-ACK packet
syn_ack_packet = client_socket.recv(1024)

# send the ACK packet
client_socket.send(b'\x00\x01\x00\x00\x00\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x01')

# the connection is now established
```

## Conclusion
The TCP three-way handshake is a process of exchanging three packets between the two hosts to establish a TCP connection. Understanding how the three-way handshake works is essential for IT development, as TCP is the most widely used protocol in the IP infrastructure. 

## External Resources
- [TCP Three-Way Handshake](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/)
- [TCP/IP Protocol Architecture Model](https://www.networkworld.com/article/3250475/tcp-ip-protocol-architecture-model.html) 
- [Transmission Control Protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)