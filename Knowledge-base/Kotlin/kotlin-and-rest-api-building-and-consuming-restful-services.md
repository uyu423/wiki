---
title: Kotlin 및 REST API: RESTful 서비스 구축 및 사용
description: 
published: true
date: 2023-02-18T02:32:31.651Z
tags: 
editor: markdown
dateCreated: 2023-02-18T02:32:24.839Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and REST API: Building and Consuming RESTful Services***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-rest-api-building-and-consuming-restful-services)
{.links-list}


# Kotlin 및 REST API: RESTful 서비스 구축 및 사용

Kotlin은 JVM(Java Virtual Machine)에서 실행되고 JavaScript 소스 코드로 컴파일될 수 있는 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin은 JetBrains에서 개발했습니다.

Kotlin 프로그래밍 언어는 간결한 구문과 Java와의 상호 운용성으로 인해 최근 인기를 얻고 있습니다. 이 기사에서는 Kotlin을 사용하여 RESTful 서비스를 구축하고 사용하는 방법을 살펴보겠습니다.

## Kotlin으로 REST API 구축

Kotlin으로 간단한 REST API를 빌드하는 것부터 시작하겠습니다. [Ktor](https://ktor.io/) 웹 프레임워크를 사용하여 API를 빌드할 것입니다.

먼저 `build.gradle` 파일에 Ktor 종속성을 추가해야 합니다.

```groovy
dependencies {
    implementation "io.ktor:ktor-server-core:1.3.2"
    implementation "io.ktor:ktor-server-netty:1.3.2"
    implementation "io.ktor:ktor-server-test:1.3.2"
}
```

다음으로 다음 코드를 사용하여 `main.kt` 파일을 만들 수 있습니다.

```kotlin
import io.ktor.application.*
import io.ktor.response.*
import io.ktor.routing.*
import io.ktor.server.engine.*
import io.ktor.server.netty.*

fun main(args: Array<String>) {
    embeddedServer(Netty, 8080) {
        routing {
            get("/") {
                call.respondText("Hello, World!")
            }
        }
    }.start(wait = true)
}
```

위의 코드에서 우리는 `routing` DSL을 사용하여 "Hello, World!"로 응답하는 경로를 정의합니다. `GET /` URL에 액세스할 때.

이제 `gradle run` 명령으로 애플리케이션을 실행하고 브라우저에서 `http://localhost:8080` URL에 액세스할 수 있습니다.

## Kotlin으로 REST API 사용

Kotlin으로 REST API를 빌드하는 방법을 살펴보았으니 이제 API를 사용하는 방법을 살펴보겠습니다. 이를 위해 [Retrofit](https://square.github.io/retrofit/) 라이브러리를 사용할 것입니다.

먼저 Retrofit 종속 항목을 `build.gradle` 파일에 추가해야 합니다.

```groovy
dependencies {
    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    implementation "com.squareup.retrofit2:converter-gson:2.9.0"
}
```

다음으로 API에 액세스하는 데 사용할 메서드를 정의하는 `Service` 인터페이스를 만들어야 합니다.

```kotlin
interface Service {
    @GET("/users/{id}")
    fun getUser(@Path("id") id: Int): Call<User>

    @POST("/users")
    fun createUser(@Body user: User): Call<User>

    @PUT("/users/{id}")
    fun updateUser(@Path("id") id: Int, @Body user: User): Call<User>

    @DELETE("/users/{id}")
    fun deleteUser(@Path("id") id: Int): Call<Void>
}
```

위의 코드에서 `/users` URL에 액세스하는 데 사용할 방법을 정의하기 위해 `@GET`, `@POST`, `@PUT` 및 `@DELETE` 주석을 사용하고 있습니다.

이제 `Retrofit` 인스턴스를 생성하고 이를 사용하여 `Service` 인스턴스를 생성할 수 있습니다.

```kotlin
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com")
    .addConverterFactory(GsonConverterFactory.create())
    .build()

val service = retrofit.create(Service::class.java)
```

이제 `service` 개체를 사용하여 API에 액세스할 수 있습니다. 예를 들어 `getUser` 메서드를 사용하여 `id = 1`인 사용자를 검색할 수 있습니다.

```kotlin
val user = service.getUser(1).execute().body()
```

## 결론

이 기사에서는 Kotlin을 사용하여 RESTful 서비스를 빌드하고 사용하는 방법을 살펴보았습니다. Kotlin은 많은 이점으로 인해 인기를 얻고 있는 간결하고 상호 운용 가능한 언어입니다.