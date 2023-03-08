---
title: The TCP Maximum Segment Size: How to Optimize TCP Performance
description: 
published: true
date: 2023-03-07T12:33:13.458Z
tags: 
editor: markdown
dateCreated: 2023-03-07T12:33:05.656Z
---

- [TCP 최대 세그먼트 크기: TCP 성능을 최적화하는 방법***Korean** document is available*](/ko/Knowledge-base/Network/the-tcp-maximum-segment-size-how-to-optimize-tcp-performance)
{.links-list}

The TCP Maximum Segment Size: How to Optimize TCP Performance

The Transmission Control Protocol (TCP) is one of the core protocols of the Internet Protocol (IP) suite. It provides reliable, ordered, and error-checked delivery of data between applications running on hosts. However, TCP performance can be affected by various factors, including the maximum segment size (MSS). In this article, we will discuss the TCP MSS and how it can be optimized to improve TCP performance.

## What is the TCP Maximum Segment Size?

The TCP MSS is the largest amount of data that a host is willing to accept in a single TCP segment. A TCP segment is a unit of data exchanged between hosts over a TCP connection. It consists of a header and a payload. The header contains control information, such as sequence numbers and flags, while the payload contains the actual data being sent.

The TCP MSS is negotiated during the TCP three-way handshake, which is the process of establishing a TCP connection between two hosts. The client sends a SYN (synchronize) segment to the server, which includes the MSS value that the client is willing to accept. The server responds with a SYN-ACK (synchronize-acknowledge) segment that includes the MSS value that the server is willing to accept. The client acknowledges the server's response with an ACK (acknowledge) segment.

The default TCP MSS value is typically set to 1460 bytes, which is the maximum data size that can be transmitted in a single IP packet on most networks. However, the actual TCP MSS can be smaller if the network path includes devices, such as routers or firewalls, that limit the maximum packet size.

## Why is the TCP Maximum Segment Size Important?

The TCP MSS can affect TCP performance in several ways. First, a smaller MSS can increase the number of TCP segments required to transmit a given amount of data, which can increase the overhead of the TCP protocol. Second, a smaller MSS can increase the likelihood of TCP fragmentation, which is the process of dividing a large TCP segment into smaller IP fragments to fit within the maximum transmission unit (MTU) of a network. Fragmentation can increase network latency and reduce TCP performance, especially on networks with high error rates.

On the other hand, a larger MSS can improve TCP performance by reducing the overhead of the TCP protocol and minimizing the likelihood of TCP fragmentation. However, a larger MSS can also increase the likelihood of packet loss, especially on networks with high error rates. This is because a larger TCP segment has a higher probability of containing a corrupt or lost packet.

## How to Optimize the TCP Maximum Segment Size?

The optimal TCP MSS value depends on several factors, including the network path, the application requirements, and the host resources. In general, the TCP MSS should be set to the largest value that does not result in TCP fragmentation or excessive packet loss.

### 1. Determine the Path MTU

The Path MTU is the maximum size of an IP packet that can be transmitted without fragmentation on a given network path. It depends on the MTU of each network link along the path, as well as any devices, such as routers or firewalls, that limit the maximum packet size. To determine the Path MTU, you can use the "traceroute" or "ping" command with the "dont-fragment" flag to probe the network path with different packet sizes.

```{language} {code}
$ traceroute -n -M do -p 80 example.com
```

```{language} {code}
$ ping -c 1 -D -s 1500 example.com
```

Once you determine the Path MTU, you can subtract the IP header size (typically 20 bytes) and the TCP header size (typically 20 bytes) to obtain the maximum TCP payload size.

### 2. Set the TCP MSS

To set the TCP MSS, you can use the "ip tcp adjust-mss" command on a network device, such as a router or a firewall, that is located along the network path. This command adjusts the MSS value in the TCP SYN segments that pass through the device, based on the Path MTU.

```{language} {code}
R1(config)# interface GigabitEthernet0/0
R1(config-if)# ip tcp adjust-mss 1400
```

Alternatively, you can set the TCP MSS on the hosts themselves, using the "iptables" or "ipfw" firewall rules on Linux or macOS hosts, or the "netsh" command on Windows hosts.

```{language} {code}
$ sudo iptables -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1400
```

```{language} {code}
$ sudo ipfw add pipe 1 tcp from any to any setup via en0 tcpflags syn mss 1400
```

```{language} {code}
C:\> netsh interface ipv4 set subinterface "Local Area Connection" mtu=1400 store=persistent
```

### 3. Test the TCP Performance

After setting the TCP MSS, you should test the TCP performance to ensure that it meets the application requirements. You can use tools, such as "iperf" or "ttcp", to measure the TCP throughput and latency between the hosts.

```{language} {code}
$ iperf -s
```

```{language} {code}
$ iperf -c 192.168.1.1 -M 1400
```

```{language} {code}
$ ttcp -r
```

```{language} {code}
$ ttcp -t 192.168.1.1 -m 1400
```

If the TCP performance does not meet the application requirements, you can adjust the TCP MSS value and repeat the testing until you achieve the optimal TCP performance.

## Conclusion

The TCP MSS is an important parameter that can affect TCP performance. By setting the TCP MSS to the optimal value, you can improve the efficiency and reliability of TCP communications. However, the optimal TCP MSS depends on various factors, and it may require testing and adjustment to achieve the best results. By following the guidelines in this article, you can optimize the TCP MSS and enhance the performance of your applications.

## External Resources

- [RFC 879 - The TCP Maximum Segment Size and Related Topics](https://tools.ietf.org/html/rfc879)
- [RFC 1191 - Path MTU Discovery](https://tools.ietf.org/html/rfc1191)
- [TCP Maximum Segment Size (MSS) Management](https://www.cisco.com/c/en/us/support/docs/ip/generic-routing-encapsulation-gre/25885-pmtud-ipfrag.html)
- [TCP Performance Tuning Tips](https://docs.oracle.com/cd/E19455-01/806-1075/6j9vh8m4u/index.html)