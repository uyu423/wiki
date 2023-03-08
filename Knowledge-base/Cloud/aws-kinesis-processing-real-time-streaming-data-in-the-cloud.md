---
title: AWS Kinesis: 클라우드에서 실시간 스트리밍 데이터 처리
description: 
published: true
date: 2023-02-14T04:55:38.228Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:55:36.660Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Kinesis: Processing Real-Time Streaming Data in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-kinesis-processing-real-time-streaming-data-in-the-cloud)
{.links-list}

      

# AWS Kinesis: 클라우드에서 실시간 스트리밍 데이터 처리

실시간 데이터 처리는 모든 조직에게 복잡하고 어려운 작업입니다. 여러 소스에서 데이터를 수집하고, 해당 데이터를 유용한 정보로 변환하고, 해당 정보를 정확한 시간에 정확한 사람에게 전달해야 합니다. 이 모든 작업을 신속하고 정확하게 수행하는 동시에 프로세스에서 데이터가 손실되거나 손상되지 않도록 해야 합니다.

AWS Kinesis는 대규모 실시간 스트리밍 데이터를 쉽게 처리할 수 있는 클라우드 기반 플랫폼입니다. Kinesis는 여러 소스에서 동시에 데이터를 수집하고 여러 Amazon EC2 인스턴스를 병렬로 사용하여 처리할 수 있습니다. 이를 통해 많은 양의 데이터를 빠르고 정확하게 처리할 수 있습니다.

Kinesis는 관리형 서비스이므로 AWS가 인프라와 확장을 관리합니다. 이렇게 하면 Kinesis를 쉽게 시작할 수 있으며 자체 서버를 프로비저닝하고 유지 관리할 필요가 없습니다. Kinesis도 서버리스이므로 사용한 리소스에 대해서만 비용을 지불하면 됩니다.

## AWS Kinesis 시작하기

AWS Kinesis를 시작하려면 먼저 스트림을 생성해야 합니다. 스트림은 샤드 그룹을 나타내는 논리적 엔터티입니다. 샤드는 데이터를 저장하고 처리하는 데 사용할 수 있는 데이터 저장 단위입니다.

AWS Management Console, AWS 명령줄 인터페이스(CLI) 또는 AWS SDK를 사용하여 스트림을 생성할 수 있습니다.

스트림을 만든 후에는 데이터 수집을 시작할 수 있습니다. 로그 파일, 애플리케이션 이벤트, 소셜 미디어 스트림 및 센서 데이터와 같은 여러 소스에서 데이터를 수집할 수 있습니다.

Kinesis Data Streams는 샤드당 초당 최대 1MB의 속도로 데이터를 수집할 수 있습니다. 더 높은 속도로 데이터를 수집해야 하는 경우 스트림의 샤드 수를 늘릴 수 있습니다.

데이터가 스트림으로 수집되면 Kinesis Data Analytics, Kinesis Data Firehose 또는 사용자 지정 애플리케이션을 사용하여 처리할 수 있습니다.

Kinesis Data Analytics는 스트리밍 데이터를 실시간으로 쉽게 분석할 수 있는 완전관리형 서비스입니다. Kinesis Data Analytics를 사용하여 집계, 필터링, 조인과 같은 복잡한 데이터 변환을 수행할 수 있습니다.

Kinesis Data Firehose는 스트리밍 데이터를 Amazon S3, Amazon Redshift 및 Amazon Elasticsearch Service와 같은 AWS 데이터 스토어로 쉽게 로드할 수 있게 해주는 완전관리형 서비스입니다.

사용자 지정 애플리케이션을 사용하여 스트림의 데이터를 처리할 수도 있습니다. 사용자 지정 애플리케이션은 모든 프로그래밍 언어로 작성할 수 있으며 Amazon EC2, Amazon ECS 또는 AWS Lambda에 배포할 수 있습니다.

## 스트림에서 데이터 처리

Kinesis Data Streams는 샤드라는 개념을 사용하여 확장성과 성능을 제공합니다. 샤드는 데이터를 저장하고 처리하는 데 사용할 수 있는 데이터 저장 단위입니다.

Kinesis Data Streams는 수평으로 확장되도록 설계되었습니다. 즉, 스트림의 샤드 수를 늘려 처리량을 늘릴 수 있습니다.

스트림의 데이터는 여러 Amazon EC2 인스턴스에서 병렬로 처리됩니다. 각 인스턴스는 스트림에 있는 하나 이상의 샤드에서 데이터를 처리합니다.

Kinesis Data Streams는 파티션 키를 사용하여 스트림의 모든 샤드에 데이터를 고르게 배포합니다. 파티션 키는 데이터 레코드가 할당될 샤드를 결정하는 데 사용되는 데이터 레코드의 속성입니다.

데이터가 스트림으로 수집되면 Kinesis Data Streams는 파티션 키를 사용하여 데이터를 수집할 샤드를 결정합니다. Kinesis Data Streams는 또한 파티션 키를 사용하여 데이터 레코드를 처리할 인스턴스를 결정합니다.

스트림의 데이터 레코드는 수신된 순서대로 처리됩니다. 그러나 데이터가 여러 샤드에 분산되어 있기 때문에 데이터 레코드가 처리되는 순서가 보장되지 않습니다.

특정 순서로 데이터 레코드를 처리해야 하는 경우 데이터 레코드의 시퀀스 번호 속성을 사용할 수 있습니다. 데이터 레코드가 스트림으로 수집될 때 Kinesis Data Streams에서 시퀀스 번호를 할당합니다.

동일한 파티션 키를 가진 데이터 레코드는 시퀀스 번호에 따라 순서대로 처리됩니다. 그러나 파티션 키가 다른 데이터 레코드는 순서 없이 처리될 수 있습니다.

## 결론

AWS Kinesis는 대규모 실시간 스트리밍 데이터를 처리하기 위한 강력한 플랫폼입니다. Kinesis는 여러 소스에서 동시에 데이터를 수집하고 여러 Amazon EC2 인스턴스를 병렬로 사용하여 처리할 수 있습니다. 이를 통해 많은 양의 데이터를 빠르고 정확하게 처리할 수 있습니다.

Kinesis는 관리형 서비스이므로 AWS가 인프라와 확장을 관리합니다. 이렇게 하면 Kinesis를 쉽게 시작할 수 있으며 자체 서버를 프로비저닝하고 유지 관리할 필요가 없습니다. Kinesis도 서버리스이므로 사용한 리소스에 대해서만 비용을 지불하면 됩니다.

## 더 읽을거리

- [AWS Kinesis Data Streams 개발자 가이드](https://docs.aws.amazon.com/kinesis/latest/datastreams/developer-guide.html)
- [AWS Kinesis Data Analytics 개발자 가이드](https://docs.aws.amazon.com/kinesisanalytics/latest/java/getting-started.html)
- [AWS Kinesis Data Firehose 개발자 가이드](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)