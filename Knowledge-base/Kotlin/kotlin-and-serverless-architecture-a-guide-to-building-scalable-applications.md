---
title: Kotlin 및 서버리스 아키텍처: 확장 가능한 애플리케이션 구축 가이드
description: 
published: true
date: 2023-02-18T11:06:34.883Z
tags: 
editor: markdown
dateCreated: 2023-02-18T11:06:33.464Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Serverless Architecture: A Guide to Building Scalable Applications***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-serverless-architecture-a-guide-to-building-scalable-applications)
{.links-list}


# Kotlin 및 서버리스 아키텍처: 확장 가능한 애플리케이션 구축 가이드

최근 몇 년 동안 Kotlin은 간결한 구문과 null 안전 기능으로 인해 Android 애플리케이션 개발에 널리 사용되었습니다. 그러나 Kotlin은 모바일 개발에만 국한되지 않고 서버 측 개발에도 사용할 수 있습니다. 이 기사에서는 Kotlin을 사용하여 서버리스 애플리케이션을 개발하는 방법을 살펴보겠습니다.

## 서버리스 아키텍처란?

서버리스 아키텍처는 서버가 개발자로부터 추상화된 애플리케이션을 구축하는 방법입니다. 서버리스 애플리케이션에서 개발자는 서버 프로비저닝 또는 관리에 대해 걱정할 필요가 없습니다. 대신 애플리케이션 로직을 구축하는 데 집중할 수 있습니다.

서버리스 아키텍처를 사용하면 다음과 같은 많은 이점이 있습니다.

- 운영 비용 절감: 서버리스 아키텍처를 사용하면 사용한 리소스에 대해서만 비용을 지불하면 됩니다. 유휴 리소스에 대해 비용을 지불할 필요가 없습니다.

- 확장성 향상: 서버리스 애플리케이션은 트래픽 수요에 따라 자동으로 확장 또는 축소할 수 있습니다.

- 개선된 내결함성: 서버리스 애플리케이션은 장애에 대한 복원력을 갖도록 설계되었습니다. 애플리케이션의 한 부분이 실패해도 나머지 애플리케이션은 계속 작동할 수 있습니다.

## Kotlin 및 서버리스 아키텍처

Kotlin은 Java와의 상호 운용성, 간결한 구문 및 함수형 프로그래밍 지원으로 인해 서버리스 애플리케이션 개발에 탁월한 선택입니다.

### Java와의 상호 운용성

Kotlin의 장점 중 하나는 Java와 상호 운용이 가능하다는 것입니다. 즉, Kotlin을 사용하여 JVM에서 실행되는 애플리케이션을 개발하고 Kotlin에서 Java 코드를 호출할 수 있습니다. 이는 라이브러리 및 프레임워크의 기존 Java 에코시스템을 사용할 수 있기 때문에 서버리스 애플리케이션에 중요합니다.

### 간결한 구문

Kotlin의 간결한 구문은 Java와 동일한 결과를 얻기 위해 더 적은 코드를 작성할 수 있음을 의미합니다. 이것은 더 읽기 쉽고 유지 관리 가능한 코드로 이어질 수 있습니다.

### 함수형 프로그래밍

Kotlin은 보다 간결하고 표현력이 풍부한 코드를 작성하는 데 사용할 수 있는 함수형 프로그래밍을 지원합니다. 함수형 프로그래밍은 순수한 함수와 불변성에 중점을 두기 때문에 서버리스 애플리케이션 개발에 특히 적합합니다.

## Kotlin으로 서버리스 애플리케이션 구축

지금까지 Kotlin이 서버리스 개발에 탁월한 선택인 몇 가지 이유를 살펴보았으므로 이제 Kotlin을 사용하여 서버리스 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

