---
title: 웹 개발을 위한 Kotlin: REST API 구축
description: 
published: true
date: 2023-02-18T00:33:20.261Z
tags: 
editor: markdown
dateCreated: 2023-02-18T00:33:18.822Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin for Web Development: Building REST APIs***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-for-web-development-building-rest-apis)
{.links-list}


# 웹 개발을 위한 Kotlin: REST API 구축

Kotlin은 표현 구문, null 안전 및 Kotlin 확장을 제공하는 JVM 언어입니다. 최근 몇 년 동안 동시성 지원과 Java에 대한 보다 간결한 대안으로 인기를 얻었습니다.

이 기사에서는 REST API를 구축하여 웹 개발을 위한 Kotlin을 살펴볼 것입니다. 우리는 Ktor 프레임워크를 사용하고 다음 주제를 다룰 것입니다.

* Ktor 프로젝트 설정
* Ktor 구성
* 라우팅
* 데이터베이스 연결 생성
* 직렬화
* 테스트

## Ktor 프로젝트 설정

Gradle 빌드 시스템을 사용하여 Ktor 프로젝트를 설정하는 것으로 시작하겠습니다. `build.gradle.kts` 파일에 다음을 추가합니다.

```kotlin
plugins {
    kotlin("jvm") version "1.3.72"
    id("io.ktor.server.netty") version "1.3.2"
}

repositories {
    jcenter()
}

dependencies {
    implementation("io.ktor:ktor-server-netty:$ktor_version")
    implementation("ch.qos.logback:logback-classic:1.2.3")
    implementation("org.slf4j:slf4j-api:1.7.30")
}
```

`$ktor_version`을 최신 버전의 Ktor로 바꿉니다. 작성 당시 최신 버전은 `1.3.2`입니다.

## Ktor 구성

`Application.kt` 파일에서 Ktor를 구성합니다.

먼저 로깅 수준을 구성합니다. 기본적으로 Ktor는 'INFO' 수준에서 모든 것을 기록합니다. 프로덕션 중인 REST API의 경우 로깅 수준을 `ERROR`로 변경하려고 합니다. `Application.kt` 파일에 다음을 추가합니다.

```kotlin
import ch.qos.logback.classic.Level
import ch.qos.logback.classic.LoggerContext
import org.slf4j.LoggerFactory

// ...

fun Application.module() {
    // ...

    // Configure logging
    val context: LoggerContext = LoggerFactory.getILoggerFactory() as LoggerContext
    context.setLogLevel(Level.ERROR)
}
```

다음으로 서버가 실행될 포트를 구성합니다. 기본적으로 Ktor는 포트 '8080'에서 실행됩니다. `Application.kt` 파일에 다음을 추가하여 이를 변경할 수 있습니다.

```kotlin
import io.ktor.server.engine.ApplicationEngine
import io.ktor.server.engine.embeddedServer
import io.ktor.server.netty.Netty

// ...

fun Application.module() {
    // ...

    // Configure port
    val server: ApplicationEngine = embeddedServer(Netty, port = 8080) {
        // ...
    }
}
```

## 라우팅

Ktor에서 경로는 'routing' 블록에서 정의됩니다. `routing` 블록은 `ApplicationCall`을 매개변수로 받는 함수입니다. `ApplicationCall` 개체는 요청 및 응답에 대한 액세스를 제공합니다.

사용자 목록을 반환하는 경로를 정의하여 시작하겠습니다. `Application.kt` 파일에 다음을 추가합니다.

```kotlin
import io.ktor.application.call
import io.ktor.response.respond
import io.ktor.routing.get
import io.ktor.routing.routing

// ...

fun Application.module() {
    // ...

    // Define routes
    routing {
        get("/users") {
            val users = listOf(
                User(1, "John"),
                User(2, "Jane")
            )
            call.respond(users)
        }
    }
}
```

위의 코드에서 `User` 개체 목록을 반환하는 `GET` 경로를 정의했습니다. `User` 클래스는 다음과 같이 정의됩니다.

```kotlin
data class User(val id: Int, val name: String)
```

서버를 실행하고 `http://localhost:8080/users`에 `GET` 요청을 하여 경로를 테스트할 수 있습니다. 다음 응답을 받아야 합니다.

