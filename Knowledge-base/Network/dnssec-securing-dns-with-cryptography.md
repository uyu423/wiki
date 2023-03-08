---
title: DNSSEC: 암호화로 DNS 보호
description: 
published: true
date: 2023-03-04T04:32:29.396Z
tags: 
editor: markdown
dateCreated: 2023-03-04T04:32:27.991Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [DNSSEC: Securing DNS with Cryptography***English** document is available*](/en/Knowledge-base/Network/dnssec-securing-dns-with-cryptography)
{.links-list}


DNSSEC: 암호화로 DNS 보호

DNSSEC란 무엇입니까?
---------------
DNSSEC(도메인 이름 시스템 보안 확장)는 DNS(도메인 이름 시스템)를 보호하는 데 사용되는 프로토콜 집합입니다. DNS는 도메인 이름(예: google.com)을 IP 주소(예: 172.217.6.14)로 변환하여 컴퓨터가 인터넷을 통해 서로 통신할 수 있도록 합니다. DNSSEC는 DNS 서버 간에 교환되는 정보에 인증 및 무결성을 제공하여 DNS에 보안 계층을 추가합니다. DNSSEC는 사용자가 받은 정보가 정확하고 변조되지 않았는지 확인합니다.

DNSSEC 작동 방식
-----------------
DNSSEC는 DNS 레코드에 디지털 서명을 추가하여 작동합니다. 공개 키 암호화를 사용하여 DNS를 보호합니다. DNS 서버는 신뢰 체인을 사용하여 DNS 레코드의 신뢰성을 확인합니다. 각 DNS 영역(DNS 네임스페이스의 일부)은 공개 및 개인 키 쌍을 유지합니다. 개인 키는 영역의 DNS 레코드에 서명하는 데 사용되며 공개 키는 DNS 영역의 상위 영역에 게시됩니다. 이렇게 하면 DNS 서버가 DNS 레코드를 인증할 수 있는 신뢰 체인이 생성됩니다.

DNS 확인자는 IP 주소에 대해 DNS 서버를 쿼리하는 클라이언트입니다. DNS 확인자가 DNS 응답을 받으면 신뢰 체인을 따라 응답의 디지털 서명을 확인합니다. 응답이 인증되면 DNS 확인자는 수신한 정보를 신뢰합니다.

DNSSEC는 리소스 레코드(RR)와 DNSKEY 레코드라는 두 가지 유형의 레코드를 사용합니다. RR에는 도메인 이름을 IP 주소에 매핑하는 데 필요한 정보가 포함되어 있습니다. DNSKEY 레코드는 DNS 레코드에 서명하는 데 사용되는 공개 키를 저장합니다.

DNSSEC 구현
--------------------
DNSSEC를 구현하려면 다음과 같은 몇 가지 단계를 수행해야 합니다.

1. DNSSEC를 지원하는 버전으로 DNS 서버 소프트웨어를 업데이트합니다.
2. DNS 영역에 대한 공개 및 개인 키 쌍을 생성합니다.
3. 상위 영역에 공개 키를 게시합니다.
4. 개인 키로 DNS 레코드에 서명합니다.
5. DNSSEC 유효성 검사기를 사용하여 DNS 레코드와 서명이 올바른지 확인합니다.
6. DNS 영역을 모니터링하여 계속해서 안전한지 확인합니다.

많은 DNS 서버 소프트웨어 패키지가 DNSSEC를 지원합니다. 예를 들어 BIND는 가장 일반적으로 사용되는 DNS 서버 소프트웨어이며 DNSSEC를 지원합니다.

다음은 BIND에서 DNSSEC를 활성화하는 방법의 예입니다.

1. BIND 구성 파일(named.conf)을 편집하고 다음 줄을 추가하여 DNSSEC를 활성화합니다.

   ```dnssec-활성화 예;```

2. dnssec-keygen 명령을 사용하여 공개 및 개인 키 쌍을 생성합니다.

   ```dnssec-keygen -a RSASHA256 -b 2048 -n ZONE example.com```

   이 명령은 Kexample.com.+008+12345.key(공개 키) 및 Kexample.com.+008+12345.private(개인 키)의 두 파일을 생성합니다.

3. DNS 영역 파일에 다음 줄을 추가하여 상위 영역에 공개 키를 게시합니다.

   ```
   example.com. IN DNSKEY 257 3 8 AwEAAagaiLbZU/…
   example.com. IN DNSKEY 256 3 8 AwEAAagaiLbZU/…
   ```

4. dnssec-signzone 명령을 사용하여 개인 키로 DNS 레코드에 서명합니다.

   ```dnssec-signzone -A -3 example.com -N INCREMENT -o example.com db.example.com```

   이 명령은 db.example.com 파일의 DNS 레코드에 서명하고 db.example.com.signed라는 서명된 새 파일을 만듭니다.

5. DNSViz와 같은 DNSSEC 유효성 검사기를 사용하여 DNS 레코드와 서명이 올바른지 확인합니다.

DNSSEC 과제
-----------------
DNSSEC 구현은 다음과 같은 여러 가지 이유로 어려울 수 있습니다.

1. DNSSEC에는 복잡하고 시간이 많이 소요될 수 있는 키 및 디지털 서명 관리가 필요합니다.
2. 일부 DNS 리졸버는 DNSSEC를 지원하지 않으므로 DNSSEC 사용 도메인에 액세스하려는 사용자에게 문제를 일으킬 수 있습니다.
3. DNSSEC는 DNS 응답에 추가 데이터를 추가하여 DNS 패킷의 크기를 증가시킬 수 있습니다.

이러한 문제에도 불구하고 DNSSEC는 DNS를 보호하고 DNS 스푸핑 및 캐시 포이즈닝과 같은 공격을 방지하는 데 필수적인 기술입니다.

결론
----------
DNSSEC는 DNS 레코드에 디지털 서명을 추가하여 DNS에 인증 및 무결성을 제공합니다. 공개 키 암호화를 사용하여 DNS를 보호하고 DNS 레코드를 인증하기 위한 신뢰 체인을 제공합니다. DNSSEC 구현은 어려울 수 있지만 DNS를 보호하고 공격을 방지하는 데 필수적인 기술입니다. DNSSEC를 구현하려면 DNS 서버 소프트웨어를 업데이트하고, 공개 및 개인 키 쌍을 생성하고, 상위 영역에 공개 키를 게시하고, DNS 레코드에 서명하고, DNS 영역이 안전한지 확인해야 합니다.