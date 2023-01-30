---
title: Java 메모리 관리 이해
description: 
published: true
date: 2023-01-30T00:05:35.177Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:05:35.177Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Understanding Java Memory Management***English** version of this document is available*](/en/Knowledge-base/Backend/understanding-java-memory-management)
{.links-list}




Java는 개발자가 강력하고 재사용 가능한 코드를 만들 수 있는 플랫폼 독립적인 객체 지향 언어입니다. Java는 소규모 애플릿에서 대규모 엔터프라이즈 애플리케이션에 이르기까지 다양한 애플리케이션에서 사용됩니다.

Java 애플리케이션은 대상 플랫폼의 JVM(Java Virtual Machine)에서 해석되는 바이트코드로 컴파일됩니다. 바이트코드는 플랫폼 독립적이므로 모든 JVM에서 동일한 코드를 실행할 수 있습니다.

JVM은 바이트코드 실행을 위한 플랫폼 독립적 환경을 제공합니다. JVM에는 애플리케이션에서 더 이상 참조하지 않는 개체가 사용하는 메모리를 자동으로 회수하는 가비지 수집기가 포함되어 있습니다.

객체가 더 이상 필요하지 않으면 가비지 수집기는 객체가 사용한 메모리를 회수합니다. Java 언어는 명시적으로 메모리를 해제하는 메커니즘을 제공하지 않습니다.

그러나 Java 언어는 개체가 가비지 수집에 적합한 시기를 제어하는 방법을 제공합니다. java.lang.ref.WeakReference 클래스를 사용하면 개체에 대한 강력한 참조가 없을 때 개체가 가비지 수집될 수 있습니다.

java.lang.ref.SoftReference 클래스를 사용하면 JVM의 메모리가 부족할 때 객체가 가비지 수집될 수 있습니다.

java.lang.ref.PhantomReference 클래스는 객체에 대한 모든 참조가 제거되었을 때 객체가 가비지 수집되도록 허용합니다.

java.lang.System.gc() 메서드를 사용하여 JVM이 가비지 수집기를 실행하도록 요청할 수 있습니다. 그러나 이 메소드가 호출될 때 가비지 콜렉션을 수행하기 위해 JVM이 필요하지 않습니다.

java.lang.Runtime.getRuntime().gc() 메서드를 사용하여 JVM이 가비지 수집기를 실행하도록 요청할 수 있습니다. 이 메서드는 java.lang.System.gc() 메서드와 동일합니다.

JVM은 애플리케이션이 사용하는 메모리 양을 모니터링하기 위한 메커니즘을 제공합니다. java.lang.management.MemoryMXBean 클래스를 사용하여 JVM에서 사용하는 메모리 양을 모니터링할 수 있습니다.

java.lang.management.MemoryUsage 클래스는 JVM에서 사용하는 메모리 양을 나타냅니다.

java.lang.management.MemoryPoolMXBean 클래스는 JVM의 메모리 풀을 나타냅니다.

JVM에는 JVM의 상태를 모니터링하는 데 사용할 수 있는 여러 내장 모니터가 있습니다. 가장 중요한 모니터는 가비지 수집기, 스레드 및 클래스 로딩 모니터입니다.

가비지 수집기 모니터를 사용하여 가비지 수집기의 성능을 모니터링할 수 있습니다.

스레드 모니터는 JVM의 스레드 스케줄링 알고리즘의 성능을 모니터하는 데 사용할 수 있습니다.

클래스 로딩 모니터는 JVM의 클래스 로딩 시스템의 성능을 모니터링하는 데 사용할 수 있습니다.

기본 제공 모니터 외에도 JVM을 모니터링하는 데 사용할 수 있는 여러 타사 도구가 있습니다.

jvisualvm은 JVM을 모니터링하는 데 사용할 수 있는 시각적 도구입니다.

YourKit은 JVM을 프로파일링하는 데 사용할 수 있는 상용 도구입니다.

EclipseMAT는 JVM을 모니터링하는 데 사용할 수 있는 무료 도구입니다.

JVMTI(JVM Tool Interface)는 JVM을 모니터링하는 데 사용할 수 있는 하위 수준 인터페이스입니다.

JVMTI(Java Virtual Machine Tool Interface)는 JVM을 모니터링하는 데 사용할 수 있는 저수준 인터페이스입니다.

JVMTI는 JVM TI 에이전트를 통해 액세스되는 기본 인터페이스입니다.

JVMTI 에이전트는 JVM을 계측하는 데 사용되는 기본 에이전트입니다.

JVMTI 에이전트는 플랫폼에 따라 다르며 JVM TI가 사용될 각 플랫폼에 대해 구현되어야 합니다.

JVMTI 에이전트는 JVM TI가 활성화되면 JVM에 로드됩니다.

JVM TI가 비활성화되면 JVMTI 에이전트가 JVM에서 언로드됩니다.

JVMTI 에이전트는 JVM의 일부가 아니며 Java 라이센스 조건이 적용되지 않습니다.

JVMTI는 JVM을 모니터링하는 데 사용할 수 있는 강력한 도구입니다. 그러나 JVMTI는 저수준 인터페이스이며 애플리케이션 모니터링에 적합하지 않습니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 고급 인터페이스입니다.

JMX는 Java 플랫폼의 일부인 표준입니다.

JMX는 java.lang.management 패키지에서 구현됩니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 플랫폼 독립적인 인터페이스입니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 유연한 인터페이스입니다.

JMX를 사용하여 JVM을 모니터링할 수 있습니다. 그러나 JMX는 애플리케이션 모니터링에 적합하지 않습니다.

JMX는 JVM 모니터링에 적합한 고급 인터페이스입니다.

JMX는 Java 플랫폼의 일부인 표준입니다.

JMX는 java.lang.management 패키지에서 구현됩니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 플랫폼 독립적인 인터페이스입니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 유연한 인터페이스입니다.

JMX를 사용하여 JVM을 모니터링할 수 있습니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 고급 인터페이스입니다.

JMX는 Java 플랫폼의 일부인 표준입니다.

JMX는 java.lang.management 패키지에서 구현됩니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 플랫폼 독립적인 인터페이스입니다.

JMX는 JVM을 모니터링하는 데 사용할 수 있는 유연한 인터페이스입니다.

JMX를 사용하여 JVM을 모니터링할 수 있습니다.