---
title: 探索 Java 本机接口 (JNI) 以实现互操作性
description: 
published: true
date: 2023-02-06T20:56:09.875Z
tags: 
editor: markdown
dateCreated: 2023-02-06T20:56:08.248Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Exploring the Java Native Interface (JNI) for Interoperability***English** document is available*](/en/Knowledge-base/Java/exploring-the-java-native-interface-jni-for-interoperability)
{.links-list}


# 探索 Java 本机接口 (JNI) 以实现互操作性

Java 本机接口 (JNI) 是一个强大的工具，它允许 Java 代码与用其他语言编写的本机代码进行互操作。在本文中，我们将仔细研究 JNI 的工作原理以及如何使用它来提高 Java 应用程序的性能。

## 什么是 Java 本机接口？

Java 本机接口是一组标准，定义了 Java 代码如何与用其他语言编写的本机代码进行交互。 JNI 是平台无关的，这意味着它可以用来编写在任何操作系统上运行的代码。

## JNI 是如何工作的？

JNI 定义了一组规则来管理 Java 代码和本机代码如何交互。当 Java 应用程序调用本地方法时，JNI 层将方法调用翻译成本地语言。然后执行本机代码，并将结果返回给 Java 应用程序。

## 使用 JNI 的好处

使用 JNI 有几个好处，包括：

- 提高性能：本机代码通常比 Java 代码更快，因此使用 JNI 可以提高 Java 应用程序的性能。
- 访问本机库：JNI 允许 Java 代码访问 Java 平台中不可用的本机库。
- 简化开发：JNI可用于编写Java较难编写的代码，例如与低级系统组件交互的代码。

## 使用 JNI 的缺点

使用 JNI 也有一些缺点，包括：

- 增加了复杂性：JNI 为 Java 应用程序增加了一层额外的复杂性。
- 有限的可移植性：JNI 代码不可跨平台移植，因此必须为每个平台重写。
- 安全风险：JNI 代码可以绕过 Java 的安全模型，这会带来安全风险。

## 什么时候应该使用 JNI？

当利大于弊时，应该使用 JNI。 JNI 最常用于提高 Java 应用程序的性能或访问 Java 平台中不可用的本机库。

## 示例：调用本机方法

让我们看一个如何使用 JNI 来提高 Java 应用程序性能的示例。我们将从计算两个整数之和的简单 Java 方法开始：

```java
public static int sum(int a, int b) {
    return a + b;
}
```

我们可以通过使用 JNI 调用在本地代码中执行计算的本地方法来提高此方法的性能。首先，我们需要用C写native方法：

```c
int sum(int a, int b) {
    return a + b;
}
```

接下来，我们需要编写一个调用本地方法的 Java 包装器方法：

```java
public static native int sum(int a, int b);
```

最后，我们需要将 C 代码和 Java 代码编译成一个共享库。在 Linux 上，我们可以使用以下命令执行此操作：

```
gcc -shared -fPIC -o libsum.so sum.c
```

然后我们可以使用以下代码将共享库加载到我们的 Java 应用程序中：

```java
System.loadLibrary("sum");
```

我们现在可以从 Java 代码中调用 sum() 方法，计算将在本机代码中执行。这可以提高我们应用程序的性能，因为本机代码通常比 Java 代码更快。

## 示例：访问本机库

JNI 还可用于访问 Java 平台中不可用的本机库。例如，Java 平台不提供用于访问 Win32 API 的本机库。但是，我们可以使用 JNI 从我们的 Java 代码中调用 Win32 API。

首先，我们需要为每个要调用的 Win32 API 函数编写一个 Java 包装器方法：

```java
public static native int MessageBox(int hWnd, String lpText, String lpCaption, int uType);
```

接下来，我们需要编写一个包含 Win32 API 和 JNI 头文件的 C++ 文件：

```c++
#include <windows.h>
#include <jni.h>
```

然后我们可以编写 Java 包装器方法的实现：

```c++
JNIEXPORT jint JNICALL Java_MessageBox_1MessageBox(JNIEnv *env, jclass cls, jint hWnd, jstring lpText, jstring lpCaption, jint uType)
{
    return MessageBox(hWnd, (LPCTSTR)lpText, (LPCTSTR)lpCaption, uType);
}
```

最后，我们需要将我们的 C++ 代码编译成一个共享库。在 Windows 上，我们可以使用以下命令执行此操作：

```
cl /LD MessageBox.cpp
```

然后我们可以使用以下代码将共享库加载到我们的 Java 应用程序中：

```java
System.loadLibrary("MessageBox");
```

我们现在可以从我们的 Java 代码调用 MessageBox() 函数，Win32 API 将被调用。这允许我们从 Java 代码访问 Win32 API，即使 Java 平台没有为 Win32 API 提供本机库。

## 示例：从本机代码调用 Java 方法

JNI 也可用于从本机代码调用 Java 方法。当我们需要从没有 JNI 接口的本机库调用 Java 方法时，这会很有用。

首先，我们需要为要调用的 Java 方法编写一个 Java 包装器方法：

```java
public static native void print(String msg);
```

接下来，我们需要编写一个包含 JNI 头文件的 C++ 文件：

```c++
#include <jni.h>
```

然后我们可以编写 Java 包装器方法的实现：

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

最后，我们需要将我们的 C++ 代码编译成一个共享库。在 Windows 上，我们可以使用以下命令执行此操作：

```
cl /LD print.cpp
```

然后我们可以使用以下代码将共享库加载到我们的 Java 应用程序中：

```java
System.loadLibrary("print");
```

我们现在可以从 C++ 代码调用 print() 方法，Java println() 方法将被调用。这允许我们从没有 JNI 接口的本机库调用 Java 方法。

## 结论

JNI 是一个强大的工具，它允许 Java 代码与用其他语言编写的本机代码进行互操作。 JNI 可用于提高 Java 应用程序的性能或访问 Java 平台中不可用的本机库。但是，JNI 也为 Java 应用程序增加了一层额外的复杂性，并且不能跨平台移植。