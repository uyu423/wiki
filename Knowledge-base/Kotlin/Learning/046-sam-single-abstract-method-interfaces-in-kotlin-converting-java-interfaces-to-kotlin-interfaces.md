---
title: 046: Kotlin의 SAM(Single Abstract Method) 인터페이스: Java 인터페이스를 Kotlin 인터페이스로 변환
description: 
published: true
date: 2023-02-05T21:55:17.906Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:55:16.376Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [046: SAM (Single Abstract Method) Interfaces in Kotlin: Converting Java Interfaces to Kotlin Interfaces***English** document is available*](/en/Knowledge-base/Kotlin/Learning/046-sam-single-abstract-method-interfaces-in-kotlin-converting-java-interfaces-to-kotlin-interfaces)
{.links-list}


# 046: Kotlin의 SAM(Single Abstract Method) 인터페이스: Java 인터페이스를 Kotlin 인터페이스로 변환

Kotlin은 JVM 언어이므로 Java와 완벽하게 호환됩니다. 즉, 모든 Java 인터페이스를 문제 없이 Kotlin 인터페이스로 변환할 수 있습니다.

그러나 한 가지 주의 사항이 있습니다. Kotlin은 SAM(Single Abstract Method) 인터페이스를 지원하지 않습니다. 즉, 단일 추상 메서드가 포함된 Java 인터페이스를 Kotlin 인터페이스로 변환할 수 없습니다.

그 이유는 Kotlin의 타입 시스템이 Java와 다르기 때문입니다. Kotlin에서 모든 인터페이스에는 본문이 없는 더미 메서드인 경우에도 하나 이상의 추상 메서드가 있어야 합니다.

여러 추상 메서드가 포함된 Java 인터페이스를 Kotlin으로 변환하는 경우에는 문제가 되지 않습니다. 그러나 SAM 인터페이스를 변환하는 경우 Kotlin 인터페이스에 추상 메서드를 추가해야 합니다.

이 작업을 수행하는 쉬운 방법이 없으므로 수동으로 추상 메서드를 추가해야 합니다. 이를 수행하는 가장 좋은 방법은 본문이 없는 더미 메서드를 추가하는 것입니다. 이렇게 하면 Kotlin 인터페이스가 Java 인터페이스와 호환됩니다.

다음은 Java SAM 인터페이스의 예입니다.

```java
public interface Runnable {
     public void run();
}
```

그리고 동등한 Kotlin 인터페이스는 다음과 같습니다.

```kotlin
interface Runnable {
    fun run()
}
```

보시다시피 Kotlin 인터페이스에는 Kotlin 유형 시스템에 필요한 추가 추상 메소드 ```run()```이 있습니다.

Java 인터페이스를 Kotlin으로 변환하는 경우 인터페이스가 SAM 인터페이스인지 항상 확인해야 합니다. 그렇다면 Kotlin 인터페이스에 별도의 추상 메서드를 추가해야 합니다.