---
title: IP Subnetting: How to Divide IP Networks into Smaller Subnets
description: 
published: true
date: 2023-03-06T02:32:49.904Z
tags: 
editor: markdown
dateCreated: 2023-03-06T02:32:42.709Z
---

- [IP 서브넷팅: IP 네트워크를 더 작은 서브넷으로 나누는 방법***Korean** document is available*](/ko/Knowledge-base/Network/ip-subnetting-how-to-divide-ip-networks-into-smaller-subnets)
{.links-list}

IP Subnetting: How to Divide IP Networks into Smaller Subnets

As networks continue to expand, it becomes necessary to segment them, and IP subnetting provides a way to do so. Subnetting is the process of dividing a larger IP network into smaller subnetworks, each with its own unique IP address range.

In this article, we will explore the basics of IP subnetting, including why it is important, how to calculate CIDR notation, and how to subnet IP addresses. We will also provide practical examples using code snippets in different programming languages.

Why is IP Subnetting Important?

Subnetting provides several benefits, including:

- Improved network performance: With subnetting, network traffic can be distributed more efficiently, reducing congestion and improving performance.
- Network security: Subnets can be used to isolate sensitive parts of the network, reducing the risk of unauthorized access or attacks.
- IP address conservation: Subnetting allows for more efficient use of IP addresses, reducing the need for frequent address assignments.

Understanding CIDR Notation

CIDR (Classless Inter-Domain Routing) notation is a way of representing IP addresses and subnet masks. It consists of an IP address followed by a slash (/) and a number between 0 and 32, representing the number of bits in the subnet mask.

For example, the CIDR notation for a network with an IP address of 192.168.1.0 and a subnet mask of 255.255.255.0 would be 192.168.1.0/24. The /24 indicates that the first 24 bits of the IP address are used for the network, and the remaining 8 bits are used for hosts.

Calculating CIDR Notation

To calculate CIDR notation, you need to determine the number of bits in the subnet mask. The easiest way to do this is to convert the subnet mask to binary form and count the number of 1s.

For example, the subnet mask 255.255.255.0 can be converted to binary form as follows:

```
11111111 11111111 11111111 00000000
```

Counting the number of 1s, we get 24, so the CIDR notation for this subnet mask is /24.

Subnetting IP Addresses

To subnet an IP address, you need to borrow bits from the host portion of the IP address and use them for the network portion. This increases the number of available networks but reduces the number of available hosts per network.

For example, suppose you have the IP address 192.168.1.0/24 and want to create four subnets. To do this, you need to borrow two bits from the host portion of the IP address, giving you six bits for the network portion.

```
Original IP address: 192.168.1.0/24
Subnet mask: 255.255.255.0
```

The binary form of the subnet mask is:

```
11111111 11111111 11111111 00000000
```

To borrow two bits, we change the subnet mask to:

```
11111111 11111111 11111100 00000000
```

This gives us four subnets, with the following ranges:

```
192.168.0.0/26
192.168.0.64/26
192.168.0.128/26
192.168.0.192/26
```

Each subnet can accommodate up to 62 hosts, with the first and last addresses reserved for the network and broadcast addresses, respectively.

Code Examples

Here are some examples of how to subnet IP addresses in different programming languages:

### Python

```python
import ipaddress

network = ipaddress.ip_network('192.168.1.0/24')
subnets = list(network.subnets(prefixlen_diff=2))

for subnet in subnets:
    print(subnet)
```

### Java

```java
import java.net.InetAddress;
import java.net.UnknownHostException;

public class SubnettingExample {
    public static void main(String[] args) throws UnknownHostException {
        InetAddress ip = InetAddress.getByName("192.168.1.0");
        byte[] octets = ip.getAddress();
        int subnetBits = 2;
        int hostBits = 8 * octets.length - subnetBits;
        byte[] subnetMask = new byte[octets.length];

        for (int i = 0; i < octets.length; i++) {
            int bits = Math.min(8, hostBits);
            int mask = (bits == 8) ? 0xFF : (0xFF << (8 - bits));
            subnetMask[i] = (byte) mask;
            hostBits -= bits;
        }

        InetAddress subnet = InetAddress.getByAddress(octets);
        for (int i = 0; i < (1 << subnetBits); i++) {
            subnetMask[octets.length - 1] |= i;
            InetAddress address = InetAddress.getByAddress(subnetMask);
            System.out.println(address);
        }
    }
}
```

### Ruby

```ruby
require 'ipaddr'

network = IPAddr.new('192.168.1.0/24')
subnets = network.subnet(2)

subnets.each do |subnet|
  puts subnet.to_s
end
```

Conclusion

In this article, we have explored the basics of IP subnetting, including why it is important, how to calculate CIDR notation, and how to subnet IP addresses. We have also provided practical examples using code snippets in different programming languages.

By subnetting, you can improve network performance, enhance network security, and conserve IP address space. It is an essential skill for any IT professional, and we hope this article has provided a solid foundation for you to build on.

External Resources

- Subnetting Practice: https://subnettingpractice.com/
- IP Subnet Calculator: https://www.calculator.net/ip-subnet-calculator.html
- Understanding IP Addressing and CIDR Charts: https://www.cisco.com/c/en/us/support/docs/ip/subnet-mask-lengths/8073-subnetting-made-easy.html