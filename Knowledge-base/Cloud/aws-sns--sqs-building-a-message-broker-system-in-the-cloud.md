---
title: AWS SNS 및 SQS: 클라우드에서 메시지 브로커 시스템 구축
description: 
published: true
date: 2023-02-02T03:23:55.440Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:23:53.851Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS SNS & SQS: Building a Message Broker System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sns--sqs-building-a-message-broker-system-in-the-cloud)
{.links-list}


# AWS SNS & SQS: 클라우드에 메시지 브로커 시스템 구축

이 기사에서는 AWS SNS 및 SQS를 사용하여 클라우드에서 메시지 브로커 시스템을 구축하는 방법을 살펴보겠습니다. 메시지 브로커 사용의 이점과 서로 다른 서비스 간의 메시지 처리 및 라우팅에 도움이 되는 방법을 살펴보겠습니다. 또한 자신의 애플리케이션에서 SNS 및 SQS를 설정하고 사용하는 방법을 보여주는 몇 가지 코드 예제를 살펴보겠습니다.

## 메시지 브로커란?

메시지 브로커는 서로 다른 소프트웨어 응용 프로그램 간에 메시지를 처리하고 라우팅하는 데 도움이 되는 시스템입니다. 다음과 같은 많은 이점을 제공할 수 있습니다.

- 메시지 전송과 메시지 처리를 분리하여 성능 향상
- 메시지 라우팅 방식의 유연성 향상
- 많은 수의 메시지를 처리하는 기능
- 메시지 대기열 관리 용이

메시지 브로커는 많은 수의 메시지를 처리해야 하거나 다른 서비스 간에 메시지를 라우팅해야 하는 애플리케이션에서 자주 사용됩니다. 예를 들어 메시지 브로커를 사용하여 웹 사이트에서 주문을 처리하고 올바른 이행 서비스로 라우팅할 수 있습니다.

## SNS와 SQS란?

SNS와 SQS는 메시지 브로커 시스템을 구축하는 데 사용할 수 있는 Amazon Web Services(AWS)의 두 가지 서비스입니다.

SNS는 여러 구독자에게 메시지를 보내는 데 사용할 수 있는 게시/구독 메시징 서비스입니다. 여러 구독자에게 메시지를 보내거나 특정 구독자에게 메시지를 보내는 데 사용할 수 있습니다.

SQS는 메시지가 처리될 때까지 메시지를 저장하는 데 사용할 수 있는 메시지 대기열 서비스입니다. 메시지 전송과 메시지 처리를 분리하거나 메시지를 일괄 처리하는 데 사용할 수 있습니다.

## SNS 및 SQS 설정

SNS와 SQS를 사용하려면 AWS 계정을 설정하고 새로운 SNS 주제와 SQS 대기열을 생성해야 합니다.

SNS 주제 생성은 2단계 프로세스입니다. 먼저 주제를 생성한 다음 주제를 구독해야 합니다. 새 SNS 주제를 생성하려면 AWS Management 콘솔을 사용하거나 AWS CLI를 사용할 수 있습니다.

AWS Management Console을 사용하여 새 SNS 주제를 생성하려면 콘솔에 로그인하고 SNS 서비스로 이동합니다. "주제 만들기" 버튼을 클릭하고 주제의 이름과 설명을 입력합니다. 주제가 생성되면 "주제 구독" 버튼을 클릭하고 구독 세부 정보를 입력하여 구독할 수 있습니다.

AWS CLI를 사용하여 새 SNS 주제를 생성하려면 다음 명령을 사용할 수 있습니다.

```
aws sns create-topic --name my-topic
```

주제를 구독하려면 다음 명령을 사용할 수 있습니다.

```
aws sns subscribe --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --protocol email --notification-endpoint myemail@example.com
```

