---
title: Nest.js 시작하기
description: 
published: true
date: 2023-01-29T19:48:13.627Z
tags: 
editor: markdown
dateCreated: 2023-01-29T19:48:13.627Z
---


# 소개

[Nest](https://nestjs.com/)는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. 프로그레시브 JavaScript를 사용하고 TypeScript로 구축되어 완벽하게 지원하며(그래도 개발자는 순수 JavaScript로 코딩할 수 있음) 테스트 기반 개발을 강력하게 지원합니다.

이 기사에서는 MongoDB 데이터베이스로 간단한 CRUD 애플리케이션을 만들어 Nest.js를 시작하는 방법을 살펴보겠습니다.

# Nest.js 프로젝트 설정

가장 먼저 해야 할 일은 Nest.js CLI를 설치하는 것입니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm i -g @nestjs/cli
```

완료되면 다음 명령을 실행하여 새 Nest.js 프로젝트를 만들 수 있습니다.

```
nest new <project-name>
```

# 몽고DB 데이터베이스 생성

우리는 데이터베이스로 MongoDB를 사용할 것입니다. MongoDB가 설치되어 있지 않은 경우 [여기](https://docs.mongodb.com/manual/installation/)의 지침을 따를 수 있습니다.

MongoDB가 설치되면 MongoDB 셸에서 다음 명령을 실행하여 새 데이터베이스를 만들 수 있습니다.

```
use <database-name>
```

# Nest.js 컨트롤러 만들기

이제 Nest.js 프로젝트 설정과 MongoDB 데이터베이스가 있으므로 CRUD 애플리케이션 생성을 시작할 수 있습니다.

Nest.js 컨트롤러를 만드는 것으로 시작하겠습니다. Nest.js에서 컨트롤러는 들어오는 요청을 처리하고 응답을 반환하는 일을 담당합니다.

컨트롤러를 생성하기 위해 다음 명령을 실행할 수 있습니다.

```
nest generate controller <controller-name>
```

#Nest.js 서비스 만들기

Nest.js에서 서비스는 비즈니스 로직을 캡슐화하는 데 사용됩니다. 컨트롤러 및 기타 서비스에 주입할 수 있습니다.

서비스를 생성하기 위해 다음 명령을 실행할 수 있습니다.

```
nest generate service <service-name>
```

# Nest.js 모듈 생성

Nest.js 모듈은 컨트롤러, 서비스 및 파이프와 같은 관련 구성 요소를 그룹화하는 데 사용됩니다.

모듈을 생성하기 위해 다음 명령을 실행할 수 있습니다.

```
nest generate module <module-name>
```

# 결론

이 기사에서는 MongoDB 데이터베이스로 간단한 CRUD 애플리케이션을 만들어 Nest.js를 시작하는 방법을 살펴보았습니다. Nest.js 프로젝트를 설정하여 시작한 다음 컨트롤러, 서비스 및 모듈을 만들었습니다.