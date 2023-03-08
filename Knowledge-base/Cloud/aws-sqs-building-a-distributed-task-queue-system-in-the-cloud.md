---
title: AWS SQS: 클라우드에서 분산 작업 대기열 시스템 구축
description: 
published: true
date: 2023-02-17T18:16:28.289Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:05:23.343Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [AWS SQS: Building a Distributed Task Queue System in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-sqs-building-a-distributed-task-queue-system-in-the-cloud)
{.links-list}


# AWS SQS: 클라우드에 분산 작업 대기열 시스템 구축

이 기사에서는 Amazon Simple Queue Service(SQS)를 사용하여 분산 작업 대기열 시스템을 구축하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

- 작업 대기열이란 무엇입니까?
- 작업 대기열을 사용하는 이유는 무엇입니까?
- Amazon SQS란 무엇입니까?
- Amazon SQS 시작하기
- Amazon SQS로 분산 작업 대기열 구축

## 태스크 큐란?

태스크 큐는 태스크를 관리하고 처리하기 위한 시스템입니다. 작업은 이메일 보내기, 이미지 처리 또는 데이터 정리와 같이 수행해야 하는 모든 작업이 될 수 있습니다.

작업 대기열은 작업을 비동기적으로 처리하는 데 사용됩니다. 이것은 작업이 대기열에 추가된 다음 나중에 작업자에 의해 처리됨을 의미합니다. 이는 작업이 즉시 처리되는 동기식 처리와 다릅니다.

작업 대기열에는 다음과 같은 이점이 있습니다.

- 기본 응용 프로그램을 차단하지 않고 백그라운드에서 작업을 처리하는 데 사용할 수 있습니다.
- 여러 작업자를 사용하여 작업을 병렬로 처리하는 데 사용할 수 있습니다.
- 여러 컴퓨터에 작업을 배포하는 데 사용할 수 있습니다.

## 작업 대기열을 사용하는 이유는 무엇입니까?

작업 대기열을 사용하려는 이유는 많습니다. 여기 예시들이 있습니다 :

- 메인 애플리케이션을 차단하지 않고 백그라운드에서 작업을 처리하고 싶습니다.
- 여러 작업자를 사용하여 작업을 병렬로 처리하려는 경우.
- 여러 컴퓨터에 작업을 배포하려고 합니다.

작업 대기열은 다양한 작업에 사용할 수 있습니다. 예를 들어 작업 대기열을 사용하여 다음을 수행할 수 있습니다.

- 이메일 보내기
- 프로세스 이미지
- 데이터 정리
- 보고서 생성

## Amazon SQS란 무엇입니까?

Amazon Simple Queue Service(SQS)는 관리형 메시지 대기열 서비스입니다. 분산 작업 대기열 시스템을 구축하는 데 사용할 수 있습니다.

SQS는 안정적이고 확장 가능하며 비용이 저렴한 메시지 대기열 서비스입니다. 표준 및 선입선출(FIFO) 대기열을 모두 지원합니다.

## Amazon SQS 시작하기

SQS를 사용하려면 먼저 Amazon SQS 대기열을 생성해야 합니다. 이는 AWS Management Console, AWS 명령줄 인터페이스(CLI) 또는 AWS SDK를 사용하여 수행할 수 있습니다.

대기열을 만든 후에는 대기열에 메시지 추가를 시작할 수 있습니다. AWS Management Console, AWS CLI 또는 AWS SDK를 사용하여 메시지를 추가할 수 있습니다.

대기열에 메시지를 추가하면 작업자가 메시지를 처리할 수 있습니다. 작업자는 AWS Management Console, AWS CLI 또는 AWS SDK를 사용하여 생성할 수 있습니다.

## Amazon SQS로 분산 작업 대기열 구축

이 섹션에서는 Amazon SQS를 사용하여 분산 작업 대기열 시스템을 구축하는 방법을 보여줍니다. 다음 구성 요소를 사용합니다.

- 아마존 SQS
- Amazon Elastic Compute Cloud(EC2)
- Amazon 단순 알림 서비스(SNS)

또한 다음 오픈 소스 소프트웨어를 사용합니다.

- 아파치 ActiveMQ
- 아파치 낙타

### Amazon SQS 대기열 생성

첫 번째 단계는 Amazon SQS 대기열을 생성하는 것입니다. 이는 AWS Management 콘솔, AWS CLI 또는 AWS SDK를 사용하여 수행할 수 있습니다.

