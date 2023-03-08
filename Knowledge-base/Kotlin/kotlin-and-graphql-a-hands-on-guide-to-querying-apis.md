---
title: Kotlin 및 GraphQL: API 쿼리 실습 가이드
description: 
published: true
date: 2023-02-17T18:03:28.541Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:16:17.744Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and GraphQL: A Hands-on Guide to Querying APIs***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-graphql-a-hands-on-guide-to-querying-apis)
{.links-list}


# Kotlin 및 GraphQL: API 쿼리 실습 가이드

이 기사에서는 Kotlin 및 GraphQL을 사용하여 API를 쿼리하는 방법을 직접 살펴보겠습니다. GraphQL 및 Kotlin의 몇 가지 기본 사항을 살펴본 다음 바로 API 쿼리에 대해 살펴보겠습니다.

## GraphQL이란?

GraphQL은 API용 쿼리 언어입니다. 2012년에 Facebook에서 만들었고 2015년에 오픈 소스로 공개되었습니다. GraphQL은 API에서 데이터를 쿼리하는 구조화된 방법을 제공합니다. 또한 기존 클라이언트를 손상시키지 않고 시간이 지남에 따라 API가 발전할 수 있습니다.

## 코틀린이란?

Kotlin은 JVM에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. 2011년에 JetBrains에서 만들었고 2012년에 오픈 소스로 공개되었습니다. Kotlin은 Java와 완벽하게 상호 운용되는 간결하고 읽기 쉬운 언어입니다.

## 시작하기

시작하려면 Kotlin 컴파일러와 GraphQL 라이브러리를 설치해야 합니다.

### Kotlin 컴파일러 설치

Kotlin 컴파일러는 [Kotlin 웹사이트](https://kotlinlang.org/)에서 다운로드할 수 있습니다. 최신 버전을 다운로드하고 원하는 디렉토리에 압축을 풀기만 하면 됩니다.

### GraphQL 라이브러리 설치

GraphQL 라이브러리는 [GraphQL 웹사이트](https://graphql.org/)에서 다운로드할 수 있습니다. 최신 버전을 다운로드하고 원하는 디렉토리에 압축을 풀기만 하면 됩니다.

## API 쿼리

이제 Kotlin 컴파일러와 GraphQL 라이브러리가 설치되었으므로 API 쿼리를 시작할 준비가 되었습니다.

API를 쿼리하려면 먼저 GraphQL 쿼리를 생성해야 합니다. GraphQL 쿼리는 쿼리하려는 필드를 지정하는 문자열입니다. 예를 들어 다음 쿼리는 사용자의 `id`, `name` 및 `email` 필드를 가져옵니다.

```graphql
query {
  user {
    id
    name
    email
  }
}
```

그런 다음 Kotlin 컴파일러를 사용하여 쿼리를 컴파일하고 API에 대해 실행할 수 있습니다. 다음 예에서는 이를 수행하는 방법을 보여줍니다.

```kotlin
import com.graphql.client.GraphQL

fun main() {
  val query = "query { user { id name email } }"
  val result = GraphQL.execute(query)
  println(result)
}
```

`execute` 메서드는 API에서 반환한 데이터가 포함된 `Result` 개체를 반환합니다. 이 경우 `Result` 개체에는 사용자의 `id`, `name` 및 `email` 필드가 포함됩니다.

## 결론

이 기사에서는 Kotlin 및 GraphQL을 사용하여 API를 쿼리하는 방법을 직접 살펴보았습니다. 우리는 GraphQL 및 Kotlin의 몇 가지 기본 사항을 살펴본 다음 바로 API 쿼리에 뛰어들었습니다.