---
title: Kotlin 지속적 배포: 모범 사례
description: 
published: true
date: 2023-02-12T01:17:45.746Z
tags: 
editor: markdown
dateCreated: 2023-02-12T01:17:38.975Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin Continuous Deployment: Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-continuous-deployment-best-practices)
{.links-list}


# Kotlin 지속적 배포: 모범 사례

이 문서에서는 Kotlin을 사용하는 CD(지속적인 배포)에 대한 몇 가지 모범 사례를 살펴보겠습니다. CD와 그 이점에 대한 간략한 개요로 시작한 다음 CD용 Kotlin 개발 환경을 설정하기 위한 몇 가지 팁으로 이동합니다. 마지막으로 몇 가지 구체적인 Kotlin CD 모범 사례를 살펴보겠습니다.

## 지속적 배포란 무엇입니까?

지속적인 배포는 코드 변경 사항이 코드베이스에 커밋되는 즉시 프로덕션에 자동으로 배포되는 소프트웨어 개발 관행입니다. 이는 개발 프로세스에 별도의 "배포 단계"가 없음을 의미합니다. 코드 변경 사항은 변경된 직후 프로덕션으로 푸시됩니다.

지속적인 배포는 지속적인 통합(CI)의 자연스러운 확장입니다. CI는 코드 변경 사항이 코드베이스에 커밋되자마자 자동으로 빌드되고 테스트되는 소프트웨어 개발 방법입니다. CD는 코드 변경 사항을 프로덕션에 자동으로 배포하여 한 단계 더 나아갑니다.

## 지속적 배포의 이점

연속 배포에는 기존의 "폭포" 개발 프로세스에 비해 여러 가지 이점이 있습니다.

* **빠른 피드백**: 지속적 배포를 사용하면 코드 변경 사항이 프로덕션에 자동으로 배포되므로 기존 개발 프로세스보다 훨씬 빠르게 이러한 변경 사항에 대한 피드백을 받을 수 있습니다.

* **위험 감소**: 지속적인 배포를 통해 코드베이스를 조금씩 점진적으로 변경하고 이러한 변경 사항을 빠르고 쉽게 배포할 수 있습니다. 이렇게 하면 문제를 쉽게 식별하고 수정할 수 있으며 각 변경 사항에 대해 새로운 문제가 발생할 위험이 줄어듭니다.

* **개선된 품질**: 지속적 배포를 사용하면 프로덕션에 배포하기 전에 코드에 대한 테스트 및 품질 보증 검사를 자동으로 실행할 수 있습니다. 이렇게 하면 코드의 품질을 개선하고 프로덕션으로 만드는 버그의 수를 줄이는 데 도움이 될 수 있습니다.

## 지속적 배포를 위한 Kotlin 개발 환경 설정

지속적인 배포를 위해 Kotlin 개발 환경을 설정하려면 몇 가지 작업을 수행해야 합니다.

1. **Kotlin 설치**: 먼저 개발용 컴퓨터에 Kotlin을 설치해야 합니다. [여기](https://kotlinlang.org/docs/tutorials/command-line.html)에서 사용할 수 있는 Kotlin 설치 패키지 중 하나를 사용하여 이 작업을 수행할 수 있습니다.

2. **IDE 구성**: Kotlin이 설치되면 Kotlin을 사용하도록 IDE를 구성해야 합니다. 이를 위한 단계는 사용 중인 IDE에 따라 다르지만 [여기](https://kotlinlang.org/docs/tutorials/getting-started.html# configuring-the)에서 가장 인기 있는 IDE에 대한 지침을 찾을 수 있습니다. -kotlin-플러그인).

3. **Kotlin 프로젝트 만들기**: 다음으로 Kotlin 프로젝트를 만들어야 합니다. `kotlinc` 명령줄 컴파일러를 사용하거나 IDE를 사용하여 이 작업을 수행할 수 있습니다.

4. **빌드 시스템 구성**: Kotlin 프로젝트를 생성했으면 빌드 시스템을 구성해야 합니다. Kotlin은 [Apache Maven](https://maven.apache.org/), [Gradle](https://gradle.org/) 또는 [ Kobalt](http://beust.com/kobalt)를 사용하여 컴파일할 수 있습니다. /). 각 빌드 시스템 구성에 대한 지침은 [여기](https://kotlinlang.org/docs/reference/using-maven.html), [여기](https://kotlinlang.org/docs/reference/ using-gradle.html) 및 [여기](https://kotlinlang.org/docs/reference/using-kobalt.html).

5. **지속적인 통합 서버 설정**: 마지막으로 지속적인 통합 서버를 설정해야 합니다. 코드베이스에 대한 변경 사항을 커밋할 때마다 코드를 자동으로 빌드하고 테스트하는 서버입니다. [Jenkins](https://jenkins.io/), [TeamCity](https://www.jetbrains.com/teamcity/) 및 [Bamboo](https ://www.atlassian.com/software/bamboo).

## Kotlin 지속적 배포 모범 사례

지속적인 배포를 위한 개발 환경을 설정했으므로 이제 몇 가지 구체적인 Kotlin CD 모범 사례를 살펴보겠습니다.

1. **빌드 자동화**: 첫 번째 단계는 빌드 프로세스를 자동화하는 것입니다. Jenkins, TeamCity 또는 Bamboo와 같은 CI 서버를 사용하여 이 작업을 수행할 수 있습니다.

2. **빌드 시스템 구성**: 빌드 프로세스를 자동화했으면 빌드 시스템을 구성해야 합니다. Kotlin은 Apache Maven, Gradle 또는 Kobalt를 사용하여 컴파일할 수 있습니다. 각 빌드 시스템 구성에 대한 지침은 [여기](https://kotlinlang.org/docs/reference/using-maven.html), [여기](https://kotlinlang.org/docs/reference/ using-gradle.html) 및 [여기](https://kotlinlang.org/docs/reference/using-kobalt.html).

3. **자동 테스트 작성**: 또 다른 중요한 단계는 코드에 대한 자동 테스트를 작성하는 것입니다. 이렇게 하면 코드가 예상대로 작동하는지 확인하고 버그가 생산에 들어가기 전에 버그를 잡는 데 도움이 됩니다.

4. **Continuous Delivery 파이프라인 설정**: 빌드 프로세스를 자동화하고 자동화된 테스트를 작성했으면 Continuous Delivery 파이프라인을 설정할 준비가 된 것입니다. 이는 코드베이스에 대한 변경 사항을 커밋할 때마다 코드를 자동으로 빌드, 테스트 및 배포하는 프로세스입니다.

5. **프로덕션 환경 모니터링**: 마지막으로 프로덕션 환경을 모니터링하여 코드가 예상대로 실행되는지 확인해야 합니다. 이를 위해 [New Relic](https://newrelic.com/) 및 [AppDynamics](https://www.appdynamics.com/)와 같은 다양한 도구가 있습니다.

## 결론

이 기사에서는 Kotlin을 사용한 지속적인 배포에 대한 몇 가지 모범 사례를 살펴보았습니다. CD용 개발 환경 설정과 몇 가지 특정 Kotlin CD 모범 사례를 다뤘습니다. 이러한 팁을 따르면 지속적인 배포를 최대한 활용하고 프로덕션 환경에서 코드가 항상 원활하게 실행되도록 할 수 있습니다.