---
title: 상호 운용성을 위한 JNI(Java Native Interface) 탐색
description: 
published: true
date: 2023-02-06T20:56:09.853Z
tags: 
editor: markdown
dateCreated: 2023-02-06T20:56:08.250Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Exploring the Java Native Interface (JNI) for Interoperability***English** document is available*](/en/Knowledge-base/Java/exploring-the-java-native-interface-jni-for-interoperability)
{.links-list}


# 상호 운용성을 위한 JNI(Java Native Interface) 탐색

JNI(Java Native Interface)는 Java 코드가 다른 언어로 작성된 네이티브 코드와 상호 작용할 수 있도록 하는 강력한 도구입니다. 이 기사에서는 JNI의 작동 방식과 JNI를 사용하여 Java 애플리케이션의 성능을 개선하는 방법에 대해 자세히 살펴보겠습니다.

## 자바 네이티브 인터페이스란?

Java 네이티브 인터페이스는 Java 코드가 다른 언어로 작성된 네이티브 코드와 상호 작용할 수 있는 방법을 정의하는 표준 집합입니다. JNI는 플랫폼 독립적이므로 모든 운영 체제에서 실행되는 코드를 작성하는 데 사용할 수 있습니다.

## JNI는 어떻게 작동합니까?

JNI는 Java 코드와 네이티브 코드가 상호 작용하는 방식을 제어하는 일련의 규칙을 정의합니다. Java 애플리케이션이 네이티브 메서드를 호출하면 JNI 계층이 메서드 호출을 네이티브 언어로 변환합니다. 그런 다음 네이티브 코드가 실행되고 결과가 Java 애플리케이션으로 반환됩니다.

## JNI 사용의 이점

JNI를 사용하면 다음과 같은 몇 가지 이점이 있습니다.

- 향상된 성능: 기본 코드는 일반적으로 Java 코드보다 빠르므로 JNI를 사용하면 Java 애플리케이션의 성능을 향상시킬 수 있습니다.
- 네이티브 라이브러리에 대한 액세스: JNI를 통해 Java 코드는 Java 플랫폼에서 사용할 수 없는 네이티브 라이브러리에 액세스할 수 있습니다.
- 간소화된 개발: JNI를 사용하여 하위 수준 시스템 구성 요소와 상호 작용하는 코드와 같이 Java로 작성하기 어려운 코드를 작성할 수 있습니다.

## JNI 사용의 단점

JNI 사용에는 다음과 같은 몇 가지 단점도 있습니다.

- 복잡성 증가: JNI는 Java 애플리케이션에 추가적인 복잡성 계층을 추가합니다.
- 제한된 이식성: JNI 코드는 플랫폼 간 이식이 불가능하므로 플랫폼마다 다시 작성해야 합니다.
- 보안 위험: JNI 코드는 Java의 보안 모델을 우회할 수 있으므로 보안 위험이 발생할 수 있습니다.

## JNI는 언제 사용해야 합니까?

장점이 단점보다 클 때 JNI를 사용해야 합니다. JNI는 Java 애플리케이션의 성능을 개선하거나 Java 플랫폼에서 사용할 수 없는 기본 라이브러리에 액세스하는 데 가장 일반적으로 사용됩니다.

## 예: 네이티브 메서드 호출

JNI를 사용하여 Java 애플리케이션의 성능을 개선하는 방법의 예를 살펴보겠습니다. 두 정수의 합을 계산하는 간단한 Java 메서드부터 시작하겠습니다.

```java
public static int sum(int a, int b) {
    return a + b;
}
```

JNI를 사용하여 네이티브 코드에서 계산을 수행하는 네이티브 메서드를 호출함으로써 이 메서드의 성능을 향상시킬 수 있습니다. 먼저 네이티브 메서드를 C로 작성해야 합니다.

```c
int sum(int a, int b) {
    return a + b;
}
```

다음으로 네이티브 메서드를 호출하는 Java 래퍼 메서드를 작성해야 합니다.

```java
public static native int sum(int a, int b);
```

마지막으로 C 코드와 Java 코드를 공유 라이브러리로 컴파일해야 합니다. Linux에서는 다음 명령으로 이를 수행할 수 있습니다.

```
gcc -shared -fPIC -o libsum.so sum.c
```

그런 다음 다음 코드를 사용하여 공유 라이브러리를 Java 애플리케이션에 로드할 수 있습니다.

```java
System.loadLibrary("sum");
```

이제 Java 코드에서 sum() 메서드를 호출할 수 있으며 네이티브 코드에서 계산이 수행됩니다. 네이티브 코드는 일반적으로 Java 코드보다 빠르기 때문에 애플리케이션의 성능을 향상시킬 수 있습니다.

