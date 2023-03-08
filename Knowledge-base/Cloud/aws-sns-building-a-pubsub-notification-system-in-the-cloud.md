---
title: AWS SNS: 클라우드에서 Pub/Sub 알림 시스템 구축
description: 
published: true
date: 2023-02-11T08:55:13.855Z
tags: 
editor: markdown
dateCreated: 2023-02-11T08:55:12.288Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS SNS: Building a Pub/Sub Notification System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sns-building-a-pubsub-notification-system-in-the-cloud)
{.links-list}


# AWS SNS: 클라우드에 Pub/Sub 알림 시스템 구축

이 기사에서는 AWS SNS(Simple Notification Service)를 사용하여 간단한 pub/sub 알림 시스템을 설정하는 방법을 살펴보겠습니다. SNS 주제 설정부터 구독 생성, 알림 전송까지 모든 것을 다룹니다.

## SNS 주제 정하기

첫 번째 단계는 SNS 주제를 만드는 것입니다. 이는 AWS Management Console, AWS CLI 또는 SDK를 통해 수행할 수 있습니다.

주제 생성은 간단한 프로세스입니다.

1. SNS 콘솔로 이동하여 **주제 만들기**를 클릭합니다.
2. **주제 이름** 및 **표시 이름**을 입력합니다.
3. **주제 만들기**를 클릭합니다.

이제 주제 목록에 새 주제가 표시됩니다.

## 구독 만들기

이제 주제가 있으므로 구독을 만들어야 합니다. 이렇게 하면 알림이 전달될 엔드포인트를 지정할 수 있습니다.

1. **구독** 탭으로 이동하여 **구독 만들기**를 클릭합니다.
2. **주제 ARN** 드롭다운에서 생성한 주제를 선택합니다.
3. **프로토콜** 드롭다운에서 전달에 사용할 프로토콜을 선택합니다. AWS SNS는 HTTP, HTTPS, 이메일 등을 비롯한 다양한 프로토콜을 지원합니다.
4. 구독에 대한 **엔드포인트**를 입력합니다. 이것은 알림이 전달될 URL 또는 이메일 주소입니다.
5. **구독 생성**을 클릭합니다.

이제 구독 목록에 새 구독이 표시됩니다.

## 알림 보내기

이제 주제와 구독이 설정되었으므로 첫 번째 알림을 보낼 준비가 되었습니다.

1. **주제** 탭으로 이동하여 알림을 보낼 주제를 선택합니다.
2. **주제에 게시**를 클릭합니다.
3. 알림에 대한 **제목** 및 **메시지**를 입력합니다.
4. **메시지 게시**를 클릭합니다.

이제 알림이 구독에 지정된 엔드포인트로 전달됩니다.

## 결론

이 기사에서는 AWS SNS를 사용하여 간단한 게시/구독 알림 시스템을 설정하는 방법을 살펴보았습니다. 주제 생성에서 구독 생성 및 알림 전송에 이르기까지 모든 것을 다루었습니다. AWS SNS를 사용하면 다양한 엔드포인트에 알림을 보내는 데 사용할 수 있는 알림 시스템을 쉽게 설정할 수 있습니다.