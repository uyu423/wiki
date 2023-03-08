---
title: Continuous Integration
description: 
published: true
date: 2023-02-17T18:15:07.074Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:36:27.360Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Continuous Integration***English** version of this document is available*](/en/Knowledge-base/Dictionary/continuous-integration)
{.links-list}


# 개요
CI(연속 통합)는 여러 기여자의 코드 변경 사항을 공유 리포지토리에 정기적으로 병합하는 소프트웨어 개발 방법입니다. 이 프로세스는 코드베이스가 작동 상태이고 오류가 없는지 확인하는 데 도움이 됩니다. CI는 또한 개발 속도를 높이고 팀이 버그를 신속하게 식별, 감지 및 수정할 수 있도록 도와줍니다.

# 설명
지속적인 통합은 공유 리포지토리에서 여러 개발자 및 기타 기여자의 코드 변경 사항을 자주 병합하는 프로세스입니다. 이렇게 하면 모든 기여자가 동일한 버전의 코드베이스에서 작업하고 코드가 작업 상태에 있는지 확인하는 데 도움이 됩니다. CI는 일반적으로 민첩한 소프트웨어 개발에 사용되며 종종 자동화된 테스트 및 코드 검토 프로세스와 결합됩니다.

지속적 통합 프로세스는 개발자가 코드 변경 사항을 공유 저장소에 푸시할 때 시작됩니다. 이렇게 하면 코드의 오류 및 기존 코드와의 충돌을 확인하는 자동화된 빌드 프로세스가 트리거됩니다. 오류가 발견되지 않으면 빌드 프로세스는 자동 테스트를 실행하여 코드가 올바르게 작동하는지 확인합니다. 테스트가 실패하면 프로세스가 중지되고 개발자에게 경고가 표시됩니다. 테스트를 통과하면 프로세스가 계속되고 코드 변경 사항이 공유 코드베이스에 병합됩니다.

CI는 소프트웨어 개발에 필요한 시간과 노력을 줄이는 데 도움이 될 수 있습니다. 코드 변경 사항을 정기적으로 병합하고 테스트함으로써 팀은 버그가 문제가 되기 전에 신속하게 식별, 탐지 및 수정할 수 있습니다. 이를 통해 팀은 민첩성을 유지하고 개발에 필요한 시간을 단축하며 제품 품질을 개선할 수 있습니다.

# 여담
지속적인 통합은 팀과 개발 환경의 요구 사항에 따라 다양한 방식으로 구현될 수 있습니다. 일반적인 방법에는 Jenkins 또는 Travis CI와 같은 **지속적인 통합 도구**를 사용하는 것이 포함됩니다. 이러한 도구는 빌드 프로세스를 자동화하고, 테스트를 실행하고, 여러 기여자의 코드 변경 사항을 병합하도록 설계되었습니다.

또한 팀은 Git 또는 Subversion과 같은 **버전 제어 시스템**을 사용하여 코드 변경 사항을 추적할 수 있습니다. 버전 제어 시스템은 시간이 지남에 따라 변경 사항을 추적하므로 팀이 서로 다른 버전의 코드베이스를 쉽게 검토하고 비교할 수 있습니다. 이를 통해 버그를 쉽게 식별, 탐지 및 수정할 수 있습니다.

# 관련된 링크들
- [지속적 통합이란?*DigitalOcean*](https://www.digitalocean.com/community/tutorials/what-is-continuous-integration)
- [지속적인 통합 도구: Jenkins, Travis CI, CircleCI*Blog 비교 – CircleCI*](https://circleci.com/blog/continuous-integration-tools-comparing-jenkins-travis-ci-and-circleci/)
- [버전 제어 시스템: 그들은 무엇입니까?*DigitalOcean*](https://www.digitalocean.com/community/tutorials/version-control-systems-what-are-they)
{.links-list}