[AWS Lambda](https://aws.amazon.com/lambda/) 플랫폼을 사용하여 애플리케이션을 구축할 것입니다. AWS Lambda는 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 서버리스 플랫폼입니다.

### 프로젝트 설정

먼저 새로운 Kotlin 프로젝트를 생성해야 합니다. 이를 위해 [IntelliJ IDEA](https://www.jetbrains.com/idea/) IDE를 사용합니다.

1. IntelliJ IDEA를 열고 **새 프로젝트 만들기**를 선택합니다.

2. 프로젝트 유형 목록에서 **Kotlin/JVM**을 선택하고 **다음**을 클릭합니다.

3. 프로젝트 이름을 입력하고 **마침**을 클릭합니다.

4. IntelliJ IDEA는 기본 디렉토리 구조로 새로운 Kotlin 프로젝트를 생성합니다.

### Java용 AWS SDK 추가

다음으로 AWS SDK for Java를 프로젝트에 추가해야 합니다. Java용 AWS SDK는 Java 코드에서 AWS 서비스와 상호 작용할 수 있게 해주는 라이브러리입니다.

Maven을 사용하여 AWS SDK for Java를 프로젝트에 추가할 수 있습니다. Maven은 종속성을 관리하는 데 사용할 수 있는 빌드 도구입니다.

1. **pom.xml** 파일을 열고 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>com.amazonaws</groupId>
    <artifactId>aws-java-sdk</artifactId>
    <version>1.11.585</version>
</dependency>
```

2. **pom.xml** 파일을 저장하면 IntelliJ IDEA가 Java용 AWS SDK를 다운로드하여 프로젝트에 추가합니다.

### Lambda 함수 작성

이제 Lambda 함수를 작성할 준비가 되었습니다. Lambda 함수는 이벤트에 대한 응답으로 실행할 수 있는 코드 조각입니다. 우리의 경우 애플리케이션에 HTTP 요청이 있을 때 트리거되는 Lambda 함수를 작성합니다.

1. 다음 내용으로 새 Kotlin 파일을 생성합니다.

```kotlin
import com.amazonaws.services.lambda.runtime.Context
import com.amazonaws.services.lambda.runtime.RequestHandler

class MyLambdaFunction : RequestHandler<Map<String, Any>, String> {

    override fun handleRequest(input: Map<String, Any>, context: Context): String {
        return "Hello, world!"
    }
}
```

2. 파일을 저장하면 IntelliJ IDEA가 코드를 컴파일합니다.

이제 Lambda 함수가 완성되었습니다. AWS에 배포해 보겠습니다.

### Lambda 함수 배포

AWS Lambda 콘솔을 사용하여 Lambda 함수를 배포할 수 있습니다.

1. [AWS Lambda 콘솔](https://console.aws.amazon.com/lambda/)에 로그인합니다.

2. **함수 만들기**를 클릭합니다.

3. **처음부터 작성**을 선택합니다.

4. 다음 정보를 입력합니다.

- 함수 이름: **MyLambdaFunction**

- 런타임: **자바 8**

- 핸들러: **com.example.MyLambdaFunction::handleRequest**

- 역할: **기본 Lambda 권한으로 새 역할 생성**

5. **함수 만들기**를 클릭합니다.

6. AWS Lambda는 지정한 이름으로 새 Lambda 함수를 생성합니다.

7. **작업**을 클릭하고 **.zip 파일 업로드**를 선택합니다.

8. 이전 단계에서 생성한 파일을 선택하고 **업로드**를 클릭합니다.

9. AWS Lambda가 파일을 업로드하고 Lambda 함수를 배포합니다.

10. **테스트**를 클릭하고 **테스트 이벤트 구성**을 선택하여 Lambda 함수를 테스트합니다.

11. **새 테스트 이벤트 만들기**를 클릭하고 다음 정보를 입력합니다.

- 이벤트 템플릿: **Hello World**

- 이벤트 이름: **TestEvent**

12. **만들기**를 클릭합니다.

13. AWS Lambda는 새로운 테스트 이벤트를 생성합니다.

14. **테스트**를 클릭합니다.

15. 테스트에 성공하면 다음 메시지가 표시됩니다.

```
Execution result: succeeded(logs)
```

16. **CloudWatch에서 로그 보기**를 클릭하여 Lambda 함수에 대한 로그를 봅니다.

17. 다음 로그 항목이 표시되어야 합니다.

```
START RequestId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Version: $LATEST
END RequestId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
REPORT RequestId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  Duration: xxx.xx ms Billed Duration: 100 ms     Memory Size: 128 MB Max Memory Used: 21 MB  
Hello, world!
```

## 결론

이 기사에서는 Kotlin을 사용하여 서버리스 애플리케이션을 개발하는 방법을 살펴보았습니다. 우리는 Kotlin의 Java와의 상호 운용성, 간결한 구문 및 함수형 프로그래밍 지원이 어떻게 서버리스 개발을 위한 탁월한 선택인지 확인했습니다. 또한 Kotlin에서 Lambda 함수를 작성하고 AWS에 배포하는 방법도 살펴보았습니다.