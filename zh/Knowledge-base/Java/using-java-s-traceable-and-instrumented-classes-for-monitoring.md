---
title: 使用 Java 的 Traceable 和 Instrumented 类进行监控
description: 
published: true
date: 2023-02-05T12:17:30.050Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:17:28.492Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Using Java's Traceable and Instrumented Classes for Monitoring***English** document is available*](/en/Knowledge-base/Java/using-java-s-traceable-and-instrumented-classes-for-monitoring)
{.links-list}


# 使用 Java 的 Traceable 和 Instrumented 类进行监控

检测代码是一种用于监视 Java 应用程序性能的强大技术。通过使用 Java 的 Traceable 和 Instrumented 类，开发人员可以收集关于他们的代码如何运行的详细信息并识别潜在的瓶颈。

检测可用于监视应用程序性能的许多方面，包括内存使用、垃圾收集活动和线程执行。在本文中，我们将重点关注使用检测来监视方法执行时间。

## 为什么要使用检测？

Instrumentation 允许开发人员收集性能数据而无需修改他们的代码。这对于监控生产系统特别有用，因为代码更改可能难以部署。

Instrumentation 也可用于监控不受开发人员控制的代码，例如第三方库。在这种情况下，可以使用检测来收集有关如何使用库的数据并识别潜在的性能问题。

## 使用 Java 的可跟踪和检测类

Java 的 Traceable 和 Instrumented 类提供了一种检测代码和收集性能数据的简单方法。这些类是 java.lang.instrument 包的一部分，在 Java 5 及更高版本中可用。

要使用 Traceable 和 Instrumented 类，开发人员需要创建 java.lang.instrument.Instrumentation 的子类并覆盖 premain() 方法。在执行应用程序的 main() 方法之前调用此方法。

在 premain() 方法中，开发人员需要创建其 Traceable 或 Instrumented 子类的实例，并将其注册到 Java 虚拟机 (JVM)。当某些事件发生时，JVM 将调用 Traceable 或 Instrumented 子类中的方法，例如调用方法。

下面是跟踪方法调用时间的 Traceable 子类的一个简单示例：

```java
public class MyTraceable extends Traceable {

private Map<String, Long> methodTimes = new HashMap<String, Long>();

@Override
public void traceMethodInvocation(MethodInfo methodInfo) {

String methodName = methodInfo.getMethodName();

if (methodTimes.containsKey(methodName)) {

long totalTime = methodTimes.get(methodName);

totalTime += methodInfo.getElapsedTime();

methodTimes.put(methodName, totalTime);

} else {

methodTimes.put(methodName, methodInfo.getElapsedTime());

}

}

public Map<String, Long> getMethodTimes() {

return methodTimes;

}

}
```

在上面的示例中，只要调用一个方法，就会调用 traceMethodInvocation() 方法。 methodInfo 参数包含有关方法的信息，包括方法的名称和执行所花费的时间。

traceMethodInvocation() 方法将方法调用时间存储在映射中。 getMethodTimes() 方法可用于检索地图。

要向 JVM 注册 MyTraceable 类，可以使用 premain() 方法：

```java
public static void premain(String args, Instrumentation instrumentation) {

instrumentation.addTransformer(new MyTraceable());

}
```

在 premain() 方法中，MyTraceable 类注册到检测对象。检测对象用于将类转换器添加到 JVM。类转换器是一段代码，它在 JVM 加载类之前修改类的字节码。

MyTraceable 类被注册为类转换器，因此只要调用方法，就会调用其 traceMethodInvocation() 方法。

一旦注册了 MyTraceable 类，应用程序就可以照常运行。每次调用方法时都会调用 traceMethodInvocation() 方法，并且会在 MyTraceable 对象中跟踪方法调用次数。

## 分析数据

MyTraceable 类收集的数据可用于识别应用程序中的潜在瓶颈。为此，可以根据每种方法花费的时间对数据进行排序。

执行时间最长的方法是潜在的瓶颈。可以进一步分析这些方法，看看它们是否可以优化。

## 结论

Instrumentation 是一种用于监视 Java 应用程序性能的强大技术。通过使用 Java 的 Traceable 和 Instrumented 类，开发人员可以收集关于他们的代码如何运行的详细信息并识别潜在的瓶颈。