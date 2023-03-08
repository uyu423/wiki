---
title: Kotlin 및 Spring 데이터: 데이터베이스와 통합
description: 
published: true
date: 2023-02-07T00:55:23.444Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:55:17.802Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Spring Data: Integrating with a Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-integrating-with-a-database)
{.links-list}


# 코틀린과 스프링 데이터: 데이터베이스와 통합

Kotlin은 간결한 구문과 Java와의 상호 운용성으로 인해 최근 몇 년 동안 인기를 얻은 JVM 언어입니다. Spring Data는 Spring 애플리케이션에서 데이터 작업을 위한 강력한 도구입니다. 이 기사에서는 Kotlin 및 Spring Data를 사용하여 데이터베이스 작업을 수행하는 방법을 살펴봅니다.

데이터베이스 엔터티를 나타내는 Kotlin 데이터 클래스를 만드는 것으로 시작하겠습니다. 그런 다음 데이터를 관리하기 위해 Spring Data Repository 인터페이스를 생성합니다. 우리는 JpaRepository로 이 인터페이스를 구현할 것입니다. 마지막으로 저장소를 사용하여 데이터를 쿼리하고 업데이트합니다.

## 데이터 클래스 만들기

데이터베이스 엔터티를 나타내는 Kotlin 데이터 클래스를 만드는 것으로 시작하겠습니다. 클래스를 `User`라고 합니다. 우리의 `User` 클래스에는 `id`, `name` 및 `email`의 세 가지 속성이 있습니다.


```kotlin
data class User(
        val id: Long,
        val name: String,
        val email: String
)
```

## 저장소 생성

다음으로 데이터를 관리하기 위해 Spring Data Repository 인터페이스를 생성합니다. 우리는 인터페이스를 `UserRepository`라고 부를 것입니다. 우리의 `UserRepository`는 `JpaRepository`를 확장하고 `User` 데이터 클래스로 매개변수화됩니다.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

## 저장소 구현

`JpaRepository`로 `UserRepository` 인터페이스를 구현할 것입니다. Kotlin `Application` 클래스에 `JpaRepository`를 삽입합니다.

```kotlin
@SpringBootApplication
class Application {

    @Autowired
    lateinit var userRepository: UserRepository

    fun main(args: Array<String>) {
        SpringApplication.run(Application::class.java, *args)
    }
}
```

## 저장소 쿼리

이제 `UserRepository`가 있으므로 이를 사용하여 데이터베이스를 쿼리할 수 있습니다. 데이터베이스에서 모든 사용자를 찾는 것부터 시작하겠습니다.

```kotlin
val users = userRepository.findAll()
```

`id`로 사용자를 찾을 수도 있습니다.

```kotlin
val user = userRepository.findById(1L)
```

## 사용자 업데이트

`UserRepository`를 사용하여 데이터베이스에서 `User`를 업데이트할 수 있습니다. 업데이트할 사용자를 찾는 것부터 시작하겠습니다. 그런 다음 `name` 및 `email` 속성을 업데이트합니다. 마지막으로 변경 사항을 저장합니다.

```kotlin
val user = userRepository.findById(1L)

user.name = "John Doe"
user.email = "john.doe@example.com"

userRepository.save(user)
```

## 사용자 삭제

`UserRepository`를 사용하여 데이터베이스에서 `User`를 삭제할 수 있습니다. 삭제할 사용자를 찾는 것부터 시작하겠습니다. 그런 다음 데이터베이스에서 삭제합니다.

```kotlin
val user = userRepository.findById(1L)

userRepository.delete(user)
```

## 결론

이 기사에서는 Kotlin 및 Spring Data를 사용하여 데이터베이스 작업을 수행하는 방법을 살펴보았습니다. 데이터베이스 엔터티를 나타내는 Kotlin 데이터 클래스를 만들었습니다. 또한 데이터를 관리하기 위해 Spring Data Repository 인터페이스를 만들었습니다. JpaRepository로 이 인터페이스를 구현했습니다. 마지막으로 저장소를 사용하여 데이터를 쿼리하고 업데이트했습니다.