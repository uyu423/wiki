---
title: 소프트웨어 개발 064: 서버리스 아키텍처
description: 
published: true
date: 2023-02-16T17:55:54.285Z
tags: 
editor: markdown
dateCreated: 2023-02-16T17:55:52.724Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Software Development 064: Serverless Architecture***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-064-serverless-architecture)
{.links-list}


# 소프트웨어 개발 064: 서버리스 아키텍처

최근 "서버리스"라는 용어가 많은 주목을 받고 있지만 실제로는 무엇을 의미합니까?

기존 웹 애플리케이션에서 애플리케이션 코드는 서버에 배포되고 서버는 클라이언트의 요청을 처리합니다. 그러나 서버리스 애플리케이션에서는 애플리케이션 코드가 "클라우드에" 배포되고 이벤트에 대한 응답으로 실행됩니다.

서버리스 아키텍처를 사용하면 다음과 같은 많은 이점이 있습니다.

- 운영 오버헤드 감소: 서버를 관리할 필요가 없기 때문에 서버리스 애플리케이션은 유지 관리가 훨씬 쉽습니다.

- 확장성: 애플리케이션 코드는 이벤트에 대응하여 실행되므로 수요에 따라 자동으로 확장할 수 있습니다.

- 비용 효율적: 서버를 프로비저닝하고 유지 관리할 필요가 없기 때문에 서버리스 애플리케이션은 매우 비용 효율적일 수 있습니다.

이 게시물에서는 서버리스 아키텍처가 무엇이며 서버리스 애플리케이션 개발을 시작하는 방법을 살펴보겠습니다.

## 서버리스 아키텍처란?

기존 웹 애플리케이션에서 애플리케이션 코드는 서버에 배포되고 서버는 클라이언트의 요청을 처리합니다. 그러나 서버리스 애플리케이션에서는 애플리케이션 코드가 "클라우드에" 배포되고 이벤트에 대한 응답으로 실행됩니다.

서버리스 아키텍처를 사용하면 다음과 같은 많은 이점이 있습니다.

- 운영 오버헤드 감소: 서버를 관리할 필요가 없기 때문에 서버리스 애플리케이션은 유지 관리가 훨씬 쉽습니다.

- 확장성: 애플리케이션 코드는 이벤트에 대응하여 실행되므로 수요에 따라 자동으로 확장할 수 있습니다.

- 비용 효율적: 서버를 프로비저닝하고 유지 관리할 필요가 없기 때문에 서버리스 애플리케이션은 매우 비용 효율적일 수 있습니다.

## 서버리스 시작하기

서버리스 애플리케이션을 개발할 수 있는 다양한 플랫폼이 있지만 이 게시물에서는 AWS Lambda에 중점을 둘 것입니다.

AWS Lambda는 서버를 프로비저닝하거나 관리할 필요 없이 클라우드에서 코드를 실행할 수 있는 플랫폼입니다. Lambda 함수는 HTTP 요청 또는 파일 업로드와 같은 이벤트에 대한 응답으로 실행됩니다.

Lambda 함수 개발을 시작하려면 먼저 AWS 계정을 생성해야 합니다. 이 작업을 완료하면 AWS 콘솔을 사용하여 Lambda 함수를 생성할 수 있습니다.

Lambda 함수를 생성할 때 함수에 의해 실행될 코드뿐만 아니라 이름과 설명을 지정해야 합니다. Lambda 함수는 Node.js, Python 및 Java를 포함하여 지원되는 모든 언어로 작성할 수 있습니다.

Lambda 함수를 생성한 후에는 이벤트로 호출하여 테스트할 수 있습니다. 예를 들어 Node.js를 사용하는 경우 다음 이벤트로 함수를 호출할 수 있습니다.

```javascript
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

함수가 Python으로 작성된 경우 다음 이벤트로 함수를 호출할 수 있습니다.

```python
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

Lambda 함수를 테스트한 후에는 AWS Lambda 함수를 생성하여 배포할 수 있습니다.

## 결론

이 게시물에서는 서버리스 아키텍처가 무엇이며 서버리스 애플리케이션 개발을 시작하는 방법을 살펴보았습니다. 서버리스 애플리케이션은 운영 오버헤드와 비용을 줄이는 좋은 방법이 될 수 있으며 수요에 맞게 자동으로 확장할 수 있습니다.

서버리스 아키텍처에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

- [서버리스란?](https://serverless.com/learn/what-is-serverless/)

- [AWS에서 서버리스 시작하기](https://aws.amazon.com/getting-started/projects/build-serverless-applications/)

- [서버리스 아키텍처](https://martinfowler.com/articles/serverless.html)