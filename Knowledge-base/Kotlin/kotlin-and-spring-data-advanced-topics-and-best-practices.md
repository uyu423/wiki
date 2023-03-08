---
title: Kotlin 및 Spring 데이터: 고급 주제 및 모범 사례
description: 
published: true
date: 2023-02-17T18:05:03.839Z
tags: 
editor: markdown
dateCreated: 2023-01-30T13:54:44.321Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and Spring Data: Advanced Topics and Best Practices***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-advanced-topics-and-best-practices)
{.links-list}


# Kotlin 및 Spring 데이터: 고급 주제 및 모범 사례

오픈 소스 플랫폼인 Kotlin은 Java와의 다용성 및 상호 운용성으로 인해 최근 몇 년 동안 인기를 얻고 있습니다. Spring Data는 Java 애플리케이션에서 데이터베이스 액세스 계층의 개발을 용이하게 하는 일반적으로 사용되는 프레임워크입니다.

이 기사에서는 Spring Data와 함께 Kotlin을 사용하는 것과 관련된 몇 가지 고급 주제와 모범 사례를 살펴봅니다. 다음 주제를 다룰 것입니다.

- 사용자 정의 저장소 생성
- 복잡한 쿼리 작성
- 지연 로딩 처리

## 사용자 지정 저장소 만들기

Spring Data로 작업할 때 일반적인 작업 중 하나는 사용자 지정 리포지토리를 만드는 것입니다. 기본 리포지토리 인터페이스에서 지원하지 않는 작업을 수행해야 하는 경우 일반적으로 사용자 지정 리포지토리가 필요합니다.

예를 들어 30일 이상 로그인하지 않은 모든 사용자를 찾아야 하는 시나리오를 생각해 보십시오. 이는 사용자 지정 리포지토리를 만들고 필요한 쿼리를 실행하는 메서드를 추가하여 수행할 수 있습니다.

첫 번째 단계는 `JpaRepository` 인터페이스를 확장하는 새 인터페이스를 만드는 것입니다. 이 인터페이스는 사용자 지정 방법을 정의하는 데 사용됩니다.

```kotlin
interface UserRepository : JpaRepository<User, Long> {

    fun findByLastLoginLessThan(thirtyDaysAgo: LocalDateTime): List<User>
}
```

다음으로 이 인터페이스를 구현해야 합니다. `JpaRepositoryImpl` 클래스를 확장하는 새 클래스를 생성하여 이를 수행할 수 있습니다. 이 클래스에는 사용자 지정 메서드의 구현이 포함됩니다.

```kotlin
class UserRepositoryImpl : JpaRepositoryImpl<User, Long>(), UserRepository {

    override fun findByLastLoginLessThan(thirtyDaysAgo: LocalDateTime): List<User> {
        val criteriaBuilder = entityManager.criteriaBuilder
        val criteriaQuery = criteriaBuilder.createQuery(User::class.java)
        val root = criteriaQuery.from(User::class.java)

        val predicate = criteriaBuilder.lessThan(root.get("lastLogin"), thirtyDaysAgo)
        criteriaQuery.where(predicate)

        val query = entityManager.createQuery(criteriaQuery)
        return query.resultList
    }
}
```

## 복잡한 쿼리 작성

Spring Data로 작업할 때 또 다른 일반적인 작업은 복잡한 쿼리를 작성하는 것입니다. 복잡한 쿼리는 일반적으로 기본 리포지토리 메서드에서 지원하지 않는 작업을 수행해야 할 때 필요합니다.

예를 들어 30일 이상 로그인하지 않고 이메일 주소를 확인하지 않은 모든 사용자를 찾아야 하는 시나리오를 생각해 보십시오. 이는 사용자 지정 리포지토리를 만들고 필요한 쿼리를 실행하는 메서드를 추가하여 수행할 수 있습니다.

첫 번째 단계는 `JpaRepository` 인터페이스를 확장하는 새 인터페이스를 만드는 것입니다. 이 인터페이스는 사용자 지정 메서드를 정의하는 데 사용됩니다.

```kotlin
interface UserRepository : JpaRepository<User, Long> {

    fun findByLastLoginLessThanAndEmailVerificationDateIsNull(thirtyDaysAgo: LocalDateTime): List<User>
}
```

다음으로 이 인터페이스를 구현해야 합니다. `JpaRepositoryImpl` 클래스를 확장하는 새 클래스를 생성하여 이를 수행할 수 있습니다. 이 클래스에는 사용자 지정 메서드의 구현이 포함됩니다.

```kotlin
class UserRepositoryImpl : JpaRepositoryImpl<User, Long>(), UserRepository {

    override fun findByLastLoginLessThanAndEmailVerificationDateIsNull(thirtyDaysAgo: LocalDateTime): List<User> {
        val criteriaBuilder = entityManager.criteriaBuilder
        val criteriaQuery = criteriaBuilder.createQuery(User::class.java)
        val root = criteriaQuery.from(User::class.java)

        val lastLoginPredicate = criteriaBuilder.lessThan(root.get("lastLogin"), thirtyDaysAgo)
        val emailVerificationDatePredicate = criteriaBuilder.isNull(root.get("emailVerificationDate"))
        val predicate = criteriaBuilder.and(lastLoginPredicate, emailVerificationDatePredicate)

        criteriaQuery.where(predicate)

        val query = entityManager.createQuery(criteriaQuery)
        return query.resultList
    }
}
```

## 지연 로딩 처리

Spring 데이터로 작업할 때 지연 로딩을 처리할 때 발생할 수 있는 문제를 인식하는 것이 중요합니다. 지연 로딩은 필요할 때까지 데이터 로딩을 연기하는 프로세스입니다.

지연 로딩을 사용할 때 발생할 수 있는 한 가지 문제는 "세션 없음" 오류입니다. 이 오류는 트랜잭션 외부에서 데이터에 액세스할 때 발생할 수 있습니다. 이 오류를 방지하려면 데이터가 트랜잭션 내에서 액세스되는지 확인하는 것이 중요합니다.

지연 로딩을 사용할 때 발생할 수 있는 또 다른 문제는 "세션 종료" 오류입니다. 이 오류는 세션이 닫힌 후 데이터에 액세스할 때 발생할 수 있습니다. 이 오류를 방지하려면 세션을 닫기 전에 데이터에 액세스했는지 확인하는 것이 중요합니다.

요약하자면, Spring Data로 지연 로딩을 사용할 때 발생할 수 있는 문제를 인식하고 이를 방지하기 위한 조치를 취하는 것이 중요합니다.