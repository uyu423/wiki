---
title: Kotlin 및 MongoDB: 문서 지향 데이터베이스에 연결
description: 
published: true
date: 2023-02-17T18:10:54.300Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:17:29.590Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and MongoDB: Connecting to a Document-Oriented Database***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-mongodb-connecting-to-a-document-oriented-database)
{.links-list}

    
# Kotlin과 MongoDB: 문서 지향 데이터베이스에 연결하기

이 기사에서는 Kotlin에서 MongoDB 데이터베이스에 연결하는 방법을 살펴보겠습니다. MongoDB는 스키마와 함께 JSON과 유사한 문서를 사용하는 오픈 소스 문서 지향 데이터베이스 시스템입니다. 웹 애플리케이션에 널리 사용되며 많은 Kotlin 애플리케이션에 데이터를 저장하는 데에도 적합합니다.

MongoDB 설치 방법부터 살펴보겠습니다. 그런 다음 Kotlin 프로젝트를 만들어 MongoDB 데이터베이스에 연결합니다. Kotlin에서 데이터베이스를 쿼리하는 방법을 살펴보는 것으로 마무리하겠습니다.

## 몽고DB 설치

MongoDB는 Windows, MacOS 및 Linux에서 사용할 수 있습니다. [MongoDB 웹 사이트](https://www.mongodb.com/download-center#community)에서 다운로드할 수 있습니다. 운영 체제와 일치하는 버전을 다운로드하십시오.

MongoDB를 다운로드했으면 아카이브의 압축을 풀고 원하는 위치에 콘텐츠를 추출합니다. 이 기사에서는 `C:\mongodb`에 추출합니다.

다음으로 MongoDB용 데이터 디렉토리를 생성해야 합니다. 데이터 디렉토리는 MongoDB가 데이터 파일을 저장하는 곳입니다. MongoDB 설치 디렉터리에 `data`라는 새 디렉터리를 만듭니다.

이제 데이터 디렉토리가 있으므로 MongoDB를 시작할 수 있습니다. 터미널 창을 열고 MongoDB 설치 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
mongod --dbpath C:\mongodb\data
```

이 명령은 MongoDB 서버를 시작하고 `data` 디렉토리를 데이터 디렉토리로 사용하도록 지시합니다. 이제 MongoDB가 백그라운드에서 실행됩니다. 이 터미널 창은 다시 필요하지 않으므로 열어두거나 닫을 수 있습니다.

## 코틀린 프로젝트 만들기

이제 Kotlin 애플리케이션 개발을 시작할 준비가 되었습니다. 이 프로젝트에는 [Gradle](https://gradle.org/) 빌드 시스템을 사용할 것입니다. 프로젝트의 새 디렉터리를 만들고 터미널 창에서 해당 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행하여 새 Gradle 프로젝트를 만듭니다.

```
gradle init --type kotlin-library
```

이 명령은 `kotlin-library` 플러그인으로 새로운 Kotlin 프로젝트를 생성합니다. 이 플러그인은 Kotlin 라이브러리 개발에 사용됩니다. 우리는 프로젝트에 이 플러그인을 사용하지 않을 것이지만 필요한 `kotlin-stdlib` 종속성을 포함하므로 어쨌든 사용할 것입니다.

## 몽고DB에 연결하기

이제 프로젝트가 설정되었으므로 종속성 추가를 시작할 수 있습니다. 필요한 첫 번째 종속성은 MongoDB 드라이버입니다. MongoDB Driver는 Kotlin에서 MongoDB에 연결하고 쿼리할 수 있게 해주는 라이브러리입니다. [Maven Central Repository](https://mvnrepository.com/artifact/org.mongodb/mongodb-driver)에서 최신 버전의 MongoDB 드라이버를 찾을 수 있습니다.

`build.gradle` 파일에 다음을 추가합니다.

```groovy
repositories {
    jcenter()
}

dependencies {
    implementation "org.mongodb:mongodb-driver:3.12.4"
}
```

첫 번째 줄은 프로젝트에 JCenter 저장소를 추가합니다. JCenter는 널리 사용되는 많은 Java 라이브러리를 호스팅하는 저장소입니다. 두 번째 줄은 MongoDB 드라이버 종속성을 추가합니다. '3.12.4'를 최신 버전의 MongoDB 드라이버로 교체하십시오.

이제 MongoDB 드라이버 종속성이 있으므로 코드 작성을 시작할 수 있습니다. MongoDB 데이터베이스를 나타내는 `Database` 개체를 만드는 것으로 시작하겠습니다. `main.kt` 파일에 다음 코드를 추가합니다.

```kotlin
val database: Database = Database("mongodb://localhost:27017/test")
```

이 코드는 MongoDB 서버에서 `test` 데이터베이스를 나타내는 `Database` 객체를 생성합니다. `mongodb` 프로토콜은 우리가 MongoDB에 연결하고 있음을 지정합니다. `localhost` 부분은 MongoDB 서버의 호스트 이름을 지정합니다. `27017`은 MongoDB가 실행 중인 포트입니다. `test` 부분은 연결하려는 데이터베이스의 이름입니다.

## 몽고DB 쿼리

이제 `Database` 개체가 있으므로 데이터베이스 쿼리를 시작할 수 있습니다. 데이터베이스의 모든 문서를 쿼리하는 것으로 시작하겠습니다. `main.kt` 파일에 다음 코드를 추가합니다.

```kotlin
val documents: List<Document> = database.find()
```

이 코드는 모든 문서에 대해 데이터베이스를 쿼리하고 문서를 `Document` 개체 목록으로 반환합니다.

특정 문서를 쿼리할 수도 있습니다. 예를 들어 값이 `1`인 `_id` 필드가 있는 모든 문서를 쿼리할 수 있습니다. `main.kt` 파일에 다음 코드를 추가합니다.

```kotlin
val document: Document? = database.findOne(Document("_id", 1))
```

이 코드는 `_id` 필드가 `1`인 문서를 데이터베이스에 쿼리하고 이를 `Document` 개체로 반환합니다. 해당 문서가 없으면 `null`을 반환합니다.

데이터베이스에 문서를 삽입할 수도 있습니다. 예를 들어 `_id` 필드가 `1`이고 `name` 필드가 `John`인 문서를 삽입할 수 있습니다. `main.kt` 파일에 다음 코드를 추가합니다.

```kotlin
database.insertOne(Document("_id", 1).append("name", "John"))
```

이 코드는 `_id` 필드가 `1`이고 `name` 필드가 `John`인 문서를 데이터베이스에 삽입합니다.

데이터베이스에서 문서를 업데이트할 수도 있습니다. 예를 들어 방금 삽입한 문서를 업데이트하여 `name` 필드의 값이 `Jane`이 되도록 할 수 있습니다. `main.kt` 파일에 다음 코드를 추가합니다.

```kotlin
database.updateOne(Document("_id", 1), Document("\$set", Document("name", "Jane")))
```

이 코드는 `name` 필드의 값이 `Jane`이 되도록 `_id` 필드가 `1`인 문서를 업데이트합니다.

## 결론

이 기사에서는 Kotlin에서 MongoDB 데이터베이스에 연결하는 방법을 살펴보았습니다. 또한 데이터베이스에서 문서를 쿼리하고 업데이트하는 방법도 살펴보았습니다. 자세한 내용은 [MongoDB 드라이버 설명서](https://mongodb.github.io/mongo-java-driver/)를 참조하세요.