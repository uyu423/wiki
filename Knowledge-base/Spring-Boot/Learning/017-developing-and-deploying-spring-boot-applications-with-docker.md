---
title: 017: Docker를 사용하여 Spring Boot 애플리케이션 개발 및 배포
description: 
published: true
date: 2023-02-03T10:04:55.334Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:04:53.785Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [017: Developing and deploying Spring Boot applications with Docker***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/017-developing-and-deploying-spring-boot-applications-with-docker)
{.links-list}


# Docker로 Spring Boot 애플리케이션 개발 및 배포

Docker는 Spring Boot 애플리케이션 개발 및 배포 프로세스를 크게 단순화할 수 있는 도구입니다. 이 게시물에서는 Docker를 사용하여 Spring Boot 애플리케이션을 개발하고 배포하는 방법을 살펴보겠습니다.

## Docker로 Spring Boot 애플리케이션 개발

Docker로 Spring Boot 애플리케이션을 개발하는 것은 매우 간단합니다. 텍스트 편집기와 Dockerfile만 있으면 됩니다.

Dockerfile은 Docker 이미지를 빌드하는 데 필요한 모든 명령이 포함된 텍스트 파일입니다. Docker 이미지는 애플리케이션을 실행하는 데 필요한 모든 파일과 종속성을 포함하는 파일입니다.

Dockerfile을 만들려면 프로젝트의 루트 디렉터리에 `Dockerfile`이라는 새 파일을 만듭니다. 그런 다음 파일에 다음 줄을 추가합니다.

```
FROM java:8

ADD . /app

WORKDIR /app

RUN ./gradlew build

EXPOSE 8080

CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]
```

첫 번째 줄 `FROM java:8`은 Docker가 `java:8` Docker 이미지를 애플리케이션의 기본 이미지로 사용하도록 지시합니다. `java:8` Docker 이미지에는 Java 8 애플리케이션에 필요한 모든 파일과 종속성이 포함되어 있습니다.

두 번째 줄, `ADD . /app`, 현재 디렉터리(`./`)의 모든 파일을 Docker 이미지의 `/app` 디렉터리에 추가하도록 Docker에 지시합니다.

세 번째 행인 `WORKDIR /app`은 Docker가 `/app` 디렉토리를 애플리케이션의 작업 디렉토리로 사용하도록 지시합니다.

네 번째 줄 `RUN ./gradlew build`는 Docker가 `./gradlew build` 명령을 실행하여 애플리케이션을 빌드하도록 지시합니다. 이 명령은 코드를 컴파일하고 `build/libs` 디렉토리에 `.jar` 파일을 생성합니다.

다섯 번째 줄인 `EXPOSE 8080`은 Docker가 애플리케이션에 대해 포트 `8080`을 노출하도록 지시합니다.

여섯 번째이자 마지막 줄인 `CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]`는 Docker에게 다음과 같이 `java` 명령을 실행하도록 지시합니다. `-jar` 옵션과 `spring-boot-app-0.0.1-SNAPSHOT.jar` 파일을 인수로 사용합니다. 그러면 포트 `8080`에서 애플리케이션이 시작됩니다.

이제 Dockerfile이 있으므로 애플리케이션용 Docker 이미지를 빌드할 수 있습니다. 이렇게 하려면 터미널을 열고 프로젝트의 루트 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
$ docker build -t spring-boot-app .
```

이 명령은 애플리케이션의 Docker 이미지를 빌드하고 `spring-boot-app` 이름으로 태그를 지정합니다.

이미지가 빌드되면 다음 명령을 사용하여 이미지를 실행할 수 있습니다.

```
$ docker run -p 8080:8080 spring-boot-app
```

이 명령은 이미지에 대한 Docker 컨테이너를 시작하고 호스트 머신의 포트 '8080'을 컨테이너의 포트 '8080'에 매핑합니다.

이제 `http://localhost:8080`에서 애플리케이션에 액세스할 수 있습니다.

## Docker를 사용하여 Spring Boot 애플리케이션 배포

Docker를 사용하여 Spring Boot 애플리케이션을 배포하는 것은 애플리케이션을 개발하는 것만큼 간단합니다. Dockerfile과 docker-compose.yml 파일만 있으면 됩니다.

docker-compose.yml 파일은 다중 컨테이너 애플리케이션을 관리하는 데 사용할 수 있는 도구인 docker-compose에 필요한 모든 구성이 포함된 YAML 파일입니다.

docker-compose.yml 파일을 만들려면 프로젝트의 루트 디렉터리에 `docker-compose.yml`이라는 새 파일을 만듭니다. 그런 다음 파일에 다음 줄을 추가합니다.

```
version: '2'

services:
  app:
    build: .
    ports:
      - "8080:8080"
```

첫 번째 줄 `version: '2'`는 docker-compose가 docker-compose 파일 형식의 버전 2를 사용하도록 지시합니다.

두 번째 줄인 `services:`는 서비스를 정의할 것임을 docker-compose에 알려줍니다. 서비스는 다중 컨테이너 애플리케이션의 일부인 컨테이너입니다.

세 번째 줄인 `app:`은 우리 서비스의 이름입니다.

네 번째 줄인 `build: .`는 docker-compose에게 현재 디렉터리(`./`)의 `Dockerfile`을 사용하여 서비스를 빌드하도록 지시합니다.

다섯 번째이자 마지막 줄인 `ports: - "8080:8080"`은 호스트 머신의 포트 `8080`을 컨테이너의 포트 `8080`에 매핑하도록 docker-compose에 지시합니다.

이제 docker-compose.yml 파일이 있으므로 다음 명령을 사용하여 애플리케이션을 배포할 수 있습니다.

```
$ docker-compose up
```

이 명령은 포트 `8080`에서 애플리케이션을 시작합니다.

## 결론

이 게시물에서는 Docker를 사용하여 Spring Boot 애플리케이션을 개발하고 배포하는 방법을 살펴보았습니다. Docker는 Spring Boot 애플리케이션 개발 및 배포 프로세스를 크게 단순화할 수 있습니다.