## 예: 기본 라이브러리에 액세스

JNI는 Java 플랫폼에서 사용할 수 없는 기본 라이브러리에 액세스하는 데에도 사용할 수 있습니다. 예를 들어 Java 플랫폼은 Win32 API에 액세스하기 위한 기본 라이브러리를 제공하지 않습니다. 그러나 JNI를 사용하여 Java 코드에서 Win32 API를 호출할 수 있습니다.

먼저 호출하려는 각 Win32 API 함수에 대한 Java 래퍼 메서드를 작성해야 합니다.

```java
public static native int MessageBox(int hWnd, String lpText, String lpCaption, int uType);
```

다음으로 Win32 API 및 JNI용 헤더 파일을 포함하는 C++ 파일을 작성해야 합니다.

```c++
#include <windows.h>
#include <jni.h>
```

그런 다음 Java 래퍼 메서드의 구현을 작성할 수 있습니다.

```c++
JNIEXPORT jint JNICALL Java_MessageBox_1MessageBox(JNIEnv *env, jclass cls, jint hWnd, jstring lpText, jstring lpCaption, jint uType)
{
    return MessageBox(hWnd, (LPCTSTR)lpText, (LPCTSTR)lpCaption, uType);
}
```

마지막으로 C++ 코드를 공유 라이브러리로 컴파일해야 합니다. Windows에서는 다음 명령으로 이 작업을 수행할 수 있습니다.

```
cl /LD MessageBox.cpp
```

그런 다음 다음 코드를 사용하여 공유 라이브러리를 Java 애플리케이션에 로드할 수 있습니다.

```java
System.loadLibrary("MessageBox");
```

이제 Java 코드에서 MessageBox() 함수를 호출할 수 있으며 Win32 API가 호출됩니다. 이를 통해 Java 플랫폼이 Win32 API용 기본 라이브러리를 제공하지 않더라도 Java 코드에서 Win32 API에 액세스할 수 있습니다.

## 예: 네이티브 코드에서 Java 메서드 호출

JNI는 네이티브 코드에서 Java 메서드를 호출하는 데에도 사용할 수 있습니다. 이는 JNI 인터페이스가 없는 네이티브 라이브러리에서 Java 메서드를 호출해야 할 때 유용할 수 있습니다.

먼저 호출하려는 Java 메서드에 대한 Java 래퍼 메서드를 작성해야 합니다.

```java
public static native void print(String msg);
```

다음으로 JNI용 헤더 파일을 포함하는 C++ 파일을 작성해야 합니다.

```c++
#include <jni.h>
```

그런 다음 Java 래퍼 메서드의 구현을 작성할 수 있습니다.

```c++
JNIEXPORT void JNICALL Java_print_1print(JNIEnv *env, jclass cls, jstring msg)
{
    // Get the printStream field from the java.lang.System class
    jclass systemClass = env->FindClass("java/lang/System");
    jfieldID printStreamField = env->GetStaticFieldID(systemClass, "out", "Ljava/io/PrintStream;");

    // Get the PrintStream object from the printStream field
    jobject printStream = env->GetStaticObjectField(systemClass, printStreamField);

    // Get the println() method from the PrintStream class
    jclass printStreamClass = env->GetObjectClass(printStream);
    jmethodID printlnMethod = env->GetMethodID(printStreamClass, "println", "(Ljava/lang/String;)V");

    // Call the println() method
    env->CallVoidMethod(printStream, printlnMethod, msg);
}
```

마지막으로 C++ 코드를 공유 라이브러리로 컴파일해야 합니다. Windows에서는 다음 명령으로 이 작업을 수행할 수 있습니다.

```
cl /LD print.cpp
```

그런 다음 다음 코드를 사용하여 공유 라이브러리를 Java 애플리케이션에 로드할 수 있습니다.

```java
System.loadLibrary("print");
```

이제 C++ 코드에서 print() 메서드를 호출할 수 있으며 Java println() 메서드가 호출됩니다. 이를 통해 JNI 인터페이스가 없는 네이티브 라이브러리에서 Java 메서드를 호출할 수 있습니다.

## 결론

JNI는 Java 코드가 다른 언어로 작성된 기본 코드와 상호 운용될 수 있도록 하는 강력한 도구입니다. JNI는 Java 애플리케이션의 성능을 개선하거나 Java 플랫폼에서 사용할 수 없는 기본 라이브러리에 액세스하는 데 사용할 수 있습니다. 그러나 JNI는 또한 Java 애플리케이션에 추가적인 복잡성 계층을 추가하며 플랫폼 간에 이식할 수 없습니다.