```json
[
    {
        "id": 1,
        "name": "John"
    },
    {
        "id": 2,
        "name": "Jane"
    }
]
```

## 데이터베이스 연결 생성

데이터베이스에 연결하기 위해 `exposed` 라이브러리를 사용할 것입니다. `exposed`는 Kotlin용 경량 SQL 라이브러리입니다.

먼저 `build.gradle.kts` 파일에 `exposed` 종속성을 추가합니다.

```kotlin
plugins {
    // ...
}

repositories {
    // ...
}

dependencies {
    // ...
    implementation("org.jetbrains.exposed:exposed-core:0.17.7")
    implementation("org.jetbrains.exposed:exposed-dao:0.17.7")
    implementation("org.jetbrains.exposed:exposed-jdbc:0.17.7")
}
```

다음으로 데이터베이스 연결을 관리하기 위해 `DatabaseFactory` 클래스를 생성합니다. `Application.kt` 파일에 다음을 추가합니다.

```kotlin
import org.jetbrains.exposed.sql.Database

class DatabaseFactory {
    companion object {
        fun init() {
            Database.connect(
                "jdbc:h2:./test",
                driver = "org.h2.Driver"
            )
        }
    }
}
```

위의 코드에서 `init` 함수를 포함하는 `Companion Object`로 `DatabaseFactory` 클래스를 정의했습니다. `init` 함수는 `Database.connect` 함수를 사용하여 데이터베이스 연결을 생성합니다.

`Application.kt` 파일에 다음을 추가하여 데이터베이스 연결을 테스트할 수 있습니다.

```kotlin
import org.jetbrains.exposed.sql.selectAll
import org.jetbrains.exposed.sql.transactions.transaction

// ...

fun main() {
    DatabaseFactory.init()
    transaction {
        println("Users:")
        User.selectAll().forEach {
            println("${it.id}: ${it.name}")
        }
    }
}
```

위의 코드에서는 `exposed` 라이브러리에서 `selectAll` 및 `transaction` 함수를 가져왔습니다. 또한 `DatabaseFactory` 클래스에서 `init` 함수를 호출하는 `main` 함수도 추가했습니다.

`main` 함수에는 `transaction` 블록도 포함되어 있습니다. `트랜잭션` 블록은 SQL 문을 실행하는 데 사용됩니다. `transaction` 블록에서 `User` 테이블의 모든 행을 반환하는 `SELECT` 문을 정의했습니다.

서버를 실행하고 `http://localhost:8080/users`에 `GET` 요청을 만들어 코드를 테스트할 수 있습니다. 다음 응답을 받아야 합니다.

```json
[
    {
        "id": 1,
        "name": "John"
    },
    {
        "id": 2,
        "name": "Jane"
    }
]
```

## 직렬화

Kotlin은 직렬화를 기본적으로 지원합니다. `@Serializable` 주석을 사용하여 데이터 클래스를 직렬화할 수 있습니다.

먼저 `build.gradle.kts` 파일에 `kotlin-serialization` 플러그인을 추가합니다.

```kotlin
plugins {
    // ...
    kotlin("plugin.serialization") version "1.3.72"
}

repositories {
    // ...
}

dependencies {
    // ...
}
```

다음으로 `@Serializable` 주석을 사용하여 `User` 클래스에 주석을 추가합니다.

```kotlin
@Serializable
data class User(val id: Int, val name: String)
```

`Application.kt` 파일에 다음을 추가하여 직렬화를 테스트할 수 있습니다.

```kotlin
import kotlinx.serialization.json.Json

// ...

fun main() {
    // ...
    transaction {
        println("Users:")
        User.selectAll().forEach {
            println(Json.encodeToString(it))
        }
    }
}
```

위의 코드에서 `kotlinx.serialization.json` 라이브러리를 추가하고 `Json` 클래스를 가져왔습니다. 또한 `DatabaseFactory` 클래스에서 `init` 함수를 호출하는 `main` 함수도 추가했습니다.

`main` 함수에는 `transaction` 블록도 포함되어 있습니다. `transaction` 블록에서 `User` 테이블의 모든 행을 반환하는 `SELECT` 문을 정의했습니다. 또한 `Json.encodeToString` 함수를 사용하여 `User` 개체를 직렬화하는 `println` 문을 추가했습니다.

