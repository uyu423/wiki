---
title: Traceroute 사용 방법: 네트워크 경로 분석을 위한 명령줄 도구
description: 
published: true
date: 2023-03-14T19:33:03.086Z
tags: 
editor: markdown
dateCreated: 2023-03-14T19:33:03.086Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Use Traceroute: A Command-Line Tool for Network Path Analysis***English** document is available*](/en/Knowledge-base/Network/how-to-use-traceroute-a-command-line-tool-for-network-path-analysis)
{.links-list}

## 소개

Traceroute는 네트워크 경로 분석에 도움이 되는 명령줄 도구입니다. 데이터 패킷이 소스에서 목적지까지 이동하는 경로를 결정하고 그 과정에서 네트워크 문제를 식별하는 데 사용됩니다. 각 네트워크 홉의 경로 및 응답 시간을 분석하여 지연, 패킷 손실 또는 네트워크 성능에 영향을 줄 수 있는 기타 문제가 있는 위치를 식별할 수 있습니다.

이 기사에서는 traceroute를 사용하여 네트워크 경로를 분석하고 네트워크 문제를 진단하며 네트워크 성능을 개선하는 방법을 살펴봅니다.

## Traceroute 기본 사항

Traceroute는 TTL(Time-to-Live) 값이 증가하는 일련의 패킷을 전송하여 작동합니다. TTL 값은 패킷이 라우터에 의해 폐기되기 전에 취할 수 있는 최대 홉 수입니다. 경로의 각 라우터는 TTL 값을 1씩 감소시키고 TTL 값이 0에 도달하면 패킷을 버리고 ICMP 오류 메시지를 발신자에게 다시 보냅니다.

Traceroute는 이 메커니즘을 사용하여 경로에 있는 각 라우터의 IP 주소와 응답 시간을 결정합니다. 기본적으로 traceroute는 각 라우터에 3개의 패킷을 보내고 각 홉에 대한 결과를 테이블 형식으로 표시합니다.

## Traceroute 사용

traceroute를 사용하려면 명령 프롬프트 또는 터미널 창을 열고 다음 명령을 입력합니다.

```
traceroute [destination IP or hostname]
```

[대상 IP 또는 호스트 이름]을 분석하려는 대상의 IP 주소 또는 호스트 이름으로 바꿉니다. 예를 들어 8.8.8.8에서 Google의 DNS 서버 경로를 분석하려면 다음 명령을 입력합니다.

```
traceroute 8.8.8.8
```

traceroute 명령을 실행하면 다음 열이 있는 테이블이 표시됩니다.

- 홉 번호: 경로에 있는 라우터의 시퀀스 번호입니다.
- 호스트 이름 또는 IP 주소: 경로에 있는 라우터의 이름 또는 IP 주소입니다.
- 응답 시간: 라우터가 traceroute 패킷에 응답하는 데 걸린 시간입니다.

출력에는 라우터의 호스트 이름과 IP 주소는 물론 각 홉에 대해 보내고 받은 패킷 수가 표시될 수도 있습니다.

## 경로 추적 옵션

Traceroute에는 동작을 사용자 지정하는 데 사용할 수 있는 몇 가지 옵션이 있습니다. 가장 일반적인 옵션은 다음과 같습니다.

- `-n`: 호스트 이름을 확인하지 않습니다. 출력에서 IP 주소만 보려면 이 옵션을 사용하십시오.
- `-q [숫자]`: 각 라우터로 보내는 패킷 수를 설정합니다. 기본값은 3개입니다.
- `-w [숫자]`: 각 응답에 대한 제한 시간을 초 단위로 설정합니다. 기본값은 5초입니다.
- `-m [숫자]`: 추적할 최대 홉 수를 설정합니다. 기본값은 30입니다.
- `-f [숫자]`: 초기 TTL 값을 설정합니다. 특정 홉에서 추적을 시작하려면 이 옵션을 사용하십시오.

옵션을 사용하려면 다음과 같이 traceroute 명령 뒤에 추가하십시오.

```
traceroute [options] [destination IP or hostname]
```

예를 들어 각 응답에 대한 제한 시간을 10초로 설정하려면 다음 명령을 사용합니다.

```
traceroute -w 10 8.8.8.8
```

## Traceroute 출력 해석

traceroute 명령을 실행할 때 처음에는 출력을 해석하기 어려울 수 있습니다. 다음은 traceroute 출력을 분석하기 위한 몇 가지 팁입니다.

- 응답 시간이 높은 홉을 찾습니다. 이러한 홉은 네트워크 정체, 패킷 손실 또는 기타 문제를 나타낼 수 있습니다.
- 응답하지 않는 홉을 찾습니다. 이러한 홉은 방화벽이나 ICMP 패킷을 차단하는 다른 네트워크 장치를 나타낼 수 있습니다.
- 출력에서 별표(*)가 있는 홉을 찾습니다. 이러한 홉은 응답 시간이 제한 시간을 초과했거나 라우터가 traceroute 패킷에 응답하지 않았음을 나타냅니다.
- 동일한 대상에 대한 여러 추적 경로의 결과를 비교합니다. 이를 통해 시간 경과에 따른 네트워크 경로 또는 성능의 변화를 식별할 수 있습니다.

## Traceroute 대안

Traceroute는 네트워크 경로를 분석하는 데 유용한 도구이지만 사용 가능한 유일한 도구는 아닙니다. 다음은 traceroute에 대한 몇 가지 대안입니다.

- **MTR(My TraceRoute)**: MTR은 traceroute와 ping의 조합입니다. 각 홉에 패킷을 보내고 결과를 실시간으로 표시합니다. 이를 통해 traceroute보다 더 빠르게 네트워크 대기 시간 및 패킷 손실 문제를 식별할 수 있습니다.
- **PathPing**: PathPing은 traceroute와 ping을 결합한 Windows 명령줄 도구입니다. 각 홉에 패킷을 보내고 결과를 테이블 형식으로 표시합니다. PathPing에는 각 홉에서 손실된 패킷 수 및 각 홉에 대한 평균 응답 시간과 같은 추가 정보도 포함됩니다.
- **PingPlotter**: PingPlotter는 결과를 실시간으로 표시하는 그래픽 경로 추적 도구입니다. 여기에는 시간 경과에 따른 네트워크 대기 시간을 그래프로 표시하고 추후 분석을 위해 추적을 저장하는 기능과 같은 추가 기능이 포함됩니다.

## 결론

Traceroute는 네트워크 경로를 분석하고 네트워크 문제를 진단하기 위한 강력한 도구입니다. traceroute의 작동 방식과 그 출력을 해석하는 방법을 이해하면 네트워크 성능에 영향을 줄 수 있는 지연, 패킷 손실 또는 기타 문제가 있는 위치를 식별할 수 있습니다.

traceroute에 어려움이 있거나 다른 옵션을 탐색하려는 경우 위에서 언급한 traceroute 대안 중 하나를 사용하는 것이 좋습니다. 이러한 도구는 네트워크 성능을 개선하고 네트워크 문제를 더 빠르게 식별하는 데 도움이 되는 추가 기능과 통찰력을 제공할 수 있습니다.

## 외부 리소스

- [Traceroute 위키백과 페이지](https://en.wikipedia.org/wiki/Traceroute)
- [MTR Wikipedia 페이지](https://en.wikipedia.org/wiki/MTR_(software))
- [PathPing Microsoft Docs](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/pathping)
- [핑플로터 홈페이지](https://www.pingplotter.com/)