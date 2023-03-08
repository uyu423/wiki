---
title: 051: Spring XD와 함께 Spring Boot 사용하기
description: 
published: true
date: 2023-02-04T17:32:31.131Z
tags: 
editor: markdown
dateCreated: 2023-02-04T17:32:29.560Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [051: Using Spring Boot with Spring XD***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/051-using-spring-boot-with-spring-xd)
{.links-list}


# Spring XD와 함께 Spring Boot 사용하기

Spring Boot는 Spring 애플리케이션을 빠르게 시작하고 실행할 수 있는 좋은 방법입니다. 자동 구성, 임베디드 서버 및 스타터 종속성을 포함하여 즉시 사용 가능한 많은 기능을 제공합니다.

Spring XD는 데이터 파이프라인을 구축하기 위한 도구입니다. 여러 소스에서 데이터를 수집하고 다양한 방식으로 처리하고 여러 싱크로 출력할 수 있습니다.

이번 포스팅에서는 Spring XD와 함께 Spring Boot를 사용하는 방법에 대해 알아보겠습니다. 파일에서 데이터를 수집하여 데이터베이스에 출력하는 간단한 예제부터 시작하겠습니다. 그런 다음 Spring XD의 고급 기능 중 일부를 살펴보겠습니다.

## 전제 조건

시작하기 전에 몇 가지를 설치해야 합니다.

* [자바 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [메이븐 3](https://maven.apache.org/download.cgi)
* [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/# getting-started-installing-the-cli)
* [스프링XD](https://spring.io/projects/spring-xd)

## 헬로월드

간단한 예부터 시작하겠습니다. 다음 내용으로 `data.txt`라는 파일을 만듭니다.

```
Hello, world!
```

다음으로 이 파일에서 데이터를 수집하고 콘솔에 출력하는 Spring XD 스트림을 생성합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
xd:>stream create --name hello --definition "file --dir=./ --pattern=data.txt | log" --deploy
```

이 스트림에는 파일 원본과 로그 싱크라는 두 가지 구성 요소가 있습니다. 파일 소스는 `./` 디렉터리(현재 디렉터리)에서 읽고 `data.txt` 패턴이 있는 파일을 찾도록 구성되어 있습니다. 로그 싱크는 단순히 데이터를 콘솔에 출력합니다.

다음 명령으로 실행 중인 스트림을 볼 수 있습니다.

```
xd:>stream list
```

그리고 다음 명령을 사용하여 스트림의 출력을 볼 수 있습니다.

```
xd:>log hello
```

## 데이터베이스 출력

이전 예제에서는 콘솔에 데이터를 출력했습니다. 그러나 대부분의 경우 데이터를 데이터베이스에 출력하려고 합니다. Spring XD는 `jdbc` 싱크로 이를 쉽게 만듭니다.

먼저 데이터베이스를 만들어야 합니다. 메모리에서 실행할 수 있는 경량 데이터베이스인 [H2](http://www.h2database.com/html/main.html)를 사용하겠습니다. 다음 명령으로 데이터베이스를 생성할 수 있습니다.

```
xd:>jdbc create --name mydb --url jdbc:h2:mem:mydb
```

그러면 메모리에 `mydb`라는 데이터베이스가 생성됩니다.

다음으로 이 데이터베이스에 테이블을 만들어야 합니다. 다음 SQL을 사용합니다.

```sql
CREATE TABLE messages (
  id IDENTITY,
  message VARCHAR(255)
);
```

다음 명령을 사용하여 이 SQL을 실행할 수 있습니다.

```
xd:>jdbc execute --name mydb --sql "CREATE TABLE messages (id IDENTITY, message VARCHAR(255))"
```

이제 데이터베이스와 테이블이 있으므로 이 테이블에 데이터를 출력하는 스트림을 만들 수 있습니다. 다음 명령으로 이를 수행할 수 있습니다.

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

이 스트림은 이전 스트림과 유사하지만 `log` 싱크 대신 `jdbc` 싱크가 있습니다. `jdbc` 싱크는 `mydb` 데이터베이스의 `messages` 테이블에 쓰도록 구성됩니다. 'columns' 속성은 스트림의 데이터로 채워져야 하는 테이블의 열을 지정합니다.

다음 SQL을 사용하여 데이터가 데이터베이스에 삽입되었는지 확인할 수 있습니다.

```sql
SELECT * FROM messages;
```

## 프로세서

이전 예제에서는 파일에서 데이터를 수집하고 이를 콘솔이나 데이터베이스로 출력하는 방법을 살펴보았습니다. 그러나 대부분의 경우 데이터를 출력하기 전에 어떤 방식으로든 데이터를 처리해야 합니다. Spring XD는 프로세서를 사용하여 이를 쉽게 만듭니다.

프로세서는 원하는 방식으로 데이터를 변환할 수 있습니다. 이 예에서는 데이터를 대문자로 변환하는 프로세서를 만듭니다. 다음 명령으로 이를 수행할 수 있습니다.

```
xd:>processor create --name uppercase --definition "transform --expression=payload.toUpperCase()" --deploy
```

이 프로세서에는 단일 '변환' 모듈이 있습니다. `transform` 모듈은 스트림의 각 데이터 조각에 대해 평가되는 표현식을 사용합니다. 이 경우 표현식은 데이터를 대문자로 변환하는 `payload.toUpperCase()`입니다.

이제 이 프로세서를 사용하도록 `db` 스트림을 수정할 수 있습니다.

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | uppercase | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

다음 SQL을 사용하여 데이터가 데이터베이스에 삽입되었는지 확인할 수 있습니다.

```sql
SELECT * FROM messages;
```

## 요약

이번 포스팅에서는 Spring XD와 함께 Spring Boot를 사용하는 방법에 대해 알아보았습니다. 파일에서 데이터를 수집하고 콘솔이나 데이터베이스로 출력하는 스트림을 만드는 방법을 살펴보았습니다. 그리고 데이터가 출력되기 전에 프로세서를 사용하여 데이터를 변환하는 방법을 살펴보았습니다.