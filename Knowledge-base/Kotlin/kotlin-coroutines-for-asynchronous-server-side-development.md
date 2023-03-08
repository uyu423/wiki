---
title: 비동기 서버 측 개발을 위한 Kotlin 코루틴
description: 
published: true
date: 2023-02-04T10:17:45.290Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:17:43.650Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin Coroutines for Asynchronous Server-side Development***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-coroutines-for-asynchronous-server-side-development)
{.links-list}


# 비동기식 서버 측 개발을 위한 Kotlin 코루틴

Kotlin 코루틴은 서버 측에서 동시성을 관리하는 효율적인 방법을 제공합니다. 개발자는 코루틴을 사용하여 풍부한 사용자 경험을 제공하면서도 사용자 입력에 더 잘 반응하는 코드를 작성할 수 있습니다.

코루틴은 Kotlin 1.1에서 도입되었으며 Kotlin 1.3부터 안정적인 기능이었습니다. 코루틴 컨텍스트에서 코루틴은 기본 스레드에서 작업을 오프로드하는 데 사용할 수 있는 경량 스레드입니다. 이를 통해 개발자는 풍부한 사용자 경험을 제공하면서도 사용자 입력에 더 잘 반응하는 코드를 작성할 수 있습니다.

코루틴은 기존 Java 라이브러리와 함께 사용할 수 있으므로 비동기식 서버 측 개발을 위한 훌륭한 도구가 됩니다. 이 기사에서는 Java 웹 애플리케이션에서 코루틴을 사용하는 방법을 살펴보겠습니다.

## 프로젝트 설정

간단한 Maven 프로젝트를 설정하는 것으로 시작하겠습니다. `pom.xml`에 다음 종속성을 추가합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.jetbrains.kotlin</groupId>
        <artifactId>kotlin-stdlib-jdk8</artifactId>
        <version>1.3.72</version>
    </dependency>
    <dependency>
        <groupId>org.jetbrains.kotlinx</groupId>
        <artifactId>kotlinx-coroutines-core</artifactId>
        <version>1.3.7</version>
    </dependency>
</dependencies>
```

우리는 Kotlin 1.3.72와 Kotlinx 코루틴 1.3.7을 사용하고 있습니다. `kotlin-stdlib-jdk8` 종속성에는 Kotlin 표준 라이브러리가 포함되며 `kotlinx-coroutines-core` 종속성은 핵심 코루틴 기능을 제공합니다.

## 코루틴 만들기

코루틴은 `kotlinx.coroutines` 패키지의 `launch` 또는 `async` 기능을 사용하여 생성할 수 있습니다. `launch` 함수는 새로운 코루틴을 생성하고 즉시 시작합니다. `async` 함수는 새로운 코루틴을 생성하지만 즉시 시작하지는 않습니다. 대신 나중에 코루틴을 시작하는 데 사용할 수 있는 `Deferred` 클래스의 인스턴스를 반환합니다.

예를 들어, `launch` 함수를 사용하여 1초 동안 대기하는 코루틴을 만들 수 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    launch {
        // Suspend this coroutine for one second
        delay(1000)
        println("Hello, world!")
    }
}
```

`async` 함수를 사용하여 코루틴을 만들 수도 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    val deferred = async {
        // Suspend this coroutine for one second
        delay(1000)
        println("Hello, world!")
    }
    // Start the coroutine
    deferred.start()
}
```

`launch` 함수는 일시 중단 함수로, 다른 코루틴 내에서 사용할 수 있음을 의미합니다. `async` 함수는 정지 함수가 아니므로 코루틴 내에서만 사용할 수 있습니다.

## 코루틴 취소

코루틴은 `cancel` 함수를 사용하여 취소할 수 있습니다. 이 함수는 코루틴이 `CancellationException`을 발생시키도록 합니다.

예를 들어, `cancel` 함수를 사용하여 1초 동안 자고 있는 코루틴을 취소할 수 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    val deferred = launch {
        try {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        } catch (e: CancellationException) {
            println("Coroutine was cancelled")
        }
    }
    // Cancel the coroutine after half a second
    delay(500)
    deferred.cancel()
}
```

## 타임아웃

코루틴은 `withTimeout` 함수를 사용하여 시간 초과될 수 있습니다. 이 함수는 코루틴이 지정된 시간 내에 완료되지 않으면 `TimeoutCancellationException`을 발생시킵니다.

