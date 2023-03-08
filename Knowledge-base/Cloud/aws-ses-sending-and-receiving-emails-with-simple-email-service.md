---
title: AWS SES: 간단한 이메일 서비스로 이메일 보내기 및 받기
description: 
published: true
date: 2023-02-17T18:14:50.242Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:57:30.665Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [AWS SES: Sending and Receiving Emails with Simple Email Service***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-ses-sending-and-receiving-emails-with-simple-email-service)
{.links-list}


# AWS SES: 간단한 이메일 서비스로 이메일 송수신

IT 개발 학습 블로그에 오신 것을 환영합니다. 이 기사에서는 AWS Simple Email Service를 사용하여 이메일을 보내고 받는 방법에 대해 설명합니다.

## AWS 심플 이메일 서비스란?

AWS Simple Email Service(SES)는 이메일을 보내고 받는 비용 효율적이고 유연한 방법입니다. 자체 도메인 이름을 사용하여 이메일을 보내고 받을 수 있는 클라우드 기반 이메일 서비스이며 개인 및 기업 사용 사례를 모두 지원합니다.

AWS SES는 다른 AWS 서비스와 통합되는 안정적이고 확장 가능한 이메일 서비스입니다. 선결제 비용이 없는 종량제 가격 모델을 제공하며 설정 및 사용이 쉽습니다.

## AWS SES로 이메일 보내기

AWS SES를 사용하여 이메일을 보내려면 AWS 계정과 확인된 이메일 주소 또는 도메인이 있어야 합니다. 아직 AWS 계정이 없다면 [여기](https://aws.amazon.com/)에서 계정을 생성할 수 있습니다.

AWS 계정이 있으면 [이메일 주소 확인](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses.html) 또는 [도메인](https:/ /docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-domains.html)을 AWS SES와 함께 사용합니다. 이메일 주소 또는 도메인을 확인한 후 이메일 전송을 시작할 수 있습니다.

AWS SES 콘솔, AWS SES API 또는 AWS 명령줄 인터페이스(CLI)를 사용하여 이메일을 보낼 수 있습니다. 이 기사에서는 AWS SES 콘솔을 사용하여 이메일을 보냅니다.

먼저 AWS SES 콘솔로 이동하여 메뉴에서 **이메일 주소**를 선택합니다. 그런 다음 **새 이메일 주소 확인**을 선택하고 확인하려는 이메일 주소를 입력합니다.

![이메일 주소 확인](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/01-verify-email-address.png)

AWS SES는 입력한 주소로 확인 이메일을 보냅니다. 확인 이메일의 지침에 따라 확인 절차를 완료하십시오.

이제 이메일 주소를 확인했으므로 첫 번째 이메일을 보낼 준비가 되었습니다. **AWS SES 콘솔**로 이동하여 **단일 이메일 보내기**를 선택합니다.

![단일 이메일 보내기](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/02-send-email.png)

**단일 이메일 보내기** 페이지에서 다음 정보를 입력합니다.

* **보낸 사람**: 이메일을 보내는 데 사용할 확인된 이메일 주소를 입력합니다.
* **받는사람**: 받는 사람의 이메일 주소를 입력합니다.
* **제목**: 이메일 제목을 입력합니다.
* **메시지**: 이메일 본문을 입력합니다. **비주얼 편집기** 또는 **HTML 편집기**를 사용하여 이메일 형식을 지정할 수 있습니다.

완료되면 **이메일 보내기**를 선택합니다.

![이메일 보내기](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/03-send-email.png)

이메일이 성공적으로 전송되면 AWS SES로부터 확인 이메일을 받아야 합니다.

## AWS SES로 이메일 받기

이메일을 보내는 것 외에도 AWS SES를 사용하여 이메일을 받을 수도 있습니다. AWS SES를 사용하여 사서함에서 이메일을 받거나 수신 이메일을 Amazon S3 또는 Amazon Lambda와 같은 다른 AWS 서비스로 라우팅할 수 있습니다.

이메일 수신을 설정하려면 먼저 AWS SES에서 [규칙 세트 설정](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/receiving-email-getting-started.html)해야 합니다. 콘솔. 규칙 세트는 AWS SES가 수신 이메일을 처리하는 방법을 결정하는 하나 이상의 규칙으로 구성됩니다.

![규칙 집합](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/04-rule-sets.png)

규칙 집합을 설정하려면 메뉴에서 **규칙 집합**을 선택한 다음 **규칙 집합 만들기**를 선택합니다. **규칙 집합 만들기** 페이지에서 규칙 집합의 이름을 입력하고 **규칙 집합 만들기**를 선택합니다.

![규칙 세트 생성](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/05-create-rule-set.png)

규칙 집합이 생성되면 여기에 규칙을 추가할 수 있습니다. 규칙은 일련의 조건과 작업으로 구성됩니다. 수신 이메일이 규칙 조건을 충족하면 작업이 실행됩니다.

규칙 세트에 규칙을 추가하려면 **규칙 추가**를 선택하고 다음 정보를 입력합니다.

* **이름**: 규칙의 이름을 입력합니다.
* **설명**: 규칙에 대한 설명을 입력합니다.
* **범위**: 규칙을 모든 이메일에 적용할지 아니면 특정 조건을 충족하는 이메일에만 적용할지 선택합니다.
* **받는 사람**: 이메일을 받을 이메일 주소를 입력합니다.
* **작업**: 규칙이 트리거될 때 AWS SES에서 수행할 작업을 선택합니다. 이메일을 Amazon S3 버킷에 저장하거나, Amazon Lambda 함수로 보내거나, 다른 이메일 주소로 전달하도록 선택할 수 있습니다.

완료되면 **규칙 만들기**를 선택합니다.

![규칙 만들기](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/06-create-rule.png)

이제 규칙 집합을 만들고 규칙을 추가했으므로 이메일을 받을 준비가 되었습니다. 설정을 테스트하려면 규칙에서 지정한 이메일 주소로 이메일을 보내십시오. 지정한 사서함이나 Amazon S3 버킷에서 이메일을 받아야 합니다.

## 결론

이 기사에서는 AWS Simple Email Service를 사용하여 이메일을 보내고 받는 방법에 대해 설명했습니다. 또한 수신 이메일을 처리하기 위해 규칙 집합을 설정하는 방법도 보여 주었습니다.

AWS SES는 이메일을 보내고 받는 비용 효율적이고 확장 가능한 방법입니다. 설정 및 사용이 간편하고 다른 AWS 서비스와 통합됩니다. 애플리케이션에서 이메일을 보내거나 받아야 하는 경우 AWS SES를 사용하는 것이 좋습니다.

## 추가 리소스

AWS SES에 대해 자세히 알아보려면 다음 리소스를 권장합니다.

* [AWS SES 개발자 가이드](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html)
* [Amazon SES로 이메일 보내기](https://aws.amazon.com/ses/sending-email/)
* [Amazon SES로 이메일 받기](https://aws.amazon.com/ses/receiving-email/)