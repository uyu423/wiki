---
title: Networking Fundamentals for Backend Developers
description: 
published: true
date: 2023-02-18T18:06:24.229Z
tags: 
editor: markdown
dateCreated: 2023-02-18T18:06:22.884Z
---

- [백엔드 개발자를 위한 네트워킹 기초***Korean** document is available*](/ko/Knowledge-base/Backend/networking-fundamentals-for-backend-developers)
{.links-list}


# Networking Fundamentals for Backend Developers

Developing backend applications usually comes with the responsibility of setting up and maintaining a server. While there are many different options and tools for doing this, understanding the basics of networking is essential for any backend developer. In this article, we will cover the basics of networking that every backend developer should know.

## IP Addresses

An IP address is a unique identifier that is assigned to each device on a network. IP addresses are typically in the format ```xxx.xxx.xxx.xxx```, where each ```x``` is a number between 0 and 255.

There are two types of IP addresses that are commonly used: public and private. Public IP addresses are used to identify devices on the internet, while private IP addresses are used to identify devices on a private network, such as a home or office network.

## Subnetting

Subnetting is the process of dividing a network into smaller subnets. This is usually done to improve network performance or to increase security.

When subnetting a network, the network is divided into two or more subnets, each with its own unique IP address range. For example, if a network has the IP address range ```192.168.1.0 - 192.168.1.255```, it can be divided into two subnets: ```192.168.1.0 - 192.168.1.127``` and ```192.168.1.128 - 192.168.1.255```.

## Ports

Ports are used to identify which application is using which network connection. When a device connects to a network, it is assigned a port number. This port number is used to identify which application on the device is using the connection.

For example, when you connect to a website, your computer sends a request to the server using the HTTP protocol. The server then responds to the request using the same HTTP protocol. The port number for the HTTP protocol is ```80```.

## Protocols

A protocol is a set of rules that govern how devices communicate with each other on a network. There are many different protocols, but some of the most common are TCP, UDP, and HTTP.

TCP (Transmission Control Protocol) is a protocol that is used for reliable, error-free communication between devices. UDP (User Datagram Protocol) is a protocol that is used for communication that does not require reliability or error-free delivery. HTTP (Hypertext Transfer Protocol) is a protocol that is used for communication between web browsers and web servers.

## DNS

DNS (Domain Name System) is a system that is used to convert human-readable domain names (like www.example.com) into IP addresses. When you type a domain name into your web browser, DNS is used to look up the IP address of the server that hosts the website.

## Conclusion

These are just the basics of networking. To learn more, check out these great resources:

- [How do I get started with networking?](https://www.lifewire.com/networking-4135484)
- [TCP/IP guide](https://www.tcpipguide.com/)
- [DNS guide](https://www.dnswatch.com/resources/dns-tutorial)