예를 들어 `withTimeout` 함수를 사용하여 1초 동안 잠자는 코루틴을 타임아웃할 수 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    try {
        withTimeout(500) {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        }
    } catch (e: TimeoutCancellationException) {
        println("Coroutine timed out")
    }
}
```

## 예외 처리

코루틴은 `supervisorScope` 함수를 사용하여 감독할 수 있습니다. 이 함수는 코루틴에 의해 발생한 모든 예외를 포착하고 나머지 코드를 계속 실행합니다.

예를 들어, `supervisorScope` 함수를 사용하여 1초 동안 잠자고 있는 코루틴을 감독할 수 있습니다.

```kotlin
import kotlinx.coroutines.*

fun main() {
    supervisorScope {
        val deferred = launch {
            // Suspend this coroutine for one second
            delay(1000)
            println("Hello, world!")
        }
        // Cancel the coroutine after half a second
        delay(500)
        deferred.cancel()
    }
}
```

## 비동기 웹 애플리케이션

코루틴은 비동기 웹 애플리케이션을 작성하는 데 사용할 수 있습니다. 이 섹션에서는 Java 웹 애플리케이션에서 코루틴을 사용하는 방법을 살펴보겠습니다.

코루틴을 사용하여 1초 동안 휴면하는 간단한 서블릿을 만드는 것으로 시작하겠습니다.

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Create a new coroutine
        launch {
            // Suspend this coroutine for one second
            delay(1000)
            // Send a response to the client
            resp.getWriter().println("Hello, world!");
        }
    }
}
```

이 서블릿에서는 `launch` 함수를 사용하여 새로운 코루틴을 생성합니다. 이 코루틴은 1초 동안 대기한 다음 클라이언트에 응답을 보냅니다.

새로운 코루틴을 생성하기 위해 `async` 함수를 사용할 수도 있습니다. 그러나 이 경우 코루틴을 수동으로 시작해야 합니다.

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Create a new coroutine
        val deferred = async {
            // Suspend this coroutine for one second
            delay(1000)
            // Send a response to the client
            resp.getWriter().println("Hello, world!");
        }
        // Start the coroutine
        deferred.start()
    }
}
```

이 서블릿에서는 `async` 함수를 사용하여 새 코루틴을 만듭니다. 이 코루틴은 1초 동안 대기한 다음 클라이언트에 응답을 보냅니다. 우리는 `start` 함수를 사용하여 코루틴을 시작합니다.

코루틴을 타임 아웃하기 위해 `withTimeout` 함수를 사용할 수도 있습니다:

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        try {
            // Time out the coroutine after 500 milliseconds
            withTimeout(500) {
                // Create a new coroutine
                launch {
                    // Suspend this coroutine for one second
                    delay(1000)
                    // Send a response to the client
                    resp.getWriter().println("Hello, world!");
                }
            }
        } catch (e: TimeoutCancellationException) {
            // Send a timeout response to the client
            resp.getWriter().println("Request timed out");
        }
    }
}
```

이 서블릿에서는 `withTimeout` 함수를 사용하여 코루틴을 시간 초과합니다. 코루틴이 500밀리초 이내에 완료되지 않으면 취소되고 시간 초과 응답이 클라이언트에 전송됩니다.

`supervisorScope` 함수를 사용하여 코루틴을 감독하는 것도 가능합니다:

```java
@WebServlet("/sleep")
public class SleepServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // Supervisor the coroutine
        supervisorScope {
            val deferred = launch {
                // Suspend this coroutine for one second
                delay(1000)
                // Send a response to the client
                resp.getWriter().println("Hello, world!");
            }
            // Cancel the coroutine after half a second
            delay(500)
            deferred.cancel()
        }
    }
}
```

이 서블릿에서는 `supervisorScope` 기능을 사용하여 코루틴을 감독합니다. 이 코루틴은 0.5초 후에 취소되지만 서블릿의 나머지 코드는 실행됩니다.

## 결론

Kotlin 코루틴은 서버 측에서 동시성을 관리하는 효율적인 방법을 제공합니다. 기존 Java 라이브러리와 함께 사용할 수 있으므로 비동기식 서버 측 개발을 위한 훌륭한 도구가 됩니다.