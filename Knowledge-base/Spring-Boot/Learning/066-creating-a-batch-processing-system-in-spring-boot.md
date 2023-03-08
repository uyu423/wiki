---
title: 066: Spring Boot에서 배치 처리 시스템 만들기
description: 
published: true
date: 2023-02-05T02:32:14.133Z
tags: 
editor: markdown
dateCreated: 2023-02-05T02:32:12.575Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [066: Creating a Batch Processing System in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/066-creating-a-batch-processing-system-in-spring-boot)
{.links-list}


# 066: Spring Boot에서 일괄 처리 시스템 만들기

이번 포스트에서는 Spring Boot에서 배치 처리 시스템을 생성하는 방법에 대해 알아보겠습니다. 다음 주제를 다룹니다.

* 일괄처리란?
* 배치 처리에 Spring Boot를 사용하는 이유는 무엇입니까?
* 일괄 처리를 위한 Spring Boot 프로젝트 설정
* 배치 작업 생성
* 배치 작업 실행

## 일괄 처리란?

일괄 처리는 미리 결정된 순차적 순서로 일련의 작업을 실행하는 것입니다. 배치 작업은 일반적으로 단일 프로세스로 실행되는 작업 단위입니다. 배치 작업은 일반적으로 데이터 ETL(추출, 변환 및 로드), 데이터 정리 또는 데이터 집계와 같이 실시간 실행에 적합하지 않은 장기 실행 리소스 집약적 작업에 사용됩니다.

## 일괄 처리에 Spring Boot를 사용하는 이유는 무엇입니까?

Spring Boot는 Java 애플리케이션을 구축하는 데 널리 사용되는 프레임워크입니다. Spring 기반 애플리케이션의 개발 및 배포를 단순화하도록 설계되었습니다. Spring Boot는 배치 작업을 구성하고 실행할 수 있는 간단하고 직접적인 방법을 제공하므로 배치 처리 시스템을 구축하는 데 탁월한 선택입니다.

## 일괄 처리를 위한 Spring Boot 프로젝트 설정

일괄 처리를 위해 Spring Boot 프로젝트를 설정하려면 프로젝트에 다음 종속성을 추가해야 합니다.

* spring-boot-starter-batch - Spring Boot 배치 작업을 위한 시작 모듈입니다.
* mysql-connector-java - MySQL JDBC 드라이버입니다. MySQL을 데이터베이스로 사용하겠습니다.

## 배치 작업 생성

CSV 파일에서 데이터를 읽고 MySQL 데이터베이스에 쓰는 간단한 배치 작업을 생성합니다. 작업에는 다음 단계가 있습니다.

1. CSV 파일에서 데이터 읽기
2. 데이터 변환
3. MySQL 데이터베이스에 데이터 쓰기

## 배치 작업 실행

배치 작업을 실행하기 위해 Spring Boot 명령줄 인터페이스(CLI)를 사용합니다. CLI는 명령줄에서 Spring Boot 애플리케이션을 실행할 수 있게 해주는 도구입니다.

## 결론

이번 포스트에서는 Spring Boot에서 배치 처리 시스템을 생성하는 방법에 대해 알아보았습니다. 우리는 다음 주제를 다루었습니다.

* 일괄처리란?
* 배치 처리에 Spring Boot를 사용하는 이유는 무엇입니까?
* 일괄 처리를 위한 Spring Boot 프로젝트 설정
* 배치 작업 생성
* 배치 작업 실행