---
title: AWS WAF: 방화벽 규칙으로 웹 애플리케이션 보호
description: 
published: true
date: 2023-01-31T15:57:42.786Z
tags: 
editor: markdown
dateCreated: 2023-01-31T15:57:39.161Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [AWS WAF: Securing Web Applications with Firewall Rules***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-waf-securing-web-applications-with-firewall-rules)
{.links-list}



# AWS WAF: 방화벽 규칙으로 웹 애플리케이션 보호

웹은 매일 새로운 기술과 위협이 등장하는 끊임없이 진화하는 플랫폼입니다. 결과적으로 웹 애플리케이션 보안은 모든 조직의 사이버 보안 전략에서 중요한 부분이 되었습니다.

웹 애플리케이션을 보호하는 가장 효과적인 방법 중 하나는 웹 애플리케이션 방화벽(WAF)을 사용하는 것입니다. WAF는 웹 애플리케이션과 인터넷 사이에 위치하여 애플리케이션으로 들어오고 나가는 트래픽을 필터링하는 소프트웨어입니다.

AWS WAF는 AWS에서 실행되는 웹 애플리케이션을 보호하는 클라우드 기반 WAF입니다. AWS WAF는 애플리케이션에 도달할 수 있는 트래픽을 제어할 수 있으므로 일반적인 웹 공격으로부터 보호하는 효과적인 도구가 됩니다.

이 기사에서는 AWS WAF를 사용하여 웹 애플리케이션을 보호하는 방법을 살펴보겠습니다. 다음 주제를 다룰 것입니다.

- AWS WAF란 무엇입니까?
- AWS WAF는 어떻게 작동합니까?
- AWS WAF 설정
- WAF 규칙 생성
- 웹 애플리케이션에 WAF 규칙 적용

## AWS WAF란 무엇입니까?

AWS WAF는 AWS에서 실행되는 웹 애플리케이션을 보호하는 클라우드 기반 WAF입니다. AWS WAF는 애플리케이션에 도달할 수 있는 트래픽을 제어할 수 있으므로 일반적인 웹 공격으로부터 보호하는 효과적인 도구가 됩니다.

AWS WAF는 설정 및 관리가 쉽고 Amazon CloudFront, Amazon API Gateway 및 Amazon AWS Lambda와 같은 다른 AWS 서비스와 통합됩니다.

## AWS WAF는 어떻게 작동합니까?

AWS WAF는 웹 애플리케이션에서 들어오고 나가는 트래픽을 검사하고 지정된 규칙을 충족하지 않는 트래픽을 필터링하여 작동합니다.

AWS WAF를 사용하여 소스 IP 주소, URL 또는 요청 콘텐츠와 같은 기준에 따라 트래픽을 허용하거나 차단하는 규칙을 생성할 수 있습니다.

AWS WAF를 사용하면 트래픽 속도를 제한하거나 특정 사용자를 제한하는 규칙을 생성할 수도 있습니다. 이는 서비스 거부(DoS) 공격으로부터 보호하는 데 유용할 수 있습니다.

## AWS WAF 설정

AWS WAF를 사용하려면 먼저 AWS 계정을 설정하고 웹 애플리케이션용 Amazon CloudFront 배포를 생성해야 합니다.

Amazon CloudFront 배포가 있으면 배포에 대해 AWS WAF를 활성화할 수 있습니다. 이렇게 하려면 WAF 웹 ACL을 생성하고 배포와 연결해야 합니다.

## WAF 규칙 만들기

AWS WAF를 설정하면 규칙 생성을 시작할 수 있습니다. 규칙은 AWS Management Console, AWS WAF API 또는 AWS 명령줄 인터페이스(CLI)를 사용하여 생성할 수 있습니다.

규칙을 만들 때 다음을 지정해야 합니다.

- 규칙의 이름
- 규칙이 트리거될 때 취할 조치(허용 또는 차단)
- 규칙을 트리거하는 조건

## 웹 애플리케이션에 WAF 규칙 적용

WAF 규칙을 만든 후에는 웹 애플리케이션에 적용해야 합니다. 이는 AWS Management Console, AWS WAF API 또는 AWS 명령줄 인터페이스(CLI)를 사용하여 수행할 수 있습니다.

웹 애플리케이션에 규칙을 적용할 때 다음을 지정해야 합니다.

- 웹 ACL의 이름
- 웹 ACL의 ARN
- 규칙의 이름
- 규칙의 우선순위

웹 애플리케이션에 WAF 규칙을 적용하면 애플리케이션에서 들어오고 나가는 모든 트래픽이 WAF에서 검사됩니다. 이는 애플리케이션의 성능에 영향을 줄 수 있으므로 프로덕션 트래픽에 규칙을 적용하기 전에 규칙을 테스트하는 것이 중요합니다.

## 결론

이 기사에서는 AWS WAF를 사용하여 웹 애플리케이션을 보호하는 방법을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

- AWS WAF란 무엇입니까?
- AWS WAF는 어떻게 작동합니까?
- AWS WAF 설정
- WAF 규칙 생성
- 웹 애플리케이션에 WAF 규칙 적용

웹 애플리케이션을 보호하려는 경우 AWS WAF는 고려해 볼 만한 강력한 도구입니다.