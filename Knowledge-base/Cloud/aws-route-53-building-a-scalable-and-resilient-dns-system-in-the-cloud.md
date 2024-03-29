---
title: AWS Route 53: 클라우드에서 확장 가능하고 탄력적인 DNS 시스템 구축
description: 
published: true
date: 2023-02-06T00:55:53.727Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:55:52.142Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Route 53: Building a Scalable and Resilient DNS System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-route-53-building-a-scalable-and-resilient-dns-system-in-the-cloud)
{.links-list}


# AWS Route 53: 클라우드에서 확장 가능하고 탄력적인 DNS 시스템 구축

DNS는 모든 웹 기반 인프라의 중요한 부분이며 Route 53은 AWS의 관리형 DNS 서비스입니다. 이 기사에서는 Route 53을 사용하여 클라우드에서 확장 가능하고 탄력적인 DNS 시스템을 구축하는 방법을 살펴보겠습니다.

## DNS란?

DNS는 사람이 읽을 수 있는 도메인 이름(예: www.example.com)을 기계가 읽을 수 있는 IP 주소(예: 192.168.1.1)로 변환하는 프로세스입니다. 이것은 인간이 숫자보다 이름을 훨씬 더 잘 기억하기 때문에 필요합니다.

DNS는 도메인 이름 및 관련 IP 주소의 데이터베이스 유지 관리를 담당하는 DNS 서버에서 처리합니다. 사용자가 브라우저에 도메인 이름을 입력하면 브라우저는 DNS 서버에 연결하여 IP 주소를 조회합니다. 그러면 DNS 서버가 IP 주소로 응답하고 브라우저는 해당 IP 주소의 웹 서버에 연결됩니다.

## 루트 53이 무엇인가요?

Route 53은 AWS의 관리형 DNS 서비스입니다. 사용자를 인터넷 응용 프로그램으로 라우팅하는 비용 효율적인 방법을 제공하는 가용성과 확장성이 뛰어난 DNS 서비스입니다. Route 53은 IPv6와 완벽하게 호환되며 다음과 같이 사용하기 쉽도록 설계된 다양한 기능을 제공합니다.

- 상태 확인: Route 53은 주기적으로 웹 서버의 상태를 확인하고 사용할 수 없는 서버에서 트래픽을 라우팅할 수 있습니다.

- 대기 시간 기반 라우팅: Route 53은 사용자 위치를 기반으로 트래픽을 가장 빠른 서버로 라우팅할 수 있습니다.

- 지리적 위치 기반 라우팅: Route 53은 사용자 위치에 따라 다른 서버로 트래픽을 라우팅할 수 있습니다. 이것은 사용자를 가장 가까운 서버로 라우팅하거나 위치에 따라 사용자를 웹 사이트의 다른 버전으로 라우팅하는 데 사용할 수 있습니다.

- 장애 조치: 기본 서버를 사용할 수 없는 경우 자동으로 대기 서버로 장애 조치하도록 Route 53을 구성할 수 있습니다.

- 가중 라우팅: Route 53은 사용자가 지정한 가중치에 따라 트래픽을 다른 서버로 라우팅하도록 구성할 수 있습니다. 이것은 테스트 중인 새 서버로 더 많은 트래픽을 라우팅하거나 문제가 있는 서버로 더 적은 트래픽을 라우팅하는 데 사용할 수 있습니다.

## Route 53 호스팅 영역 생성

Route 53 사용을 시작하려면 먼저 호스팅 영역을 생성해야 합니다. 호스팅 영역은 단일 도메인에 대한 DNS 레코드 모음입니다. 예를 들어 도메인 example.com을 소유하고 있는 경우 example.com에 대한 호스팅 영역을 생성하고 호스팅 영역에 DNS 레코드를 추가합니다.

호스팅 영역을 생성하려면 AWS Management Console, Route 53 API 또는 AWS Command Line Interface(CLI)를 사용할 수 있습니다.

## Route 53 호스팅 영역에 DNS 레코드 추가

호스팅 영역을 생성한 후에는 호스팅 영역에 DNS 레코드를 추가할 수 있습니다. DNS 레코드는 트래픽을 웹사이트 또는 애플리케이션으로 라우팅하는 데 사용됩니다.

DNS 레코드에는 다양한 유형이 있지만 가장 일반적인 유형은 A 레코드입니다. A 레코드는 도메인 이름을 IPv4 주소에 매핑합니다. 예를 들어 IPv4 주소 192.168.1.1을 가리키는 도메인 example.com에 대한 A 레코드를 만들 수 있습니다.

Route 53 호스팅 영역에 A 레코드를 추가하려면 AWS Management Console, Route 53 API 또는 AWS 명령줄 인터페이스(CLI)를 사용할 수 있습니다.

## Amazon EC2 인스턴스로 트래픽 라우팅

