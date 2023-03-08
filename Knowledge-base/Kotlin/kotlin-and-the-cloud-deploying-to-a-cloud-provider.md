---
title: Kotlin과 클라우드: 클라우드 공급자에 배포
description: 
published: true
date: 2023-02-01T09:57:43.501Z
tags: 
editor: markdown
dateCreated: 2023-02-01T09:57:42.014Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and the Cloud: Deploying to a Cloud Provider***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-the-cloud-deploying-to-a-cloud-provider)
{.links-list}



Kotlin은 최신 멀티플랫폼 애플리케이션을 위한 정적으로 유형이 지정된 프로그래밍 언어입니다. Java와 100% 상호 운용 가능하며 Android, 서버 측, 웹 및 데스크톱 애플리케이션을 개발하는 데 사용할 수 있습니다.

이 기사에서는 Kotlin 애플리케이션을 클라우드 제공업체에 배포하는 방법에 중점을 둘 것입니다. 다음 주제를 다룰 것입니다.

- 클라우드 공급자란 무엇입니까?
- 클라우드 공급자를 사용하는 이유는 무엇입니까?
- 클라우드 공급자와 함께 Kotlin을 사용하는 이점
- Kotlin 애플리케이션을 클라우드 제공업체에 배포하는 방법

## 클라우드 공급자란?

클라우드 공급자는 클라우드 컴퓨팅 서비스를 제공하는 회사입니다. 이러한 서비스에는 스토리지, 컴퓨팅 성능, 네트워킹 및 소프트웨어가 포함됩니다. 가장 인기 있는 세 가지 클라우드 공급자는 Amazon Web Services(AWS), Microsoft Azure 및 Google Cloud Platform(GCP)입니다.

## 클라우드 공급자를 사용하는 이유는 무엇입니까?

클라우드 공급자를 사용하는 데는 여러 가지 이유가 있습니다. 가장 일반적인 이유는 인프라 비용을 절약하기 위해서입니다. 클라우드 공급자를 사용하면 사용한 리소스에 대해서만 비용을 지불하면 됩니다. 이는 자체 물리적 인프라를 구매하고 유지 관리하는 것보다 리소스를 사용하는 훨씬 효율적인 방법입니다.

클라우드 공급자를 사용하는 또 다른 일반적인 이유는 확장성을 향상시키기 위해서입니다. 클라우드 공급자를 사용하면 요구 사항이 변경될 때 리소스를 쉽게 추가하거나 제거할 수 있습니다. 이는 물리적 인프라에서 수행하기 훨씬 더 어렵습니다.

## 클라우드 공급자와 함께 Kotlin을 사용할 때의 이점

Kotlin은 클라우드 제공업체에 배포할 애플리케이션을 개발하는 데 탁월한 선택입니다. Kotlin은 간결하고 읽기 쉬운 언어로 복잡한 애플리케이션을 쉽게 개발할 수 있습니다. Kotlin은 또한 Java와 100% 상호 운용 가능합니다. 즉, Kotlin 애플리케이션을 개발할 때 기존의 모든 Java 라이브러리를 사용할 수 있습니다.

Kotlin에는 클라우드 기반 애플리케이션 개발을 위해 특별히 설계된 몇 가지 뛰어난 기능도 있습니다. 예를 들어 Kotlin의 코루틴을 사용하면 비동기 코드를 쉽게 작성할 수 있습니다. 이는 확장이 필요한 애플리케이션을 개발하는 데 중요합니다.

## Kotlin 애플리케이션을 클라우드 제공업체에 배포하는 방법

Kotlin 애플리케이션을 클라우드 제공업체에 배포하는 방법에는 여러 가지가 있습니다. 이 섹션에서는 가장 널리 사용되는 두 가지 방법인 명령줄 사용과 IDE 사용에 대해 설명합니다.

### 명령줄 사용

첫 번째 단계는 Kotlin 코드를 JAR 파일로 컴파일하는 것입니다. Kotlin 컴파일러를 사용하여 이 작업을 수행할 수 있습니다.

```kotlin
kotlinc my-app.kt -include-runtime -d my-app.jar
```

코드를 컴파일한 후에는 공급자의 명령줄 도구를 사용하여 클라우드 공급자에 배포할 수 있습니다. 예를 들어 AWS에 배포하려면 AWS CLI를 사용합니다.

```
aws deploy my-app.jar
```

Azure에 배포하려면 Azure CLI를 사용합니다.

```
azure deploy my-app.jar
```

GCP에 배포하려면 gcloud 도구를 사용합니다.

```
gcloud deploy my-app.jar
```

### IDE 사용

IntelliJ IDEA와 같은 IDE를 사용하는 경우 IDE의 기본 제공 도구를 사용하여 Kotlin 애플리케이션을 클라우드 제공업체에 배포할 수 있습니다.

AWS에 배포하려면 AWS Toolkit for IntelliJ IDEA를 사용할 수 있습니다. AWS Toolkit은 AWS 기능을 IDE에 추가하는 플러그인입니다. AWS Toolkit을 설치하려면 파일 > 설정 > 플러그인으로 이동하여 "AWS Toolkit"을 검색하십시오. 플러그인을 설치했으면 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 "AWS에 배포"를 선택하여 애플리케이션을 AWS에 배포할 수 있습니다.

Azure에 배포하려면 IntelliJ IDEA용 Azure 도구 키트를 사용할 수 있습니다. Azure 도구 키트는 Azure 기능을 IDE에 추가하는 플러그인입니다. Azure Toolkit을 설치하려면 파일 > 설정 > 플러그인으로 이동하여 "Azure Toolkit"을 검색합니다. 플러그인을 설치했으면 프로젝트를 마우스 오른쪽 단추로 클릭하고 "Azure에 배포"를 선택하여 Azure에 애플리케이션을 배포할 수 있습니다.

GCP에 배포하려면 IntelliJ IDEA용 Google Cloud Platform 플러그인을 사용할 수 있습니다. 플러그인을 설치하려면 파일 > 설정 > 플러그인으로 이동하여 "Google Cloud Platform"을 검색하십시오. 플러그인을 설치했으면 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 'GCP에 배포'를 선택하여 애플리케이션을 GCP에 배포할 수 있습니다.

## 결론

이 기사에서는 Kotlin 애플리케이션을 클라우드 제공업체에 배포하는 방법을 다루었습니다. 클라우드 제공업체 사용의 이점과 Kotlin을 통해 클라우드 기반 애플리케이션을 쉽게 개발하는 방법에 대해 논의했습니다. 또한 Kotlin 애플리케이션을 클라우드 제공업체에 배포하는 두 가지 방법인 명령줄 사용과 IDE 사용에 대해서도 다루었습니다.