대기열이 생성되면 구성해야 합니다. 다음 구성 설정이 필요합니다.

- 메시지 보유 기간: 메시지가 삭제되기 전에 대기열에 남아 있는 시간입니다. 최소값은 4초이고 최대값은 14일입니다.

- 배달 지연: 메시지가 작업자에게 배달되기 전에 대기열에 남아 있는 시간입니다. 최소값은 0초이고 최대값은 15분입니다.

- 수신 핸들: 큐에서 메시지를 삭제하는 데 사용되는 토큰입니다.

- Visibility timeout: 메시지가 다른 작업자에게 표시되기 전에 대기열에 남아 있는 시간입니다. 최소값은 0초이고 최대값은 12시간입니다.

### Amazon EC2 인스턴스 생성

다음 단계는 Amazon EC2 인스턴스를 생성하는 것입니다. 이는 AWS Management 콘솔, AWS CLI 또는 AWS SDK를 사용하여 수행할 수 있습니다.

인스턴스가 생성되면 구성해야 합니다. 다음 구성 설정이 필요합니다.

- 보안 그룹: 포트 22(SSH) 및 포트 8080(HTTP)에서 인바운드 트래픽을 허용하는 보안 그룹을 생성해야 합니다.

- 키 쌍: 키 쌍을 생성하고 개인 키를 안전한 장소에 저장해야 합니다.

- IAM 역할: EC2 인스턴스가 SQS에 액세스할 수 있도록 허용하는 IAM 역할을 생성해야 합니다.

### Apache ActiveMQ 설치 및 구성

다음 단계는 Apache ActiveMQ를 설치 및 구성하는 것입니다. Apache ActiveMQ는 오픈 소스 메시지 브로커입니다.

먼저 Apache ActiveMQ를 다운로드해야 합니다. 이는 다음 명령을 사용하여 수행할 수 있습니다.

```
wget http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.8/apache-activemq-5.15.8-bin.tar.gz&action=download
```

Next, you need to extract the downloaded file. This can be done using the following command:

```
tar -xzf apache-activemq-5.15.8-bin.tar.gz
```

다음으로 ActiveMQ 디렉토리로 변경해야 합니다. 이는 다음 명령을 사용하여 수행할 수 있습니다.

```
cd apache-activemq-5.15.8/
```

다음으로 ActiveMQ 구성 파일을 편집해야 합니다. 즐겨 사용하는 텍스트 편집기를 사용하여 이 작업을 수행할 수 있습니다. 예를 들어 다음 명령을 사용할 수 있습니다.

```
nano conf/activemq.xml
```

ActiveMQ 구성 파일은 잘 문서화되어 있습니다. 설명서를 읽고 다음과 같이 변경합니다.

- ```<broker>``` element, set the ```persistent="true"``` attribute.

- In the ```<transportConnectors>``` element, add the following ```<transportConnector>``` element:

```xml
<transportConnector name="sqs" uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act" />
```

- In the ```<destinations>``` element, add the following ```<queue>``` element:

```xml
<대기열 물리적 이름="TASK_QUEUE_NAME" />
```

Replace ```TASK_QUEUE_NAME``` with the name of the Amazon SQS queue that you created earlier.

- In the ```<systemUsage>``` element, set the ```storeUsage>``` and ```tempUsage>``` elements to the following values:

```xml
<storeUsage limit="20GB"/>
<tempUsage 제한="10GB"/>
```

This will ensure that the ActiveMQ broker does not run out of storage space.

- In the ```<plugins>``` element, add the following ```<statisticsBrokerPlugin>``` element:

```xml
<statisticsBrokerPlugin/>
```

This will enable ActiveMQ broker statistics.

- Save your changes and exit the text editor.

### Starting Apache ActiveMQ

The next step is to start the Apache ActiveMQ broker. This can be done using the following command:

```
빈/activemq 시작
```

You can check that the broker is running by executing the following command:

```
빈/activemq 상태
```

You should see the following output:

```
ACTIVEMQ_HOME: /home/ec2-user/apache-activemq-5.15.8
ACTIVEMQ_DATA: /home/ec2-user/apache-activemq-5.15.8/data
브로커 URL에 연결 중: sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act
포함: queue://TASK_QUEUE_NAME
로그: Apache ActiveMQ 5.15.8(localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1)이 시작 중입니다.
위로
정보: 도움말이나 자세한 정보는 http://activemq.apache.org를 참조하십시오.
정보: http://0.0.0.0:8161/에서 사용할 수 있는 ActiveMQ WebConsole
정보: Spring 애플리케이션 컨텍스트를 닫는 중입니다.
정보: Apache ActiveMQ 5.15.8(localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1) 가동 시간
37.528초
정보: Apache ActiveMQ 5.15.8(localhost, ID:ip-10-0-1-32.ec2.internal-39767-1588389434974-0:1)은
종료
```

