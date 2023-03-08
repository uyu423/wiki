---
title: 构建自定义 Java 日志处理程序
description: 
published: true
date: 2023-02-07T05:17:59.114Z
tags: 
editor: markdown
dateCreated: 2023-02-07T05:17:57.424Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building Custom Java Logging Handlers***English** document is available*](/en/Knowledge-base/Java/building-custom-java-logging-handlers)
{.links-list}


# 构建自定义 Java 日志处理程序

Java 平台为日志记录和记录系统范围的事件提供了内置支持。除了许多开箱即用的选项外，Java 开发人员还可以创建自己的自定义日志记录处理程序。

日志处理程序是一个对象，负责从记录器接收日志记录并将它们导出到目的地，例如文件、控制台或远程服务器。

在本文中，我们将了解如何在 Java 中构建自定义日志记录处理程序。我们还将探索创建和使用日志处理程序的一些最佳实践。

## 创建自定义日志处理程序

在 Java 中创建自定义日志记录处理程序是一个两步过程。首先，我们需要创建一个扩展 java.util.logging.Handler 类的类。此类将定义我们的自定义处理程序的行为。

接下来，我们需要向 java.util.logging.LogManager 注册我们的处理程序。这可以通过编程方式或使用配置文件来完成。

让我们看一下每种方法的示例。

### 程序化注册

编程注册是注册自定义日志处理程序的最简单方法。我们可以通过调用 LogManager.addHandler() 方法来完成此操作。此方法接受我们的自定义处理程序类的实例作为参数。

这是一个例子：

```java
import java.util.logging.Handler;
import java.util.logging.LogManager;
import java.util.logging.Logger;

public class MyCustomHandler extends Handler {
    // ...
}

public class Main {
    public static void main(String[] args) {
        // create an instance of our custom handler
        Handler handler = new MyCustomHandler();
        
        // get the root logger
        Logger logger = LogManager.getLogManager().getLogger("");
        
        // add our handler to the root logger
        logger.addHandler(handler);
    }
}
```

在上面的示例中，我们首先创建自定义 Handler 类的实例。接下来，我们从 LogManager 获取根记录器。最后，我们将处理程序添加到根记录器。

### 配置文件注册

配置文件注册比编程注册稍微复杂一些，但它提供了更大的灵活性。

通过配置文件注册，我们需要在 Java 应用程序的“conf”目录中创建一个名为“logging.properties”的文件。该文件包含许多配置 Java 日志记录系统的属性。

下面是一个 logging.properties 文件的示例：

```
# default logging level
.level=INFO

# default handler
handlers=java.util.logging.ConsoleHandler

# custom handler
com.example.MyCustomHandler.level=ALL
com.example.MyCustomHandler.formatter=java.util.logging.SimpleFormatter
com.example.MyCustomHandler.encoding=UTF-8
```

在上面的示例中，我们为自定义处理程序定义了许多属性。第一个属性“level”指定我们的处理程序的日志记录级别。第二个属性“formatter”指定我们的处理程序要使用的格式化程序。第三个属性“encoding”指定我们的处理程序使用的字符编码。

## 创建自定义日志处理程序的最佳实践

现在我们已经了解了如何在 Java 中创建自定义日志记录处理程序，让我们看一下创建和使用日志记录处理程序的一些最佳实践。

### 把事情简单化

创建自定义日志记录处理程序时，保持设计简单很重要。一个好的经验法则是只覆盖绝对必要的方法。

例如，java.util.logging.Handler 类定义了许多处理日志记录的方法。然而，我们只需要覆盖 publish() 方法。其他方法可以保持原样。

### 使用现有处理程序作为起点

创建自定义日志记录处理程序时，使用现有处理程序作为起点通常很有帮助。例如，java.util.logging.ConsoleHandler 类是一个将日志记录写入控制台的简单处理程序。

如果我们正在创建一个将日志记录写入文件的处理程序，我们可以使用 java.util.logging.FileHandler 类作为起点。此类定义了将日志记录写入文件的所有必要方法。

### 不要阻塞记录器的线程

创建自定义日志记录处理程序时，避免阻塞记录器的线程很重要。阻塞处理程序可能导致记录器停止处理日志记录。

避免阻塞记录器线程的一种方法是使用单独的线程来导出日志记录。例如，java.util.logging.AsyncHandler 类使用单独的线程来导出日志记录。

避免阻塞记录器线程的另一种方法是使用队列。 java.util.logging.QueueHandler 类使用队列来存储日志记录。然后记录由单独的线程导出。

### 使用格式化程序

创建自定义日志记录处理程序时，使用格式化程序很重要。格式化程序是负责将日志记录转换为字符串的对象。

java.util.logging.Handler 类定义了一个 setFormatter() 方法，可用于设置处理程序的格式化程序。默认情况下，创建处理程序时会调用此方法。

如果我们使用自定义格式化程序，我们需要确保格式化程序是线程安全的。这是因为格式化程序可能会被多个线程调用。

确保格式化程序线程安全的一种方法是使用 java.util.logging.ThreadLocalFormatter 类。此类定义特定于当前线程的格式化程序。

确保格式化程序线程安全的另一种方法是使用 java.util.logging.SynchronizedFormatter 类。此类包装现有的格式化程序并同步所有格式化程序的方法。

### 使用过滤器

创建自定义日志记录处理程序时，使用过滤器通常很有帮助。过滤器是一个对象，负责确定处理程序应导出哪些日志记录。

java.util.logging.Handler 类定义了一个 setFilter() 方法，可用于为处理程序设置过滤器。默认情况下，创建处理程序时会调用此方法。

如果我们使用自定义过滤器，我们需要确保过滤器是线程安全的。这是因为过滤器可能被多个线程调用。

确保过滤器线程安全的一种方法是使用 java.util.logging.SynchronizedFilter 类。此类包装现有过滤器并同步所有过滤器的方法。

另一种确保过滤器线程安全的方法是使用 java.util.logging.ThreadLocalFilter 类。此类定义特定于当前线程的过滤器。

### 使用锁

创建自定义日志记录处理程序时，使用锁通常很有帮助。锁是用于同步对资源的访问的对象。

java.util.logging.Handler 类定义了一个 setLock() 方法，可用于为处理程序设置锁。默认情况下，创建处理程序时会调用此方法。

如果我们使用自定义锁，我们需要确保锁是线程安全的。这是因为锁可能被多个线程访问。

确保锁是线程安全的一种方法是使用 java.util.concurrent.locks.ReentrantLock 类。这个类定义了一个可以被多个线程使用的锁。

确保锁是线程安全的另一种方法是使用 java.util.concurrent.locks.Lock 类。此类包装现有锁并同步所有锁的方法。

## 结论

在本文中，我们了解了如何在 Java 中创建自定义日志记录处理程序。我们还了解了如何使用 java.util.logging.LogManager 注册我们的处理程序。最后，我们了解了一些创建和使用日志处理程序的最佳实践。