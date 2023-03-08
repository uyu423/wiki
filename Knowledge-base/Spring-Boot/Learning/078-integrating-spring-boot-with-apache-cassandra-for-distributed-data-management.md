---
title: 078: 분산 데이터 관리를 위해 Apache Cassandra와 Spring Boot 통합
description: 
published: true
date: 2023-02-05T09:32:41.421Z
tags: 
editor: markdown
dateCreated: 2023-02-05T09:32:39.727Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [078: Integrating Spring Boot with Apache Cassandra for Distributed Data Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/078-integrating-spring-boot-with-apache-cassandra-for-distributed-data-management)
{.links-list}


# 078: 분산 데이터 관리를 위해 Apache Cassandra와 Spring Boot 통합

## 소개

이번 포스트에서는 [Spring Boot](https://spring.io/projects/spring-boot)와 [Apache Cassandra](http://cassandra.apache.org/)를 통합하는 방법에 대해 알아보겠습니다. 데이터 관리.

Cassandra는 확장성이 뛰어난 NoSQL 데이터베이스로 대규모 데이터 저장 및 관리에 매우 적합합니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 인기 있는 Java 프레임워크입니다.

## 카산드라 개요

Cassandra는 고가용성과 확장성을 위해 설계된 NoSQL 데이터베이스입니다. 대규모 데이터 저장 및 관리에 널리 사용되는 선택입니다.

Cassandra는 [마스터리스](https://en.wikipedia.org/wiki/Masterless_architecture) 데이터베이스이므로 단일 실패 지점이 없습니다. 데이터는 Cassandra 클러스터의 여러 노드에 복제되며 각 노드는 [시드 노드](http://docs.datastax.com/en/cassandra/3.x/cassandra/initialize/initializeSingleDS.html) 역할을 할 수 있습니다. 다른 노드.

Cassandra는 또한 [선형 확장 가능](https://en.wikipedia.org/wiki/Linear_scalability)합니다. 즉, 클러스터에 더 많은 노드를 추가하여 증가하는 로드를 처리할 수 있습니다.

## 카산드라 데이터 모델

Cassandra는 [열 중심](https://en.wikipedia.org/wiki/Column-oriented_DBMS) 데이터 모델을 사용합니다. 데이터는 관계형 데이터베이스의 테이블과 유사한 [열 계열](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlAboutDataModels.html)로 구성됩니다.

각 컬럼 패밀리에는 데이터 행을 고유하게 식별하는 데 사용되는 [기본 키](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlPrimaryKeyConcept.html)가 있습니다. 기본 키는 하나 이상의 [열](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlColumns.html)로 구성됩니다.

Cassandra는 또한 [보조 인덱스](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlIndexesConcept.html)를 지원합니다. 기본 키의 일부가 아닙니다.

## 카산드라 쿼리 언어

Cassandra는 CQL(Cassandra Query Language)이라는 [SQL과 유사한 쿼리 언어](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlSelect.html)를 사용합니다. Cassandra 데이터베이스의 데이터를 업데이트합니다.

CQL은 SQL과 유사하지만 완전히 호환되는 SQL 데이터베이스는 아닙니다. CQL과 SQL 사이에는 Cassandra로 작업할 때 알아야 할 몇 가지 [차이점](http://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlCommandsTOC.html)이 있습니다.

## 스프링 부트 개요

[Spring Boot](https://spring.io/projects/spring-boot)는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 인기 있는 Java 프레임워크입니다.

Spring Boot는 널리 사용되는 Java 애플리케이션 프레임워크인 [Spring 프레임워크](https://spring.io/projects/spring-framework)를 기반으로 합니다. Spring Boot를 사용하면 [기본 구성](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html)을 제공하여 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. ) 및 [시작 종속성](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-maven-guides.html# getting-started-with-maven-dependency-management ) 다양한 응용 프로그램을 만드는 데 사용할 수 있습니다.

## 스프링 부트와 카산드라

Spring Boot를 사용하면 Cassandra와 쉽게 [통합](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html# boot-features-nosql-cassandra) . Spring Boot는 [Cassandra 자동 구성](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html#boot-features-nosql-cassandra)을 제공합니다. Cassandra 데이터베이스를 구성하고 연결하는 데 사용할 수 있습니다.

Spring Boot는 사용할 수 있는 [CassandraTemplate](https://docs.spring.io/spring-data/cassandra/docs/current/api/org/springframework/data/cassandra/core/CassandraTemplate.html) 객체도 제공합니다. Cassandra 데이터베이스에서 데이터를 쿼리하고 업데이트합니다.

## 시작하기

이 섹션에서는 Spring Boot 및 Cassandra를 시작하는 방법을 살펴보겠습니다. [Spring Initializr](https://start.spring.io/)를 사용하여 새로운 Spring Boot 프로젝트를 생성하는 것으로 시작하겠습니다.

프로젝트에 다음 종속성을 추가해야 합니다.

- 웹 - 애플리케이션에 웹 서버를 추가하는 데 사용됩니다.
- Cassandra - Cassandra 데이터베이스에 연결하는 데 사용됩니다.

또한 프로젝트에 다음 Maven 종속 항목을 추가해야 합니다.

- [Cassandra 드라이버](https://mvnrepository.com/artifact/org.apache.cassandra/cassandra-driver-core) - Cassandra 데이터베이스에 연결하는 데 사용됩니다.
- [Cassandra Unit](https://mvnrepository.com/artifact/org.cassandraunit/cassandra-unit) - Cassandra 코드를 단위 테스트하는 데 사용됩니다.

## 카산드라 설정

이 섹션에서는 Spring Boot 애플리케이션에 대해 Cassandra를 구성하는 방법을 살펴보겠습니다.

먼저 [Cassandra 구성](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# cassandra-configuration) 파일을 프로젝트에 추가합니다. 이 파일은 Cassandra 연결을 구성하는 데 사용됩니다.

구성 파일에서 다음 속성을 설정해야 합니다.

- `cassandra.contact-points` - 애플리케이션이 Cassandra 클러스터에 연결하는 데 사용할 Cassandra 접점
- `cassandra.port` - Cassandra 클러스터가 실행 중인 포트
- `cassandra.keyspace-name` - 애플리케이션에서 사용할 키스페이스의 이름
- `cassandra.username` - 애플리케이션이 Cassandra에 연결하는 데 사용할 사용자 이름입니다.
- `cassandra.password` - 애플리케이션이 Cassandra에 연결하는 데 사용할 비밀번호

## 카산드라 엔터티 생성

이 섹션에서는 [Cassandra 엔터티](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# cassandra-mapping-entity) 클래스를 만드는 방법을 살펴보겠습니다. .

Cassandra 엔터티는 [JPA 엔터티](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# orm-support.jpa.entity)와 유사합니다. Cassandra 테이블을 Java 클래스에 매핑하는 데 사용됩니다.

Cassandra 엔터티 클래스에 `@Table` 주석을 추가해야 합니다. 이 주석은 엔터티가 매핑될 Cassandra 테이블의 이름을 지정하는 데 사용됩니다.

또한 엔티티 클래스에 `@PrimaryKeyClass` 주석을 추가해야 합니다. 이 주석은 엔티티의 기본 키 클래스를 지정하는 데 사용됩니다.

기본 키 클래스는 각 기본 키 열에 대해 `@PrimaryKeyColumn` 주석을 추가해야 합니다. 이 주석은 열의 이름과 기본 키에서 사용될 순서를 지정하는 데 사용됩니다.

## 카산드라 리포지토리 생성

이 섹션에서는 [Cassandra 저장소](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# repositories.query-methods.details)를 만드는 방법을 살펴보겠습니다. ) 상호 작용.

Cassandra 리포지토리는 [JPA 리포지토리](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# repositories)와 유사합니다. Cassandra 데이터베이스의 데이터에 액세스하는 데 사용됩니다.

Cassandra 리포지토리 인터페이스에 `@Repository` 주석을 추가해야 합니다. 이 주석은 인터페이스를 Spring Data 저장소로 표시하는 데 사용됩니다.

또한 `@CassandraRepository` 주석으로 리포지토리 인터페이스에 주석을 달아야 합니다. 이 주석은 인터페이스를 Cassandra 저장소로 표시하는 데 사용됩니다.

리포지토리 메서드에서 `@Query` 주석을 사용하여 CQL 쿼리를 지정할 수 있습니다. 또한 `@Param` 주석을 사용하여 메소드 매개변수를 CQL 쿼리 매개변수에 바인딩할 수 있습니다.

## 단위 테스트 카산드라 코드

이 섹션에서는 Cassandra 코드를 단위 테스트하는 방법을 살펴보겠습니다.

`@RunWith(CassandraUnitRunner.class)` 주석으로 테스트 클래스에 주석을 달면서 시작하겠습니다. 이 주석은 Cassandra Unit 실행기로 단위 테스트를 실행하는 데 사용됩니다.

또한 테스트 클래스에 `@CassandraDataSet` 주석을 추가해야 합니다. 이 주석은 Cassandra 데이터 세트를 테스트 환경에 로드하는 데 사용됩니다.

`@EmbeddedCassandra` 주석을 사용하여 단위 테스트를 위해 임베디드 Cassandra 서버를 시작할 수 있습니다. 또한 `@SharedEmbeddedCassandra` 주석을 사용하여 단위 테스트를 위한 공유 임베디드 Cassandra 서버를 시작할 수 있습니다.

## 결론

이 게시물에서는 분산 데이터 관리를 위해 Spring Boot를 Cassandra와 통합하는 방법을 살펴보았습니다. Cassandra 데이터 모델과 쿼리 언어를 살펴보는 것으로 시작했습니다. 그런 다음 Spring Boot 및 Cassandra를 시작하는 방법을 살펴보았습니다.

그런 다음 Spring Boot 애플리케이션에 대해 Cassandra를 구성하는 방법을 살펴보았습니다. 또한 Cassandra 엔터티 클래스와 Cassandra 저장소 인터페이스를 만드는 방법도 살펴보았습니다.

마지막으로 Cassandra 코드를 단위 테스트하는 방법을 살펴보았습니다.