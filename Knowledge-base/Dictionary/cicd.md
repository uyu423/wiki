---
title: CI/CD
description: 
published: true
date: 2023-02-26T19:32:36.485Z
tags: 
editor: markdown
dateCreated: 2023-02-26T19:32:35.120Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [CI/CD***English** document is available*](/en/Knowledge-base/Dictionary/cicd)
{.links-list}


# 개요
CI/CD(지속적인 통합/지속적인 배포)는 소프트웨어 개발자가 코드 변경 사항을 빠르고 안정적으로 빌드, 테스트 및 배포할 수 있도록 하는 일련의 도구 및 사례입니다. DevOps 및 Agile 소프트웨어 개발 프로세스의 핵심 구성 요소입니다.

# 설명
지속적 통합(CI)은 여러 개발자의 코드 변경 사항을 정기적으로 단일 코드베이스로 병합하는 방법입니다. 이 프로세스는 일반적으로 개발자가 소스 코드 리포지토리에 대한 변경 사항을 커밋할 때 자동화되고 트리거됩니다. 그런 다음 자동화된 테스트를 사용하여 코드 변경으로 인해 기존 기능이 중단되지 않는지 확인합니다.

CD(Continuous Delivery)는 프로덕션 시스템에 대한 코드 변경 배포를 자동화하는 방법입니다. 이 프로세스에는 일반적으로 릴리스 패키지 생성, 이에 대한 자동화된 테스트 실행, 패키지를 프로덕션 시스템에 배포하는 작업이 포함됩니다.

CI/CD는 CI와 CD 관행의 조합입니다. 코드 변경 사항을 빌드, 테스트 및 배포하는 프로세스를 자동화하여 빠르고 안정적인 소프트웨어 개발이 가능하도록 설계되었습니다. 또한 일관되고 신뢰할 수 있는 방식으로 코드 변경 사항을 테스트하고 생산 시스템에 배포하는 데 도움이 됩니다.

# 특징
CI/CD에는 일반적으로 다음 단계가 포함됩니다.

1. 소스 코드는 소스 코드 저장소에 체크인됩니다.
2. 자동화된 빌드 프로세스가 트리거되고 코드가 컴파일되고 테스트됩니다.
3. 자동화된 테스트를 실행하여 코드 변경으로 인해 기존 기능이 중단되지 않는지 확인합니다.
4. 코드는 릴리스 패키지로 패키지됩니다.
5. 릴리스 패키지는 추가 테스트를 위해 스테이징 환경에 배포됩니다.
6. 릴리스 패키지가 프로덕션 시스템에 배포됩니다.

# 예
CI/CD 프로세스의 예는 다음과 같습니다.

1. 개발자는 코드 변경 사항을 소스 코드 리포지토리에 커밋합니다.
2. 자동화된 빌드 프로세스가 트리거되고 코드가 컴파일되고 테스트됩니다.
3. 자동화된 테스트를 실행하여 코드 변경으로 인해 기존 기능이 중단되지 않는지 확인합니다.
4. 코드가 릴리스 패키지로 패키징되어 스테이징 환경에 배포됩니다.
5. 릴리스 패키지는 스테이징 환경에서 테스트됩니다.
6. 릴리스 패키지가 프로덕션 시스템에 배포됩니다.

# 장점과 단점
CI/CD의 주요 이점은 다음과 같습니다.

- 소프트웨어 개발 프로세스를 자동화하고 간소화합니다.
- 코드 변경 사항이 일관되고 안정적인 방식으로 테스트 및 배포되도록 보장합니다.
- 개발자가 프로덕션 시스템에 코드 변경 사항을 빠르고 안정적으로 배포할 수 있습니다.

CI/CD의 주요 단점은 다음과 같습니다.

- 설정 및 유지 관리가 어려울 수 있습니다.
- 일이 잘못되면 디버그 및 문제 해결이 어려울 수 있습니다.
- 기존 시스템 및 프로세스와 통합하기 어려울 수 있습니다.

# 관련 기술
CI/CD는 다음과 같은 다른 DevOps 및 Agile 소프트웨어 개발 사례와 밀접한 관련이 있습니다.

- IaC(Infrastructure as Code): 코드를 사용하여 인프라를 관리하고 프로비저닝하는 방식입니다.
- 구성 관리: 코드를 사용하여 시스템 구성을 관리하는 방법.
- 테스트 자동화: 코드를 사용하여 소프트웨어 테스트를 자동화하는 방식입니다.
- 지속적인 모니터링: 코드를 사용하여 시스템 성능을 모니터링하는 방식입니다.

# 기타
CI/CD는 최신 소프트웨어 개발의 필수 부분이며 조직이 고객 요구에 보다 민첩하고 대응하기 위해 노력함에 따라 점점 더 인기를 얻고 있습니다. 또한 조직이 클라우드 네이티브 아키텍처 및 마이크로서비스 기반 아키텍처로 이동함에 따라 점점 더 중요해지고 있습니다.