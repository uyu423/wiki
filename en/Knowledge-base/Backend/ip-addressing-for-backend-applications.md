---
title: IP Addressing for Backend Applications
description: 
published: true
date: 2023-01-31T19:36:40.205Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:36:36.574Z
---

- [백엔드 애플리케이션을 위한 IP 주소 지정***Korean** version of this document is available*](/ko/Knowledge-base/Backend/ip-addressing-for-backend-applications)
{.links-list}
- [バックエンド アプリケーションの IP アドレッシング***Japanese** version of this document is available*](/ja/Knowledge-base/Backend/ip-addressing-for-backend-applications)
{.links-list}
- [后端应用程序的 IP 寻址***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Backend/ip-addressing-for-backend-applications)
{.links-list}


  IP Addressing for Backend Applications

The internet protocol (IP) address is a numerical label assigned to each device connected to a computer network that uses the IP for communication. An IP address serves two main functions: host or network interface identification and location addressing.

The Internet Protocol version 4 (IPv4) is the most common version of the IP address. It consists of four sets of numbers ranging from 0 to 255, separated by periods. For example, an IPv4 address might look like this: 192.168.1.1.

The Internet Protocol version 6 (IPv6) is the most recent version of the IP address. It consists of eight sets of four hexadecimal digits, separated by colons. For example, an IPv6 address might look like this: 2001:0db8:85a3:0000:0000:8a2e:0370:7334.

IP addresses are assigned to devices by a network administrator. For example, the administrator of a company's network might assign the IP address 192.168.1.1 to the company's router and reserve the addresses 192.168.1.2 through 192.168.1.254 for use by computers on the network.

When configuring a computer's network settings, the administrator must specify the IP address of the computer's default gateway, which is typically the router. The administrator must also specify the computer's subnet mask.

The subnet mask is a 32-bit number that determines which portion of the IP address identifies the network and which portion identifies the individual devices on the network. For example, the subnet mask 255.255.255.0 indicates that the first three octets of the IP address identify the network and the fourth octet identifies the individual devices on the network.

When sending data over the internet, the data is divided into small packets. Each packet contains the sender's IP address, the receiver's IP address, and other information.

The sender's IP address is used to route the packet to the receiver's IP address. The receiver's IP address is used to deliver the packet to the correct computer on the network.

The process of routing packets from one computer to another is known as packet forwarding. Packet forwarding is performed by devices on the network, such as routers.

Routers maintain a table of IP addresses and their corresponding next-hop router. When a router receives a packet, it looks up the receiver's IP address in its table and forwards the packet to the next-hop router.

This process continues until the packet reaches its destination.

The internet is a network of networks. When you connect to the internet, your computer is assigned an IP address by your ISP.

Your ISP then routes packets to and from your computer through the internet.

The internet is made up of many different types of networks, including:

- Local area networks (LANs)
- Wireless LANs (WLANs)
- Metropolitan area networks (MANs)
- Wide area networks (WANs)

The most common type of LAN is the home network. A home network typically consists of a router connected to a modem. The router is connected to the computers on the network.

A WLAN is a LAN that uses wireless technology to connect devices. WLANs are commonly used in homes and businesses.

A MAN is a network that spans a city. MANs are typically used by ISPs to connect to their customers.

A WAN is a network that spans a large geographic area, such as a country or continent. WANs are used to connect LANs and MANs.

The internet is a global network of computers that use the IP to communicate with each other.

When you connect to the internet, your computer is assigned an IP address by your ISP. Your ISP then routes packets to and from your computer through the internet.

The internet is made up of many different types of networks, including:

- Local area networks (LANs)
- Wireless LANs (WLANs)
- Metropolitan area networks (MANs)
- Wide area networks (WANs)

The most common type of LAN is the home network. A home network typically consists of a router connected to a modem. The router is connected to the computers on the network.

A WLAN is a LAN that uses wireless technology to connect devices. WLANs are commonly used in homes and businesses.

A MAN is a network that spans a city. MANs are typically used by ISPs to connect to their customers.

A WAN is a network that spans a large geographic area, such as a country or continent. WANs are used to connect LANs and MANs.

The internet is a global network of computers that use the IP to communicate with each other.