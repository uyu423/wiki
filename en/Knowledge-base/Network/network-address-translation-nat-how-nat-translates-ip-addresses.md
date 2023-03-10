---
title: Network Address Translation (NAT): How NAT Translates IP Addresses
description: 
published: true
date: 2023-03-10T23:32:48.575Z
tags: 
editor: markdown
dateCreated: 2023-03-10T23:32:48.575Z
---

- [네트워크 주소 변환(NAT): NAT가 IP 주소를 변환하는 방법***Korean** document is available*](/ko/Knowledge-base/Network/network-address-translation-nat-how-nat-translates-ip-addresses)
{.links-list}



Network Address Translation (NAT): How NAT Translates IP Addresses

As the Internet has evolved and grown, the number of devices that need to be connected to the internet has increased exponentially. In order to connect these devices to the internet, they must be assigned an IP address. IPv4 addresses are the most commonly used addresses, and there are only a limited number of these addresses available. Therefore, Network Address Translation (NAT) was developed to allow multiple devices to share a single IP address to connect to the internet. In this article, we will discuss how NAT works and how it translates IP addresses.

## What is NAT?

Network Address Translation (NAT) is a technique used to hide the private IP addresses of devices within a private network from the public IP address of the internet. NAT allows multiple devices on a private network to share a single public IP address assigned by an internet service provider (ISP).

## How NAT Translates IP Addresses

NAT operates by translating the private IP address of a device on a private network to a public IP address that is visible on the internet. When a device on a private network sends a request to access a website or a server on the internet, the NAT device replaces the source IP address of the request with the public IP address assigned by the ISP. 

When the response from the website or server is received by the NAT device, it replaces the destination IP address of the response with the private IP address of the device that originally sent the request. This allows the device on the private network to receive the response from the website or server it was trying to access. 

## Types of NAT

There are three types of NAT: static NAT, dynamic NAT, and port address translation (PAT).

### Static NAT

Static NAT is a one-to-one mapping between a private IP address and public IP address. Static NAT is typically used when a device on a private network needs to have a permanent public IP address. 

An example of static NAT using Cisco IOS commands is shown below:

```{language=cisco}
ip nat inside source static {private IP address} {public IP address}
```

### Dynamic NAT

Dynamic NAT is a many-to-many mapping between private IP addresses and public IP addresses. Dynamic NAT is typically used when there are many devices on a private network that need to access the internet but do not require a permanent public IP address.

An example of dynamic NAT using Cisco IOS commands is shown below:

```{language=cisco}
ip nat pool {pool name} {first public IP address} {last public IP address} netmask {subnet mask}
ip nat inside source list {access list} pool {pool name}
access-list {access list number} permit {private IP address} {subnet mask}
```

### Port Address Translation (PAT)

Port Address Translation (PAT) is a technique that allows multiple devices on a private network to share a single public IP address. PAT operates by translating the source port number of a device on a private network to a different source port number on the public IP address assigned by the ISP.

An example of PAT using Cisco IOS commands is shown below:

```{language=cisco}
interface {interface name}
ip nat inside
!
interface {interface name}
ip nat outside
!
ip nat inside source list {access list} interface {interface name} overload
access-list {access list number} permit {private IP address} {subnet mask}
```

## Benefits of NAT

There are several benefits of using NAT:

- NAT provides an additional layer of security by hiding the private IP addresses of devices on a private network from the public IP address of the internet.
- NAT allows multiple devices to share a single public IP address, which conserves the limited number of public IP addresses available.
- NAT can be used to translate private IP addresses to public IP addresses, allowing devices on a private network to access the internet.

## Drawbacks of NAT

While NAT provides several benefits, there are also some drawbacks to using NAT:

- NAT can cause issues with some applications that require a public IP address, such as video conferencing or online gaming.
- NAT can cause issues with some network protocols that embed IP addresses inside the data payload, such as IPsec or FTP.
- NAT can add additional latency to network traffic, which can negatively impact the performance of real-time applications such as voice over IP (VoIP).

## Conclusion

Network Address Translation (NAT) is a technique used to hide the private IP addresses of devices within a private network from the public IP address of the internet. NAT allows multiple devices on a private network to share a single public IP address assigned by an internet service provider (ISP). There are three types of NAT: static NAT, dynamic NAT, and port address translation (PAT). While NAT provides several benefits, there are also some drawbacks to using NAT. 

## External Resources

- [Network Address Translation (NAT) Explained - Cisco](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/26704-nat-faq-00.html)
- [Network Address Translation (NAT) - GeeksforGeeks](https://www.geeksforgeeks.org/network-address-translation-nat/)
- [NAT Types - TechTarget](https://searchnetworking.techtarget.com/definition/NAT-types-static-NAT-and-dynamic-NAT)