SQS 대기열 생성은 3단계 프로세스입니다. 먼저 대기열을 생성한 다음 권한을 설정하고 마지막으로 대기열을 구독해야 합니다. 새 SQS 대기열을 생성하려면 AWS Management 콘솔을 사용하거나 AWS CLI를 사용할 수 있습니다.

AWS Management Console을 사용하여 새 SQS 대기열을 생성하려면 콘솔에 로그인하고 SQS 서비스로 이동합니다. "대기열 만들기" 버튼을 클릭하고 대기열의 이름과 설명을 입력합니다. 대기열이 생성되면 "권한" 탭을 클릭하고 새 권한을 추가하여 권한을 설정할 수 있습니다. 마지막으로 "주제 구독" 버튼을 클릭하고 구독 세부 정보를 입력하여 대기열을 구독할 수 있습니다.

AWS CLI를 사용하여 새 SQS 대기열을 생성하려면 다음 명령을 사용할 수 있습니다.

```
aws sqs create-queue --queue-name my-queue
```

권한을 설정하려면 다음 명령을 사용할 수 있습니다.

```
aws sqs set-queue-attributes --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --attributes '{"Policy":"{\"Version\":\"2012-10-17\",\"Id\":\"MyQueuePolicy\",\"Statement\":[{\"Sid\":\"MyQueueSid\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":\"*\"},\"Action\":\"sqs:SendMessage\",\"Resource\":\"arn:aws:sqs:us-east-1:123456789012:my-queue\",\"Condition\":{\"ArnLike\":{\"aws:SourceArn\":\"arn:aws:sns:us-east-1:123456789012:my-topic\"}}}]}"}'
```

대기열을 구독하려면 다음 명령을 사용할 수 있습니다.

```
aws sqs subscribe-queue --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic
```

## 메시지 보내기

이제 SNS 주제와 SQS 대기열을 설정했으므로 메시지 전송을 시작할 수 있습니다. 메시지를 보내려면 AWS Management 콘솔을 사용하거나 AWS CLI를 사용할 수 있습니다.

AWS Management Console을 사용하여 메시지를 보내려면 콘솔에 로그인하고 SNS 서비스로 이동합니다. "메시지 작성" 버튼을 클릭하고 메시지 세부 정보를 입력합니다. 보낼 메시지 수와 메시지의 지속 시간을 지정할 수도 있습니다. 메시지 작성이 완료되면 "메시지 게시" 버튼을 클릭하여 메시지를 보낼 수 있습니다.

AWS CLI를 사용하여 메시지를 보내려면 다음 명령을 사용할 수 있습니다.

```
aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --message "Hello, world!"
```

## 메시지 수신

메시지를 보내면 SQS 대기열에 저장됩니다. 메시지를 수신하려면 AWS Management 콘솔을 사용하거나 AWS CLI를 사용할 수 있습니다.

AWS Management Console을 사용하여 메시지를 받으려면 콘솔에 로그인하고 SQS 서비스로 이동합니다. "메시지 가져오기" 버튼을 클릭하고 검색할 메시지 수를 선택합니다. 또한 메시지의 TTL(Time To Live) 및 가시성 제한 시간을 지정할 수도 있습니다. 메시지가 검색되면 "메시지 삭제" 버튼을 클릭하여 대기열에서 메시지를 삭제할 수 있습니다.

AWS CLI를 사용하여 메시지를 수신하려면 다음 명령을 사용할 수 있습니다.

```
aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue
```

## 결론

이 기사에서는 AWS SNS 및 SQS를 사용하여 클라우드에서 메시지 브로커 시스템을 구축하는 방법을 살펴보았습니다. 메시지 브로커가 여러 가지 이점을 제공하는 방법과 SNS 및 SQS를 사용하여 메시지를 보내고 받는 방법을 살펴보았습니다. 또한 자신의 애플리케이션에서 SNS 및 SQS를 설정하고 사용하는 방법을 보여주는 몇 가지 코드 예제를 살펴보았습니다.