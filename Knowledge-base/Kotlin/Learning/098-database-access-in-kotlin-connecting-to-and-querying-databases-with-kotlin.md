---
title: 098: Kotlin의 데이터베이스 액세스: Kotlin으로 데이터베이스 연결 및 쿼리
description: 
published: true
date: 2023-02-09T06:17:13.824Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:17:12.237Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [098: Database Access in Kotlin: Connecting to and Querying Databases with Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/Learning/098-database-access-in-kotlin-connecting-to-and-querying-databases-with-kotlin)
{.links-list}


# Kotlin의 데이터베이스 액세스: Kotlin으로 데이터베이스 연결 및 쿼리

이 게시물에서는 Kotlin을 사용하여 데이터베이스에 연결하고 쿼리하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

- 데이터베이스에 연결
- SQL 문 생성 및 실행
- 데이터베이스에서 결과 검색

## 데이터베이스에 연결

데이터베이스에 연결하려면 JDBC 드라이버를 사용해야 합니다. Kotlin에는 데이터베이스에 연결하는 데 사용할 수 있는 JDBC 드라이버가 내장되어 있습니다.

데이터베이스에 연결하려면 먼저 JDBC 연결을 생성해야 합니다. JDBC DriverManager 클래스를 사용하여 이를 수행할 수 있습니다. DriverManager 클래스는 JDBC 연결을 얻기 위한 정적 메서드를 제공합니다.

JDBC 연결이 있으면 이를 사용하여 Statement 객체를 생성할 수 있습니다. Statement 객체는 SQL 문을 실행하는 데 사용됩니다.

## SQL 문 생성 및 실행

Statement 객체가 있으면 이를 사용하여 SQL 문을 실행할 수 있습니다. SQL 문을 실행하는 데 사용할 수 있는 두 가지 방법이 있습니다.

- execute(): 이 메서드는 SQL 문을 실행하고 문이 쿼리인지 여부를 나타내는 부울 값을 반환합니다.
- executeQuery(): 이 메서드는 SQL 쿼리를 실행하고 쿼리 결과를 포함하는 ResultSet 개체를 반환합니다.

## 데이터베이스에서 결과 검색

executeQuery() 메서드를 사용하여 SQL 쿼리를 실행하면 쿼리 결과가 포함된 ResultSet 객체를 얻게 됩니다.

ResultSet 개체에는 레코드 목록이 포함되어 있습니다. 각 레코드에는 쿼리의 열 값이 포함됩니다.

ResultSet 개체를 사용하여 데이터베이스에서 레코드를 검색할 수 있습니다. next() 메서드를 사용하여 ResultSet의 다음 레코드로 이동할 수 있습니다. getString() 메서드를 사용하여 현재 레코드에서 열 값을 검색할 수 있습니다.

데이터베이스에서 레코드를 검색했으면 ResultSet 및 Statement 개체를 닫을 수 있습니다. 마지막으로 JDBC 연결을 닫을 수 있습니다.