이 섹션에서는 트래픽을 Amazon EC2 인스턴스로 라우팅하는 방법을 살펴보겠습니다. Amazon EC2는 클라우드에서 크기 조정 가능한 컴퓨팅 용량을 제공하는 웹 서비스입니다.

트래픽을 Amazon EC2 인스턴스로 라우팅하려면 Amazon EC2 인스턴스의 퍼블릭 IP 주소를 가리키는 A 레코드를 생성해야 합니다. Amazon EC2 인스턴스의 퍼블릭 IP 주소는 Amazon EC2 콘솔에서 찾을 수 있습니다.

## Amazon S3 버킷으로 트래픽 라우팅

이 섹션에서는 트래픽을 Amazon S3 버킷으로 라우팅하는 방법을 살펴보겠습니다. Amazon S3는 클라우드에 스토리지를 제공하는 웹 서비스입니다.

트래픽을 Amazon S3 버킷으로 라우팅하려면 Amazon S3 버킷을 가리키는 CNAME 레코드를 생성해야 합니다. Amazon S3 버킷은 인터넷에서 액세스할 수 있도록 구성해야 합니다.

## Route 53 상태 확인

Route 53을 사용하여 웹 서버의 상태를 주기적으로 확인하고 사용할 수 없는 서버에서 트래픽을 라우팅할 수 있습니다. 이것을 건강 검사라고 합니다.

상태 확인을 생성할 때 Route 53이 웹 서버의 상태를 확인하는 데 사용할 프로토콜(HTTP, HTTPS 또는 TCP), 포트, 경로 또는 도메인을 지정합니다. 그런 다음 Route 53은 주기적으로 지정된 경로 또는 도메인에 요청을 보내고 응답 코드를 확인하여 웹 서버의 상태를 확인합니다.

서버 상태에 따라 특정 서버로 트래픽을 라우팅하려는 경우 각 서버에 대한 상태 확인을 생성한 다음 트래픽을 정상 서버로 라우팅하도록 Route 53을 구성할 수 있습니다.

## Route 53 지연 시간 기반 라우팅

Route 53은 사용자의 위치에 따라 트래픽을 가장 빠른 서버로 라우팅하는 데 사용할 수 있습니다. 이를 대기 시간 기반 라우팅이라고 합니다.

지연 시간 기반 라우팅을 사용하려면 트래픽을 라우팅하려는 각 서버에 대해 지연 시간 리소스 레코드 세트를 생성해야 합니다. 그런 다음 Route 53은 사용자와 각 서버 간의 대기 시간을 주기적으로 확인하여 가장 빠른 서버를 결정합니다.

## Route 53 지리적 위치 기반 라우팅

Route 53을 사용하여 사용자 위치에 따라 다른 서버로 트래픽을 라우팅할 수 있습니다. 이를 지리적 위치 기반 라우팅이라고 합니다.

지리적 위치 기반 라우팅을 사용하려면 트래픽을 라우팅하려는 각 서버에 대한 지리적 위치 리소스 레코드 세트를 생성해야 합니다. 그런 다음 Route 53은 사용자의 위치를 사용하여 트래픽을 라우팅할 서버를 결정합니다.

## Route 53 장애 조치

기본 서버를 사용할 수 없는 경우 자동으로 대기 서버로 장애 조치하도록 Route 53을 구성할 수 있습니다. 이를 장애 조치라고 합니다.

장애 조치를 사용하려면 트래픽을 라우팅하려는 각 서버에 대한 장애 조치 리소스 레코드 세트를 생성해야 합니다. 그런 다음 Route 53은 기본 서버의 상태를 주기적으로 확인합니다. 기본 서버를 사용할 수 없는 경우 Route 53은 트래픽을 대기 서버로 라우팅합니다.

## Route 53 가중 라우팅

지정한 가중치에 따라 다른 서버로 트래픽을 라우팅하도록 Route 53을 구성할 수 있습니다. 이를 가중치 라우팅이라고 합니다.

가중치 기반 라우팅을 사용하려면 트래픽을 라우팅하려는 각 서버에 대해 가중치 기반 리소스 레코드 세트를 생성해야 합니다. 그런 다음 Route 53은 지정한 가중치를 사용하여 트래픽을 라우팅할 서버를 결정합니다.

## 결론

이 기사에서는 Route 53을 사용하여 클라우드에서 확장 가능하고 탄력적인 DNS 시스템을 구축하는 방법을 살펴보았습니다. Route 53 호스팅 영역을 생성하고 DNS 레코드를 호스팅 영역에 추가하고 트래픽을 Amazon EC2 및 Amazon S3 인스턴스로 라우팅하는 방법을 살펴보았습니다. 또한 Route 53 상태 확인, 대기 시간 기반 라우팅, 지리적 위치 기반 라우팅, 장애 조치 및 가중치 기반 라우팅을 사용하는 방법도 살펴보았습니다.