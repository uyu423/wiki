---
title: IP 서브넷팅: IP 네트워크를 더 작은 서브넷으로 나누는 방법
description: 
published: true
date: 2023-03-06T02:32:44.086Z
tags: 
editor: markdown
dateCreated: 2023-03-06T02:32:42.706Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [IP Subnetting: How to Divide IP Networks into Smaller Subnets***English** document is available*](/en/Knowledge-base/Network/ip-subnetting-how-to-divide-ip-networks-into-smaller-subnets)
{.links-list}

IP 서브넷팅: IP 네트워크를 더 작은 서브넷으로 나누는 방법

네트워크가 계속 확장됨에 따라 네트워크를 분할해야 하며 IP 서브넷팅은 이를 위한 방법을 제공합니다. 서브넷팅은 더 큰 IP 네트워크를 각각 고유한 IP 주소 범위를 가진 더 작은 서브네트워크로 나누는 프로세스입니다.

이 기사에서는 중요한 이유, CIDR 표기법 계산 방법 및 IP 주소를 서브넷팅하는 방법을 포함하여 IP 서브넷팅의 기본 사항을 살펴봅니다. 또한 다양한 프로그래밍 언어의 코드 스니펫을 사용하는 실용적인 예를 제공합니다.

IP 서브넷팅이 중요한 이유는 무엇입니까?

서브넷팅은 다음과 같은 여러 이점을 제공합니다.

- 향상된 네트워크 성능: 서브넷을 사용하면 네트워크 트래픽을 보다 효율적으로 분산하여 혼잡을 줄이고 성능을 향상시킬 수 있습니다.
- 네트워크 보안: 서브넷을 사용하여 네트워크의 민감한 부분을 격리하여 무단 액세스 또는 공격의 위험을 줄일 수 있습니다.
- IP 주소 보존: 서브넷팅을 통해 IP 주소를 보다 효율적으로 사용할 수 있으므로 빈번한 주소 할당의 필요성이 줄어듭니다.

CIDR 표기법 이해

CIDR(Classless Inter-Domain Routing) 표기법은 IP 주소와 서브넷 마스크를 나타내는 방법입니다. IP 주소 뒤에 슬래시(/)와 서브넷 마스크의 비트 수를 나타내는 0에서 32 사이의 숫자로 구성됩니다.

예를 들어 IP 주소가 192.168.1.0이고 서브넷 마스크가 255.255.255.0인 네트워크의 CIDR 표기법은 192.168.1.0/24입니다. /24는 IP 주소의 처음 24비트가 네트워크에 사용되고 나머지 8비트는 호스트에 사용됨을 나타냅니다.

CIDR 표기법 계산

CIDR 표기법을 계산하려면 서브넷 마스크의 비트 수를 결정해야 합니다. 이를 수행하는 가장 쉬운 방법은 서브넷 마스크를 이진 형식으로 변환하고 1의 수를 세는 것입니다.

예를 들어 서브넷 마스크 255.255.255.0은 다음과 같이 이진 형식으로 변환할 수 있습니다.

```
11111111 11111111 11111111 00000000
```

1의 수를 세면 24가 되므로 이 서브넷 마스크의 CIDR 표기법은 /24입니다.

서브넷 IP 주소

IP 주소를 서브넷팅하려면 IP 주소의 호스트 부분에서 비트를 빌려 네트워크 부분에 사용해야 합니다. 이렇게 하면 사용 가능한 네트워크 수가 증가하지만 네트워크당 사용 가능한 호스트 수는 줄어듭니다.

예를 들어 IP 주소가 192.168.1.0/24이고 4개의 서브넷을 생성하려고 한다고 가정합니다. 이렇게 하려면 IP 주소의 호스트 부분에서 2비트를 빌려 네트워크 부분에 6비트를 제공해야 합니다.

```
Original IP address: 192.168.1.0/24
Subnet mask: 255.255.255.0
```

서브넷 마스크의 이진 형식은 다음과 같습니다.

```
11111111 11111111 11111111 00000000
```

두 비트를 빌리기 위해 서브넷 마스크를 다음과 같이 변경합니다.

```
11111111 11111111 11111100 00000000
```

그러면 다음 범위의 4개 서브넷이 제공됩니다.

```
192.168.0.0/26
192.168.0.64/26
192.168.0.128/26
192.168.0.192/26
```

각 서브넷은 최대 62개의 호스트를 수용할 수 있으며 첫 번째 주소와 마지막 주소는 각각 네트워크 및 브로드캐스트 주소용으로 예약되어 있습니다.

코드 예제

다음은 다양한 프로그래밍 언어로 IP 주소를 서브넷팅하는 방법에 대한 몇 가지 예입니다.

### 파이썬

```python
import ipaddress

network = ipaddress.ip_network('192.168.1.0/24')
subnets = list(network.subnets(prefixlen_diff=2))

for subnet in subnets:
    print(subnet)
```

### 자바

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

### 루비

```ruby
require 'ipaddr'

network = IPAddr.new('192.168.1.0/24')
subnets = network.subnet(2)

subnets.each do |subnet|
  puts subnet.to_s
end
```

결론

이 기사에서는 중요한 이유, CIDR 표기법 계산 방법 및 IP 주소를 서브넷팅하는 방법을 포함하여 IP 서브넷팅의 기본 사항을 살펴보았습니다. 또한 다양한 프로그래밍 언어로 된 코드 스니펫을 사용하는 실용적인 예제를 제공했습니다.

서브넷을 통해 네트워크 성능을 개선하고 네트워크 보안을 강화하며 IP 주소 공간을 절약할 수 있습니다. 이는 모든 IT 전문가에게 필수적인 기술이며 이 기사가 여러분이 구축할 수 있는 견고한 토대를 제공했기를 바랍니다.

외부 자원

- 서브넷팅 실습: https://subnettingpractice.com/
- IP 서브넷 계산기: https://www.calculator.net/ip-subnet-calculator.html
- IP 주소 지정 및 CIDR 차트 이해: https://www.cisco.com/c/en/us/support/docs/ip/subnet-mask-lengths/8073-subnetting-made-easy.html