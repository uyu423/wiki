---
title: Exploring the Java Native Interface (JNI) for Interoperability
description: 
published: true
date: 2023-02-06T20:56:13.990Z
tags: 
editor: markdown
dateCreated: 2023-02-06T20:56:08.260Z
---

- [Exploración de la interfaz nativa de Java (JNI) para la interoperabilidad***Spanish** document is available*](/es/Knowledge-base/Java/exploring-the-java-native-interface-jni-for-interoperability)
{.links-list}
- [探索 Java 本机接口 (JNI) 以实现互操作性***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/exploring-the-java-native-interface-jni-for-interoperability)
{.links-list}
- [상호 운용성을 위한 JNI(Java Native Interface) 탐색***Korean** document is available*](/ko/Knowledge-base/Java/exploring-the-java-native-interface-jni-for-interoperability)
{.links-list}


# Exploring the Java Native Interface (JNI) for Interoperability

The Java Native Interface (JNI) is a powerful tool that allows Java code to interoperate with native code written in other languages. In this article, we'll take a closer look at how JNI works and how it can be used to improve the performance of Java applications.

## What is the Java Native Interface?

The Java Native Interface is a set of standards that define how Java code can interact with native code written in other languages. JNI is platform-independent, meaning that it can be used to write code that runs on any operating system.

## How Does JNI Work?

JNI defines a set of rules that govern how Java code and native code can interact. When a Java application calls a native method, the JNI layer translates the method call into the native language. The native code is then executed, and the result is returned to the Java application.

## Benefits of Using JNI

There are several benefits to using JNI, including:

- Improved performance: Native code is typically faster than Java code, so using JNI can improve the performance of Java applications.
- Access to native libraries: JNI allows Java code to access native libraries that are not available in the Java platform.
- Simplified development: JNI can be used to write code that is more difficult to write in Java, such as code that interacts with low-level system components.

## Drawbacks of Using JNI

There are also some drawbacks to using JNI, including:

- Increased complexity: JNI adds an additional layer of complexity to Java applications.
- Limited portability: JNI code is not portable across platforms, so it must be rewritten for each platform.
- Security risks: JNI code can bypass Java's security model, which can introduce security risks.

## When Should JNI Be Used?

JNI should be used when the benefits outweigh the drawbacks. JNI is most commonly used to improve the performance of Java applications or to access native libraries that are not available in the Java platform.

## Example: Calling a Native Method

Let's take a look at an example of how JNI can be used to improve the performance of a Java application. We'll start with a simple Java method that calculates the sum of two integers:

```java
public static int sum(int a, int b) {
    return a + b;
}
```

We can improve the performance of this method by using JNI to call a native method that performs the calculation in native code. First, we need to write the native method in C:

```c
int sum(int a, int b) {
    return a + b;
}
```

Next, we need to write a Java wrapper method that calls the native method:

```java
public static native int sum(int a, int b);
```

Finally, we need to compile the C code and the Java code into a shared library. On Linux, we can do this with the following command:

```
gcc -shared -fPIC -o libsum.so sum.c
```

We can then load the shared library into our Java application with the following code:

```java
System.loadLibrary("sum");
```

We can now call the sum() method from our Java code and the calculation will be performed in native code. This can improve the performance of our application since native code is typically faster than Java code.

## Example: Accessing a Native Library

JNI can also be used to access native libraries that are not available in the Java platform. For example, the Java platform does not provide a native library for accessing the Win32 API. However, we can use JNI to call the Win32 API from our Java code.

First, we need to write a Java wrapper method for each Win32 API function that we want to call:

```java
public static native int MessageBox(int hWnd, String lpText, String lpCaption, int uType);
```

Next, we need to write a C++ file that includes the header files for the Win32 API and JNI:

```c++
#include <windows.h>
#include <jni.h>
```

We can then write the implementation of our Java wrapper method:

```c++
JNIEXPORT jint JNICALL Java_MessageBox_1MessageBox(JNIEnv *env, jclass cls, jint hWnd, jstring lpText, jstring lpCaption, jint uType)
{
    return MessageBox(hWnd, (LPCTSTR)lpText, (LPCTSTR)lpCaption, uType);
}
```

Finally, we need to compile our C++ code into a shared library. On Windows, we can do this with the following command:

```
cl /LD MessageBox.cpp
```

We can then load the shared library into our Java application with the following code:

```java
System.loadLibrary("MessageBox");
```

We can now call the MessageBox() function from our Java code and the Win32 API will be called. This allows us to access the Win32 API from our Java code, even though the Java platform does not provide a native library for the Win32 API.

## Example: Calling a Java Method from Native Code

JNI can also be used to call Java methods from native code. This can be useful when we need to call a Java method from a native library that does not have a JNI interface.

First, we need to write a Java wrapper method for the Java method that we want to call:

```java
public static native void print(String msg);
```

Next, we need to write a C++ file that includes the header files for JNI:

```c++
#include <jni.h>
```

We can then write the implementation of our Java wrapper method:

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

Finally, we need to compile our C++ code into a shared library. On Windows, we can do this with the following command:

```
cl /LD print.cpp
```

We can then load the shared library into our Java application with the following code:

```java
System.loadLibrary("print");
```

We can now call the print() method from our C++ code and the Java println() method will be called. This allows us to call a Java method from a native library that does not have a JNI interface.

## Conclusion

JNI is a powerful tool that allows Java code to interoperate with native code written in other languages. JNI can be used to improve the performance of Java applications or to access native libraries that are not available in the Java platform. However, JNI also adds an additional layer of complexity to Java applications and is not portable across platforms.