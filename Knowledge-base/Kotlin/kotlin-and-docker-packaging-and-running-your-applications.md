---
title: Kotlin 및 Docker: 애플리케이션 패키징 및 실행
description: 
published: true
date: 2023-02-12T00:17:31.054Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:17:29.378Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Docker: Packaging and Running Your Applications***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-docker-packaging-and-running-your-applications)
{.links-list}


# Kotlin 및 Docker: 애플리케이션 패키징 및 실행

Kotlin은 간결한 구문과 Java와의 상호 운용성으로 인해 최근 몇 년 동안 인기를 얻은 JVM 호환 언어입니다. Docker는 개발자가 격리된 환경에서 애플리케이션을 패키징하고 실행할 수 있도록 하는 컨테이너화 플랫폼입니다.

이 기사에서는 Kotlin 애플리케이션을 Docker 컨테이너로 패키징하고 서버에서 실행하는 방법을 보여줍니다. 또한 Kotlin과 Docker를 함께 사용할 때의 몇 가지 이점에 대해서도 간략하게 설명합니다.

## Docker 컨테이너에 Kotlin 애플리케이션 패키징

Kotlin 애플리케이션을 Docker 컨테이너에 패키징하려면 기본 이미지와 필요한 종속 항목을 지정하는 `Dockerfile`을 생성해야 합니다. `openjdk:8-jdk-alpine` 이미지를 기본 이미지로 사용합니다. 이 이미지에는 OpenJDK 8 JVM 및 Alpine Linux 배포가 포함되어 있습니다. Alpine Linux는 Docker 컨테이너에 이상적인 경량 Linux 배포판입니다.

또한 `kotlin-stdlib` 종속성을 지정해야 합니다. 이 종속 항목에는 모든 Kotlin 애플리케이션에 필요한 Kotlin 표준 라이브러리가 포함되어 있습니다.

```Dockerfile
FROM openjdk:8-jdk-alpine

# Add the Kotlin standard library as a dependency
RUN apk add --no-cache kotlin-stdlib
```

다음으로 Kotlin 코드를 컨테이너에 복사해야 합니다. `/app` 디렉토리에 코드를 배치합니다.

```Dockerfile
# Copy our Kotlin code into the container
COPY src/ /app/src/
```

마지막으로 `ENTRYPOINT` 및 `CMD` 값을 지정해야 합니다. `ENTRYPOINT` 값은 컨테이너가 시작될 때 실행될 명령을 지정합니다. `CMD` 값은 `ENTRYPOINT` 명령에 전달될 인수를 지정합니다. 이 경우 `kotlinc` 명령을 사용하여 코드를 컴파일하고 `java` 명령을 사용하여 컴파일된 코드를 실행합니다.

```Dockerfile
# Specify the entrypoint and command
ENTRYPOINT ["kotlinc", "-include-runtime", "/app/src/main.kt", "-d", "/app/app.jar"]
CMD ["java", "-jar", "/app/app.jar"]
```

`-include-runtime` 인수는 `kotlinc` 컴파일러에게 컴파일된 코드에 Kotlin 런타임을 포함하도록 지시합니다. 이는 Kotlin 런타임이 `kotlin-stdlib` 종속성에 포함되지 않기 때문에 필요합니다.

## Docker 컨테이너에서 Kotlin 애플리케이션 실행

이제 `Dockerfile`이 있으므로 Docker 이미지를 빌드하고 Docker 컨테이너에서 Kotlin 애플리케이션을 실행할 수 있습니다.

먼저 Docker 이미지를 빌드해야 합니다. `docker build` 명령을 사용하여 이미지를 빌드합니다. 이미지 이름을 `kotlin-app`으로 지정하고 `latest` 태그로 태그를 지정합니다.

```console
$ docker build -t kotlin-app:latest .
```

다음으로 Docker 이미지를 실행해야 합니다. `docker run` 명령을 사용하여 이미지를 실행합니다. 또한 `-p 8080:8080` 인수를 지정하여 호스트의 포트 `8080`을 컨테이너의 포트 `8080`에 매핑합니다.

```console
$ docker run -p 8080:8080 kotlin-app:latest
```

Kotlin 애플리케이션은 현재 Docker 컨테이너에서 실행 중이며 `http://localhost:8080`에서 액세스할 수 있습니다.

## Kotlin과 Docker를 함께 사용할 때의 이점

Kotlin과 Docker를 함께 사용하면 여러 가지 이점이 있습니다.

첫째, Kotlin은 매우 간결한 언어입니다. 이는 Kotlin 코드가 동등한 Java 코드보다 훨씬 작다는 것을 의미합니다. 이미지가 작을수록 빌드 및 배포가 더 빠르기 때문에 Docker 컨테이너에 애플리케이션을 패키징할 때 중요합니다.

둘째, Kotlin은 Java와 완벽하게 상호 운용됩니다. 즉, Kotlin 코드에서 기존 Java 라이브러리를 쉽게 사용할 수 있습니다. 이는 기존 Java 애플리케이션을 Docker로 컨테이너화할 때 중요합니다.

셋째, Kotlin은 JVM 호환 언어입니다. 즉, JVM을 지원하는 모든 플랫폼에서 Kotlin 코드를 실행할 수 있습니다. 이는 기본 운영 체제에 관계없이 Docker를 지원하는 모든 플랫폼에서 컨테이너를 실행할 수 있기 때문에 Docker 컨테이너에 애플리케이션을 배포할 때 중요합니다.

## 결론

이 기사에서는 Kotlin 애플리케이션을 Docker 컨테이너에 패키징하고 서버에서 실행하는 방법을 보여주었습니다. 또한 Kotlin과 Docker를 함께 사용할 때의 몇 가지 이점에 대해서도 간략하게 논의했습니다.