서버를 실행하고 `http://localhost:8080/users`에 `GET` 요청을 만들어 코드를 테스트할 수 있습니다. 다음 응답을 받아야 합니다.

```json
[
    {"id":1,"name":"John"},
    {"id":2,"name":"Jane"}
]
```

## 테스트

REST API용 테스트를 작성하기 위해 `kotlintest` 라이브러리를 사용할 것입니다. 'kotlintest'는 Kotlin을 위한 유연하고 포괄적인 테스트 도구입니다.

먼저 `kotlintest` 종속성을 `build.gradle.kts` 파일에 추가합니다.

```kotlin
plugins {
    // ...
}

repositories {
    // ...
}

dependencies {
    // ...
    testImplementation("io.kotlintest:kotlintest-runner-junit5:3.4.2")
    testImplementation("io.kotlintest:kotlintest-extensions-junit5:3.4.2")
}
```

다음으로 `GET /users` 경로에 대한 테스트를 작성합니다. `ApplicationTest.kt` 파일에 다음을 추가합니다.

```kotlin
import io.ktor.server.testing.withTestApplication
import org.junit.jupiter.api.Test
import kotlintest.specs.StringSpec
import org.jetbrains.exposed.sql.transactions.transaction

@Test
class ApplicationTest : StringSpec() {
    init {
        "should return list of users" {
            withTestApplication {
                DatabaseFactory.init()
                transaction {
                    // given
                    val users = listOf(
                        User(1, "John"),
                        User(2, "Jane")
                    )

                    // when
                    val response = handleRequest {
                        uri = "/users"
                        method = HttpMethod.Get
                    }.response

                    // then
                    response.status() shouldBe HttpStatusCode.OK
                    response.content shouldBe Json.encodeToString(users)
                }
            }
        }
    }
}
```

위의 코드에서는 `ktor-server-testing` 및 `kotlintest` 라이브러리에서 `withTestApplication`, `transaction`, `handleRequest` 및 `response` 함수를 가져왔습니다. `Json` 클래스도 가져왔습니다.

`kotlintest` 라이브러리에서 `StringSpec` 클래스를 확장하는 `ApplicationTest` 클래스를 정의했습니다. `ApplicationTest` 클래스에는 `사용자 목록을 반환해야 함` 테스트가 포함되어 있습니다.

`should return list of users` 테스트에는 `withTestApplication` 블록이 포함되어 있습니다. `withTestApplication` 블록을 사용하면 애플리케이션을 따로 테스트할 수 있습니다.

`withTestApplication` 블록에서 `DatabaseFactory` 클래스의 `init` 함수를 호출했습니다. 우리는 또한 `트랜잭션` 블록을 정의했습니다. `transaction` 블록에서 `given`, `when` 및 `then` 섹션을 정의했습니다.

`given` 섹션에서 `User` 개체 목록을 정의했습니다. `when` 섹션에서 `/users` 경로에 `GET` 요청을 했습니다. 'then' 섹션에서 응답 상태 코드가 '200 OK'이고 응답 본문이 JSON으로 인코딩된 'User' 개체 목록과 같다고 주장했습니다.

`test` Gradle 작업을 실행하여 테스트를 실행할 수 있습니다. 다음 출력이 표시됩니다.

```
$ ./gradlew test

> Task :test
Users:
1: John
2: Jane

io.ktor.server.testing.ApplicationTest > should return list of users STANDARD_OUT
    Users:
    1: John
    2: Jane

io.ktor.server.testing.ApplicationTest > should return list of users PASSED

Executed 1 tests in 0.002s

> Task :test PASSED

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/6.5/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 0s
3 actionable tasks: 2 executed, 1 up-to-date
```

## 결론

이 기사에서는 REST API를 빌드하여 웹 개발을 위한 Kotlin을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

* Ktor 프로젝트 설정
* Ktor 구성
* 라우팅
* 데이터베이스 연결 생성
* 직렬화
* 테스트

Kotlin에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

* [코틀린 문서](https://kotlinlang.org/docs/reference/)
* [Ktor 문서](https://ktor.io/docs/introduction.html)
* [노출된 문서](https://github.com/JetBrains/Exposed/wiki)
* [코틀린테스트 문서](https://github.com/kotlintest/kotlintest/tree/master/doc)