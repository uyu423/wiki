---
title: AWS 및 Azure의 서버리스 아키텍처 소개
description: 
published: true
date: 2023-03-02T08:21:36.466Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:21:29.322Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Introduction to Serverless Architecture on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/introduction-to-serverless-architecture-on-aws-and-azure)
{.links-list}
## 서버리스 아키텍처란?

서버리스 아키텍처는 서버 관리가 필요하지 않은 애플리케이션을 구축하고 실행하는 방법입니다. 이를 통해 개발자는 서버 또는 인프라 관리에 대한 걱정 없이 코드 작성에 집중할 수 있습니다. 기존 애플리케이션 아키텍처와 달리 서버리스 아키텍처는 이벤트 기반이므로 특정 이벤트가 트리거될 때만 실행됩니다.

## 서버리스 아키텍처의 이점

### 운영 비용 절감

서버리스 아키텍처는 서버 관리의 필요성을 제거하여 운영 비용을 줄입니다. 이러한 작업은 클라우드 공급자가 처리하므로 개발자는 서버 유지 관리, 확장 또는 패치에 대해 걱정할 필요가 없습니다.

### 향상된 확장성

서버리스 아키텍처는 수요에 따라 자동으로 확장됩니다. 요청 수가 증가하면 클라우드 공급자는 요청을 처리하기 위해 더 많은 리소스를 할당하고 수요가 줄어들면 할당을 해제합니다.

### 개발 주기 단축

서버리스 아키텍처는 인프라 관리를 추상화하므로 개발자는 코드 작성에만 집중할 수 있습니다. 그 결과 개발자가 인프라를 관리하고 유지하는 데 시간을 소비할 필요가 없기 때문에 개발 주기가 빨라집니다.

### 출시 기간 단축

서버리스 아키텍처를 통해 개발자는 코드를 더 빠르고 더 자주 배포할 수 있으므로 새로운 기능의 시장 출시 기간이 단축됩니다.

## AWS의 서버리스 아키텍처

Amazon Web Services(AWS)는 다양한 서버리스 서비스를 제공하는 업계 최고의 클라우드 제공업체 중 하나입니다. AWS에서 제공하는 인기 있는 서버리스 서비스는 다음과 같습니다.

### AWS 람다

AWS Lambda는 개발자가 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 컴퓨팅 서비스입니다. Java, Python, Node.js 및 C# 을 비롯한 여러 프로그래밍 언어를 지원합니다. 개발자는 코드를 작성하여 AWS Lambda에 업로드하고 서버 관리에 대한 걱정 없이 주문형으로 실행할 수 있습니다.

다음은 "Hello World" 메시지를 반환하는 간단한 AWS Lambda 함수의 예입니다.

```python
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hello World!'
    }
```

### 아마존 API 게이트웨이

Amazon API Gateway는 개발자가 API를 쉽게 생성, 게시 및 관리할 수 있는 완전관리형 서비스입니다. RESTful API 및 WebSocket API를 지원하며 개발자가 API에 대한 사용자 지정 도메인 이름을 만들 수 있습니다.

### 아마존 다이나모DB

Amazon DynamoDB는 완벽한 확장성과 함께 빠르고 예측 가능한 성능을 제공하는 완전 관리형 NoSQL 데이터베이스 서비스입니다. 수요에 따라 자동으로 확장 및 축소되는 서버리스 데이터베이스입니다.

## Azure의 서버리스 아키텍처

Microsoft Azure는 다양한 서버리스 서비스를 제공하는 또 다른 주요 클라우드 공급자입니다. Azure에서 제공하는 인기 있는 서버리스 서비스 중 일부는 다음과 같습니다.

### 애저 펑션

Azure Functions는 개발자가 서버를 관리하지 않고 주문형으로 코드를 실행할 수 있는 서버리스 컴퓨팅 서비스입니다. C# , Java, Python 및 JavaScript를 포함한 여러 프로그래밍 언어를 지원합니다. 개발자는 코드를 작성하고 Azure Functions에 업로드하고 주문형으로 실행할 수 있습니다.

다음은 "Hello World" 메시지를 반환하는 간단한 Azure 함수의 예입니다.

```csharp
public static HttpResponseMessage Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    // Parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Build response message
    var responseMessage = string.IsNullOrEmpty(name)
        ? $"Hello, "
        : $"Hello, {name}";

    return req.CreateResponse(HttpStatusCode.OK, responseMessage);
}
```

### 애저 이벤트 그리드

Azure Event Grid는 개발자가 이벤트 기반 애플리케이션을 빌드할 수 있도록 하는 이벤트 라우팅 서비스입니다. Azure Functions, Azure Logic Apps 및 Azure Event Hubs를 비롯한 여러 Azure 서비스를 지원합니다.

### 애저 코스모스 DB

Azure Cosmos DB는 원활한 확장성과 함께 빠르고 예측 가능한 성능을 제공하는 완전 관리형 NoSQL 데이터베이스 서비스입니다. 수요에 따라 자동으로 확장 및 축소되는 서버리스 데이터베이스입니다.

## 결론

서버리스 아키텍처를 사용하면 개발자가 인프라 관리 및 유지 관리에 대한 걱정 없이 코드 작성에만 집중할 수 있습니다. 운영 비용을 줄이고 확장성을 개선하며 새로운 기능의 출시 기간을 단축합니다. AWS와 Azure는 각각 AWS Lambda와 Azure Functions를 포함하여 다양한 서버리스 서비스를 제공하는 두 가지 주요 클라우드 공급자입니다.

## 외부 리소스

- [AWS 서버리스](https://aws.amazon.com/serverless/)
- [Azure 함수](https://azure.microsoft.com/en-us/services/functions/)
- [서버리스 프레임워크](https://www.serverless.com/)
- [서버리스 아키텍처란 무엇이며 언제 사용합니까?](https://www.altar.io/blog/what-is-serverless-architecture-and-when-to-use-it)