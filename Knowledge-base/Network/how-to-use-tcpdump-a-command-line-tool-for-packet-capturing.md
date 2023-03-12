---
title: Tcpdump 사용 방법: 패킷 캡처를 위한 명령줄 도구
description: 
published: true
date: 2023-03-12T19:33:04.669Z
tags: 
editor: markdown
dateCreated: 2023-03-12T19:33:04.669Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Use Tcpdump: A Command-Line Tool for Packet Capturing***English** document is available*](/en/Knowledge-base/Network/how-to-use-tcpdump-a-command-line-tool-for-packet-capturing)
{.links-list}

## 소개
Tcpdump는 네트워크 분석에서 패킷 캡처를 위해 널리 사용되는 명령줄 도구입니다. 네트워크 관리자와 보안 전문가가 네트워크 문제를 식별하고, 네트워크 문제를 해결하고, 네트워크 트래픽을 분석하는 데 필수적인 도구입니다. Tcpdump는 네트워크 패킷을 실시간으로 캡처 및 표시하거나 나중에 분석할 수 있도록 파일에 저장합니다. 이 자습서에서는 Tcpdump를 사용하여 네트워크 패킷을 캡처하고 분석하는 방법에 대한 포괄적인 가이드를 제공합니다.

## Tcpdump 설치
Tcpdump 사용 방법에 대해 알아보기 전에 Tcpdump가 시스템에 설치되어 있는지 확인해야 합니다. Tcpdump는 macOS를 포함한 대부분의 Linux 및 Unix 기반 운영 체제에서 사용할 수 있습니다. Tcpdump를 설치하려면 터미널을 열고 다음 명령을 실행합니다.

```
sudo apt-get install tcpdump
```

macOS 사용자의 경우 다음 명령을 실행하여 Homebrew를 사용하여 Tcpdump를 설치할 수 있습니다.

```
brew install tcpdump
```

설치가 완료되면 다음 명령을 실행하여 Tcpdump가 설치되었는지 확인할 수 있습니다.

```
tcpdump --version
```

## 기본 Tcpdump 명령
Tcpdump는 명령줄 도구이며 다양한 매개변수를 사용하여 네트워크 트래픽을 캡처하고 분석합니다. Tcpdump를 사용하여 네트워크 트래픽을 캡처하는 가장 기본적인 명령은 다음과 같습니다.

```
sudo tcpdump
```

이 명령은 기본 네트워크 인터페이스에서 모든 네트워크 트래픽을 캡처하고 실시간으로 패킷을 표시합니다. 패킷 캡처를 중지하려면 ```CTRL+C```를 누르십시오.

특정 네트워크 인터페이스에서 패킷을 캡처하려면 ```-i``` 옵션 뒤에 인터페이스 이름을 사용할 수 있습니다. 예를 들면 다음과 같습니다.

```
sudo tcpdump -i eth0
```

이 명령은 eth0 인터페이스를 통해 흐르는 모든 패킷을 캡처합니다.

특정 유형의 트래픽만 캡처하려면 Tcpdump의 필터 옵션을 사용할 수 있습니다. Tcpdump는 프로토콜, 포트, IP 주소 등을 기반으로 트래픽을 필터링합니다. 예를 들어 포트 80에서 HTTP 트래픽을 캡처하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump port 80
```

이 명령은 소스 또는 대상 포트가 80인 모든 패킷을 캡처합니다.

## 고급 Tcpdump 명령
Tcpdump에는 네트워크 트래픽을 자세히 캡처하고 분석할 수 있는 많은 고급 옵션이 있습니다. 다음은 특정 네트워크 트래픽을 캡처하는 데 사용할 수 있는 몇 가지 고급 Tcpdump 명령입니다.

### 1. ICMP 트래픽 캡처
ICMP 트래픽을 캡처하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump icmp
```

이 명령은 ping 요청 및 응답을 포함하여 모든 ICMP 패킷을 캡처합니다.

### 2. DNS 트래픽 캡처
DNS 트래픽을 캡처하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump port 53
```

이 명령은 포트 53에서 모든 DNS 패킷을 캡처합니다.

### 3. HTTP 트래픽 캡처
HTTP 트래픽을 캡처하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump port 80 -s 0 -w http.pcap
```

이 명령은 포트 80에서 모든 HTTP 패킷을 캡처하여 ```http.pcap```이라는 파일에 저장하고 스냅샷 길이를 0으로 설정합니다. 이는 전체 패킷을 캡처한다는 의미입니다.

### 4. FTP 트래픽 캡처
FTP 트래픽을 캡처하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump port ftp or ftp-data
```

이 명령은 포트 21의 모든 FTP 패킷과 포트 20의 FTP 데이터 패킷을 캡처합니다.

### 5. 텔넷 트래픽 캡처
텔넷 트래픽을 캡처하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump port 23 -w telnet.pcap
```

이 명령은 포트 23에서 모든 Telnet 패킷을 캡처하여 ```telnet.pcap```이라는 파일에 저장합니다.

## Tcpdump 출력 분석
Tcpdump를 사용하여 네트워크 트래픽을 캡처한 후 캡처된 패킷을 분석하여 네트워크 문제를 식별하고 네트워크 문제를 해결하고 네트워크 트래픽을 분석해야 합니다. Tcpdump에는 다음을 포함하여 캡처된 패킷을 분석하는 몇 가지 옵션이 있습니다.

### 1. 캡처된 패킷 표시
캡처된 패킷을 표시하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump -r file.pcap
```

이 명령은 ```file.pcap``` 파일에서 패킷을 읽고 표시합니다.

### 2. 캡처된 패킷 필터링
캡처된 패킷을 필터링하기 위해 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump -r file.pcap src 192.168.0.10
```

이 명령은 파일 ```file.pcap```에서 패킷을 읽고 소스 IP 주소가 ```192.168.0.10```인 패킷을 표시합니다.

### 3. 캡처된 패킷 통계
캡처된 패킷에 대한 통계를 얻으려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump -r file.pcap -qtnx
```

이 명령은 ```file.pcap``` 파일에서 패킷을 읽고 패킷 수, 소스 및 대상 IP 주소, 프로토콜 및 패킷 크기를 표시합니다.

### 4. 캡처된 패킷에서 데이터 추출
캡처된 패킷에서 데이터를 추출하려면 다음 명령을 사용할 수 있습니다.

```
sudo tcpdump -r file.pcap -A | grep keyword
```

이 명령은 ```file.pcap``` 파일에서 패킷을 읽고 각 패킷의 ASCII 데이터를 표시하고 키워드가 포함된 패킷을 필터링합니다.

## 마무리 생각
Tcpdump는 네트워크 관리자와 보안 전문가가 네트워크 트래픽을 캡처하고 분석하는 데 필수적인 도구입니다. 이 자습서에서는 특정 네트워크 트래픽을 캡처하는 기본 및 고급 Tcpdump 명령을 다루고 캡처된 패킷을 분석하여 네트워크 문제를 식별하고 네트워크 문제를 해결했습니다. Tcpdump는 마스터하기 전에 약간의 연습이 필요한 강력한 도구이지만 네트워크 트래픽으로 작업할 때 귀중한 리소스입니다.

## 외부 리소스
- [Tcpdump 매뉴얼 페이지](https://www.tcpdump.org/manpages/tcpdump.1.html)
- [초보자를 위한 Tcpdump 튜토리얼](https://danielmiessler.com/study/tcpdump/)
- [Tcpdump 예제](https://hackertarget.com/tcpdump-examples/)