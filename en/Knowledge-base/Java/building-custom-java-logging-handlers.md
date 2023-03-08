---
title: Building Custom Java Logging Handlers
description: 
published: true
date: 2023-02-07T05:18:03.221Z
tags: 
editor: markdown
dateCreated: 2023-02-07T05:17:57.427Z
---

- [Creación de controladores de registro de Java personalizados***Spanish** document is available*](/es/Knowledge-base/Java/building-custom-java-logging-handlers)
{.links-list}
- [构建自定义 Java 日志处理程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/building-custom-java-logging-handlers)
{.links-list}
- [사용자 지정 Java 로깅 처리기 빌드***Korean** document is available*](/ko/Knowledge-base/Java/building-custom-java-logging-handlers)
{.links-list}


# Building Custom Java Logging Handlers

The Java platform provides built-in support for logging and recording system-wide events. In addition to the many options available out-of-the-box, Java developers can also create their own custom logging handlers.

A logging handler is an object that is responsible for receiving log records from a logger and exporting them to a destination, such as a file, the console, or a remote server.

In this article, we'll take a look at how to build a custom logging handler in Java. We'll also explore some best practices for creating and using logging handlers.

## Creating a Custom Logging Handler

Creating a custom logging handler in Java is a two-step process. First, we need to create a class that extends the java.util.logging.Handler class. This class will define the behavior of our custom handler.

Next, we need to register our handler with the java.util.logging.LogManager. This can be done programmatically or by using a configuration file.

Let's take a look at an example of each approach.

### Programmatic Registration

Programmatic registration is the simplest way to register a custom logging handler. We can do this by calling the LogManager.addHandler() method. This method accepts an instance of our custom Handler class as a parameter.

Here's an example:

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

In the example above, we first create an instance of our custom Handler class. Next, we get the root logger from the LogManager. Finally, we add our handler to the root logger.

### Configuration File Registration

Configuration file registration is a bit more complex than programmatic registration, but it offers more flexibility.

With configuration file registration, we need to create a file named "logging.properties" in the "conf" directory of our Java application. This file contains a number of properties that configure the Java logging system.

Here's an example of a logging.properties file:

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

In the example above, we've defined a number of properties for our custom handler. The first property, "level", specifies the logging level for our handler. The second property, "formatter", specifies the formatter to be used by our handler. The third property, "encoding", specifies the character encoding to be used by our handler.

## Best Practices for Creating Custom Logging Handlers

Now that we've seen how to create a custom logging handler in Java, let's take a look at some best practices for creating and using logging handlers.

### Keep It Simple

When creating a custom logging handler, it's important to keep the design simple. A good rule of thumb is to only override the methods that are absolutely necessary.

For example, the java.util.logging.Handler class defines a number of methods for handling log records. However, we only need to override the publish() method. The other methods can be left as-is.

### Use Existing Handlers as a starting point

When creating a custom logging handler, it's often helpful to use an existing handler as a starting point. For example, the java.util.logging.ConsoleHandler class is a simple handler that writes log records to the console.

If we're creating a handler that writes log records to a file, we can use the java.util.logging.FileHandler class as a starting point. This class defines all of the necessary methods for writing log records to a file.

### Don't Block the Logger's Thread

When creating a custom logging handler, it's important to avoid blocking the logger's thread. A blocking handler can cause the logger to stop processing log records.

One way to avoid blocking the logger's thread is to use a separate thread for exporting log records. For example, the java.util.logging.AsyncHandler class uses a separate thread for exporting log records.

Another way to avoid blocking the logger's thread is to use a queue. The java.util.logging.QueueHandler class uses a queue to store log records. The records are then exported by a separate thread.

### Use a Formatter

When creating a custom logging handler, it's important to use a formatter. A formatter is an object that is responsible for converting a log record into a string.

The java.util.logging.Handler class defines a setFormatter() method that can be used to set the formatter for a handler. By default, this method is called when a handler is created.

If we're using a custom formatter, we need to make sure that the formatter is thread-safe. This is because the formatter may be called by multiple threads.

One way to ensure that a formatter is thread-safe is to use the java.util.logging.ThreadLocalFormatter class. This class defines a formatter that is specific to the current thread.

Another way to ensure that a formatter is thread-safe is to use the java.util.logging.SynchronizedFormatter class. This class wraps an existing formatter and synchronizes all of the formatter's methods.

### Use aFilter

When creating a custom logging handler, it's often helpful to use a filter. A filter is an object that is responsible for determining which log records should be exported by a handler.

The java.util.logging.Handler class defines a setFilter() method that can be used to set the filter for a handler. By default, this method is called when a handler is created.

If we're using a custom filter, we need to make sure that the filter is thread-safe. This is because the filter may be called by multiple threads.

One way to ensure that a filter is thread-safe is to use the java.util.logging.SynchronizedFilter class. This class wraps an existing filter and synchronizes all of the filter's methods.

Another way to ensure that a filter is thread-safe is to use the java.util.logging.ThreadLocalFilter class. This class defines a filter that is specific to the current thread.

### Use a Lock

When creating a custom logging handler, it's often helpful to use a lock. A lock is an object that is used to synchronize access to a resource.

The java.util.logging.Handler class defines a setLock() method that can be used to set the lock for a handler. By default, this method is called when a handler is created.

If we're using a custom lock, we need to make sure that the lock is thread-safe. This is because the lock may be accessed by multiple threads.

One way to ensure that a lock is thread-safe is to use the java.util.concurrent.locks.ReentrantLock class. This class defines a lock that can be used by multiple threads.

Another way to ensure that a lock is thread-safe is to use the java.util.concurrent.locks.Lock class. This class wraps an existing lock and synchronizes all of the lock's methods.

##Conclusion

In this article, we've seen how to create a custom logging handler in Java. We've also seen how to register our handler with the java.util.logging.LogManager. Finally, we've looked at some best practices for creating and using logging handlers.