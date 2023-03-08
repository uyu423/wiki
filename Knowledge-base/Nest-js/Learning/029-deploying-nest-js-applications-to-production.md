---
title: 029: Nest.js 애플리케이션을 프로덕션에 배포
description: 
published: true
date: 2023-02-09T18:17:35.614Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:17:33.935Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [029: Deploying Nest.js applications to production***English** document is available*](/en/Knowledge-base/Nest-js/Learning/029-deploying-nest-js-applications-to-production)
{.links-list}


# Nest.js 애플리케이션을 프로덕션에 배포

## 소개

Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 비교적 새로운 프레임워크이며 사용 편의성과 확장성으로 인해 인기를 얻고 있습니다.

Nest.js 프레임워크는 Express.js 프레임워크를 기반으로 하며 개발을 위해 JavaScript의 상위 집합인 TypeScript를 사용합니다.

Nest.js 애플리케이션은 온프레미스 서버, 클라우드 기반 서버 또는 서버리스 환경과 같은 다양한 프로덕션 환경에 배포할 수 있습니다.

이 게시물에서는 Nest.js 애플리케이션을 프로덕션 환경에 배포하는 방법에 중점을 둘 것입니다.

## 전제 조건

시작하기 전에 다음과 같은 몇 가지 사항이 필요합니다.

- Nest.js 애플리케이션. 없는 경우 Nest.js CLI를 사용하여 간단한 것을 만들 수 있습니다.
- 생산 환경. 온프레미스 서버, 클라우드 기반 서버 또는 서버리스 환경일 수 있습니다.
- 도메인 이름. 이는 선택 사항이지만 전 세계에서 애플리케이션에 액세스할 수 있도록 하려면 권장됩니다.

## 프로덕션 환경에 배포

프로덕션 환경에 Nest.js 애플리케이션을 배포하는 두 가지 주요 방법이 있습니다.

- Nest.js CLI 또는 Nest.js Deployer와 같은 Nest.js 전용 도구를 사용하여 배포.
- 수동 배포.

### Nest.js 특정 도구를 사용하여 배포

Nest.js 애플리케이션을 프로덕션 환경에 배포하는 가장 쉬운 방법은 Nest.js 관련 도구를 사용하는 것입니다.

이를 위해 사용할 수 있는 두 가지 주요 도구는 Nest.js CLI와 Nest.js Deployer입니다.

Nest.js CLI는 Nest.js 애플리케이션을 배포하는 데 사용할 수 있는 명령줄 인터페이스입니다. 글로벌 Node.js 모듈로 설치되며 온프레미스 서버, 클라우드 기반 서버 또는 서버리스 환경과 같은 다양한 프로덕션 환경에 애플리케이션을 배포하는 데 사용할 수 있습니다.

Nest.js CLI를 사용하려면 먼저 npm을 사용하여 설치해야 합니다.

```
npm install -g @nestjs/cli
```

Nest.js CLI가 설치되면 이를 사용하여 Nest.js 애플리케이션을 배포할 수 있습니다.

예를 들어 Nest.js 애플리케이션을 온프레미스 서버에 배포하려면 다음 명령을 사용합니다.

```
nest deploy --server=on-premises
```

이렇게 하면 Nest.js 애플리케이션이 온프레미스 서버에 배포됩니다.

Nest.js Deployer는 온프레미스 서버, 클라우드 기반 서버 또는 서버리스 환경과 같은 다양한 프로덕션 환경에 Nest.js 애플리케이션을 배포하는 데 사용할 수 있는 도구입니다.

Nest.js Deployer를 사용하려면 먼저 npm을 사용하여 설치해야 합니다.

```
npm install -g @nestjs/deployer
```

Nest.js Deployer가 설치되면 이를 사용하여 Nest.js 애플리케이션을 배포할 수 있습니다.

예를 들어 Nest.js 애플리케이션을 온프레미스 서버에 배포하려면 다음 명령을 사용합니다.

```
deployer deploy --server=on-premises
```

이렇게 하면 Nest.js 애플리케이션이 온프레미스 서버에 배포됩니다.

### 수동 배포

Nest.js 전용 도구를 사용하여 Nest.js 애플리케이션을 배포하지 않으려면 수동으로 배포할 수 있습니다.

Nest.js 애플리케이션을 수동으로 배포하려면 다음을 수행해야 합니다.

- Nest.js 애플리케이션을 빌드합니다.
- 프로덕션 환경에 애플리케이션을 배포합니다.

#### Nest.js 애플리케이션 구축

첫 번째 단계는 Nest.js 애플리케이션을 빌드하는 것입니다.

이렇게 하려면 Nest.js CLI를 사용해야 합니다.

Nest.js CLI는 Nest.js 애플리케이션을 빌드하는 데 사용할 수 있는 명령줄 인터페이스입니다. 글로벌 Node.js 모듈로 설치되며 온프레미스 서버, 클라우드 기반 서버 또는 서버리스 환경과 같은 다양한 프로덕션 환경을 위한 애플리케이션을 구축하는 데 사용할 수 있습니다.

Nest.js CLI를 사용하려면 먼저 npm을 사용하여 설치해야 합니다.

```
npm install -g @nestjs/cli
```

Nest.js CLI가 설치되면 이를 사용하여 Nest.js 애플리케이션을 빌드할 수 있습니다.

예를 들어 온프레미스 서버용 Nest.js 애플리케이션을 빌드하려면 다음 명령을 사용합니다.

```
nest build --server=on-premises
```

이렇게 하면 온프레미스 서버용 Nest.js 애플리케이션이 빌드됩니다.

#### 프로덕션 환경에 애플리케이션 배포

다음 단계는 애플리케이션을 프로덕션 환경에 배포하는 것입니다.

애플리케이션을 배포하는 방법은 프로덕션 환경에 따라 다릅니다.

예를 들어 온프레미스 서버에 배포하는 경우 scp와 같은 도구를 사용하여 애플리케이션 파일을 서버에 복사해야 합니다.

클라우드 기반 서버에 배포하는 경우 AWS Elastic Beanstalk와 같은 도구를 사용하여 애플리케이션을 배포해야 합니다.

서버리스 환경에 배포하는 경우 AWS Lambda와 같은 도구를 사용하여 애플리케이션을 배포해야 합니다.

## 결론

이 게시물에서는 Nest.js 애플리케이션을 프로덕션 환경에 배포하는 방법을 다루었습니다.

이를 수행하는 두 가지 주요 방법을 살펴보았습니다.

- Nest.js CLI 또는 Nest.js Deployer와 같은 Nest.js 전용 도구를 사용하여 배포.
- 수동 배포.

어떤 방법을 선택하든 사용자에게 제공하기 전에 프로덕션 환경에서 애플리케이션을 철저하게 테스트해야 합니다.