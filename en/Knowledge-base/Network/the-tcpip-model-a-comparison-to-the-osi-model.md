---
title: The TCP/IP Model: A Comparison to the OSI Model
description: 
published: true
date: 2023-03-11T02:32:43.455Z
tags: 
editor: markdown
dateCreated: 2023-03-11T02:32:43.455Z
---

- [TCP/IP 모델: OSI 모델과의 비교***Korean** document is available*](/ko/Knowledge-base/Network/the-tcpip-model-a-comparison-to-the-osi-model)
{.links-list}

## Introduction

When it comes to understanding computer networking, one of the most fundamental models that we need to learn is the OSI model. This model has been used for decades and has helped engineers to design and troubleshoot networks. However, in the 1980s, a new model called the TCP/IP model was introduced. In this article, we'll take a closer look at the TCP/IP model, what it is, and how it compares to the OSI model.

## What is the TCP/IP Model?

The TCP/IP model is a networking model that defines how data is transmitted over a network. The model was developed by the Department of Defense (DoD) in the 1970s to create a network that could survive a nuclear attack. The TCP/IP model is based on four layers: the application layer, the transport layer, the Internet layer, and the network access layer.

### Application Layer

The application layer is the layer closest to the end-user. It defines how applications communicate with each other over a network. This layer includes protocols such as HTTP, FTP, SMTP, and Telnet. These protocols define how data is formatted, transmitted, and received by applications.

### Transport Layer

The transport layer is responsible for ensuring that data is delivered reliably and accurately between applications. This layer includes protocols such as TCP and UDP. TCP is used when reliability is important, while UDP is used when speed is important.

### Internet Layer

The Internet layer is responsible for routing data between networks. This layer includes the Internet Protocol (IP), which defines how data is sent from one network to another. Other protocols that operate at this layer include Internet Control Message Protocol (ICMP) and Internet Group Management Protocol (IGMP).

### Network Access Layer

The network access layer is responsible for transmitting data between the network and the physical medium. This layer includes protocols such as Ethernet, Wi-Fi, Token Ring, and FDDI.

## How Does the TCP/IP Model Compare to the OSI Model?

The TCP/IP model and the OSI model are two of the most well-known networking models. While they share some similarities, there are also several key differences between the two models.

### Layers

One of the biggest differences between the TCP/IP model and the OSI model is the number of layers. The TCP/IP model has four layers, while the OSI model has seven layers. The TCP/IP model combines the presentation, session, and application layers into a single application layer. The transport, internet, and network access layers in the TCP/IP model are equivalent to the transport, network, and data link layers in the OSI model.

### Protocols

Another difference between the TCP/IP model and the OSI model is the protocols used at each layer. While the TCP/IP model has fewer layers, it also has fewer protocols. The OSI model has more protocols, which can make it more complex to implement. The TCP/IP model uses protocols such as TCP, IP, and HTTP, while the OSI model uses protocols such as FTP, SMTP, and SNMP.

### Real-World Example

To understand how the TCP/IP model works in the real world, let's look at an example of a web request. When a user types a URL into their web browser, the browser sends an HTTP request to the web server. The request is transmitted through the application layer and the transport layer, using the HTTP and TCP protocols. The request is then transmitted through the internet layer, using the IP protocol, and finally through the network access layer, using the Ethernet or Wi-Fi protocol.

## Conclusion

The TCP/IP model is a networking model that defines how data is transmitted over a network. While it has some similarities to the OSI model, it has several key differences. Understanding the TCP/IP model is essential for anyone working in IT development, as it provides a framework for designing and troubleshooting networks. By understanding how data is transmitted between layers, you can optimize network performance and ensure that your applications are communicating effectively.

## External Resources

- [TCP/IP Model vs OSI Model](https://www.guru99.com/tcp-ip-model-vs-osi-model.html)
- [TCP/IP Model](https://www.geeksforgeeks.org/tcp-ip-model/)
- [OSI Model](https://www.cisco.com/c/en/us/about/press/internet-protocol-journal/back-issues/table-contents-58/135-models.html)