If the broker is not running, you can start it using the following command:

```
빈/activemq 시작
```

### Installing and configuring Apache Camel

The next step is to install and configure Apache Camel. Apache Camel is an open-source integration framework.

First, you need to download Apache Camel. This can be done using the following command:

```
wget http://www.apache.org/dyn/closer.cgi?filename=/camel/2.23.1/apache-camel-2.23.1.tar.gz&action=download
```

다음으로 다운로드한 파일을 추출해야 합니다. 이는 다음 명령을 사용하여 수행할 수 있습니다.

```
tar -xzf 아파치 낙타-2.23.1.tar.gz
```

Next, you need to change into the Camel directory. This can be done using the following command:

```
cd 아파치-낙타-2.23.1/
```

Next, you need to create a configuration file. This can be done using your favorite text editor. For example, you could use the following command:

```
나노 conf/camel.xml
```

Add the following content to the file:

```xml
<콩 xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:스키마 위치="
  http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">
 
  <camelContext id="낙타" xmlns="http://camel.apache.org/schema/spring">
    <노선>
      <from uri="sqs://ACCESS_KEY_ID:SECRET_ACCESS_KEY@sqs.us-east-1.amazonaws.com:9324?queuePrefix=act&amp;delay=5000&concurrentConsumers=5&maxMessagesPerPoll=10"/>
      <to uri="activemq:TASK_QUEUE_NAME"/>
    </경로>
  </camelContext>
</콩>
```

Replace ```ACCESS_KEY_ID``` and ```SECRET_ACCESS_KEY``` with your Amazon SQS access key id and secret access key. Replace ```TASK_QUEUE_NAME``` with the name of the Amazon SQS queue that you created earlier.

- Save your changes and exit the text editor.

### Running Apache Camel

The next step is to start Apache Camel. This can be done using the following command:

```
빈/낙타
```

You can check that Apache Camel is running by executing the following command:

```
빈/낙타 상태
```

You should see the following output:

```
 낙타가 달리지 않습니다.
```

If Apache Camel is not running, you can start it using the following command:

```
빈/낙타 시작
```

### Sending messages to the queue

The next step is to send messages to the Amazon SQS queue. This can be done using the AWS Management Console, AWS CLI, or AWS SDK.

Messages can be any JSON-formatted data. The following is an example message:

```json
{
  "작업": "send_email",
  "에": "john@example.com",
  "from": "noreply@example.com",
  "제목": "안녕하세요 존",
  "body": "안녕하세요 존,\n\n작업 대기열에서 보낸 메시지입니다."
}
```

### Processing messages

Messages in the Amazon SQS queue can be processed by workers. Workers can be created using the AWS Management Console, AWS CLI, or AWS SDK.

Workers can be any type of program, such as a web application, a command-line program, or a script. The following is an example worker written in PHP:

```php
<?php

// 메시지가 수신되었는지 확인합니다.
if (!empty($_GET['message'])) {
  // 메시지를 디코딩합니다.
  $message = json_decode($_GET['메시지']);
 
  // 메시지를 처리합니다.
  스위치 ($message->task) {
    케이스 'send_email':
      // 이메일을 보냅니다.
      mail($message->to, $message->제목, $message->body, '보낸 사람: ' . $message->from);
      부서지다;
 
    케이스 'process_image':
      // 이미지를 처리합니다.
      // ...
      부서지다;
 
    케이스 'cleanup_data':
      // 데이터를 정리합니다.
      // ...
      부서지다;
 
    케이스 'generate_report':
      // 보고서를 생성합니다.
      // ...
      부서지다;
  }
}
```

## 결론

이 기사에서는 Amazon Simple Queue Service(SQS)를 사용하여 분산 작업 대기열 시스템을 구축하는 방법을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

- 작업 대기열이란 무엇입니까?
- 작업 대기열을 사용하는 이유는 무엇입니까?
- Amazon SQS란 무엇입니까?
- Amazon SQS 시작하기
- Amazon SQS로 분산 작업 대기열 구축

질문이 있으시면 언제든지 의견에 게시하십시오.