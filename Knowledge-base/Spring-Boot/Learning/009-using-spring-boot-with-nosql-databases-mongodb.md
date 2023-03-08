---
title: 009: NoSQL 데이터베이스(MongoDB)에서 Spring Boot 사용
description: 
published: true
date: 2023-02-03T08:36:55.375Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:36:50.437Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [009: Using Spring Boot with NoSQL databases (MongoDB)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/009-using-spring-boot-with-nosql-databases-mongodb)
{.links-list}


# NoSQL 데이터베이스(MongoDB)와 함께 Spring Boot 사용

이 게시물에서는 널리 사용되는 NoSQL 데이터베이스인 MongoDB와 함께 Spring Boot를 사용하는 방법을 살펴보겠습니다.

다음 주제를 다룹니다.

* 몽고DB란?
* Spring Boot에서 MongoDB를 사용하는 이유는 무엇입니까?
* 몽고디비 설정
* MongoDB로 Spring Boot 애플리케이션 만들기
* 결론

## 몽고DB란?

MongoDB는 강력한 문서 지향 NoSQL 데이터베이스입니다. 인덱스 기반 검색 기능과 유연한 스키마가 있습니다. MongoDB는 확장하기 쉽고 고성능과 확장성으로 유명합니다.

## Spring Boot에서 MongoDB를 사용하는 이유는 무엇입니까?

Spring Boot는 웹 애플리케이션 구축에 널리 사용되는 Java 프레임워크입니다. Spring 프레임워크 위에 구축되어 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

MongoDB는 설정 및 사용이 쉽기 때문에 Spring Boot와 함께 사용하기에 적합합니다. MongoDB는 또한 쉽게 확장할 수 있으며 이는 성장이 예상되는 애플리케이션에 중요합니다.

## 몽고DB 설정

Spring Boot와 함께 MongoDB를 사용하기 전에 설정해야 합니다.

MongoDB를 설정하는 방법에는 두 가지가 있습니다.

* MongoDB Atlas와 같은 호스팅 서비스 사용
* 로컬에 MongoDB 설치

아래에서 두 가지 옵션을 모두 다룰 것입니다.

### MongoDB Atlas와 같은 호스팅 서비스 사용

MongoDB를 설정하는 가장 쉬운 방법은 MongoDB Atlas와 같은 호스팅 서비스를 사용하는 것입니다. MongoDB Atlas는 클라우드 호스팅 MongoDB 서비스입니다. 설정 및 사용이 쉽습니다.

MongoDB Atlas를 사용하려면 계정을 만들고 클러스터를 설정해야 합니다. 클러스터는 데이터를 저장하는 데 사용되는 MongoDB 서버 그룹입니다.

계정을 만들고 클러스터를 설정했으면 사용자를 만들어야 합니다. 사용자는 Spring Boot 애플리케이션에서 MongoDB 데이터베이스에 연결하는 데 사용됩니다.

사용자를 생성한 후 연결 문자열을 가져와야 합니다. 연결 문자열은 Spring Boot 애플리케이션을 MongoDB 데이터베이스에 연결하는 데 사용됩니다.

### 로컬에 MongoDB 설치

MongoDB를 로컬에 설치하려면 MongoDB 웹 사이트의 지침을 따르십시오.

MongoDB를 설치했으면 데이터베이스를 생성해야 합니다. 데이터베이스는 Spring Boot 애플리케이션에서 데이터를 저장하는 데 사용됩니다.

데이터베이스를 생성한 후 사용자를 생성해야 합니다. 사용자는 Spring Boot 애플리케이션에서 MongoDB 데이터베이스에 연결하는 데 사용됩니다.

사용자를 생성한 후 연결 문자열을 가져와야 합니다. 연결 문자열은 Spring Boot 애플리케이션을 MongoDB 데이터베이스에 연결하는 데 사용됩니다.

## MongoDB로 Spring Boot 애플리케이션 만들기

이제 MongoDB가 설정되었으므로 MongoDB를 사용하는 Spring Boot 애플리케이션을 만들 수 있습니다.

새로운 Spring Boot 애플리케이션을 생성하는 것으로 시작하겠습니다. "spring-boot-mongodb"라고 하겠습니다.

다음으로 프로젝트에 다음 종속성을 추가합니다.

* spring-boot-starter-data-mongodb: 이 종속성은 MongoDB 데이터베이스에 연결하는 데 사용됩니다.
* spring-boot-starter-web: 이 종속성은 웹 애플리케이션을 만드는 데 사용됩니다.

또한 application.properties 파일에 다음 속성을 추가해야 합니다.

spring.data.mongodb.uri=mongodb://localhost/spring-boot-mongodb

이 속성은 MongoDB 데이터베이스에 대한 연결을 구성하는 데 사용됩니다.

다음으로 모델 클래스를 만듭니다. 이 클래스는 데이터를 나타내는 데 사용됩니다. "사용자"라고 하겠습니다.

User 클래스에는 다음 필드가 있습니다.

* id: 사용자의 아이디입니다. 이 필드는 MongoDB에서 생성됩니다.
* 이름: 사용자의 이름입니다.
* 이메일: 사용자의 이메일입니다.

다음으로 리포지토리 인터페이스를 만듭니다. 이 인터페이스는 데이터에 액세스하는 데 사용됩니다. 우리는 그것을 "UserRepository"라고 부를 것입니다.

UserRepository 인터페이스는 MongoRepository 인터페이스를 확장합니다. MongoRepository 인터페이스는 CRUD 작업을 위한 메서드를 제공합니다.

다음으로 컨트롤러를 만듭니다. 이 컨트롤러는 웹 요청을 처리하는 데 사용됩니다. 우리는 그것을 "UserController"라고 부를 것입니다.

UserController 클래스에는 다음과 같은 메서드가 있습니다.

* getAllUsers: 이 메서드는 모든 사용자를 가져오는 데 사용됩니다.
* createUser: 이 메서드는 사용자를 생성하는 데 사용됩니다.
* getUser: 이 메서드는 id로 사용자를 가져오는 데 사용됩니다.
* updateUser: 이 메서드는 사용자를 업데이트하는 데 사용됩니다.
* deleteUser: 이 메서드는 사용자를 삭제하는 데 사용됩니다.

마지막으로 서비스 클래스를 만듭니다. 이 클래스는 비즈니스 로직에 사용됩니다. "UserService"라고 하겠습니다.

UserService 클래스에는 다음과 같은 메서드가 있습니다.

* getAllUsers: 이 메서드는 모든 사용자를 가져오는 데 사용됩니다.
* createUser: 이 메서드는 사용자를 생성하는 데 사용됩니다.
* getUser: 이 메서드는 id로 사용자를 가져오는 데 사용됩니다.
* updateUser: 이 메서드는 사용자를 업데이트하는 데 사용됩니다.
* deleteUser: 이 메서드는 사용자를 삭제하는 데 사용됩니다.

## 결론

이 게시물에서는 MongoDB와 함께 Spring Boot를 사용하는 방법을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

* 몽고DB란?
* Spring Boot에서 MongoDB를 사용하는 이유는 무엇입니까?
* 몽고디비 설정
* MongoDB로 Spring Boot 애플리케이션 만들기