---
title: Understanding Java's Attach API for Dynamic Instrumentation
description: 
published: true
date: 2023-03-06T04:32:35.829Z
tags: 
editor: markdown
dateCreated: 2023-03-06T04:32:35.829Z
---

- [동적 계측을 위한 Java의 Attach API 이해***Korean** document is available*](/ko/Knowledge-base/Java/understanding-java-s-attach-api-for-dynamic-instrumentation)
{.links-list}



Understanding Java's Attach API for Dynamic Instrumentation

Java's Attach API is a powerful mechanism for attaching to a running Java Virtual Machine (JVM) and injecting instrumentation agents into it. Dynamic instrumentation is the process of injecting code into a running application to intercept method calls, monitor performance, and gather data about an application's behavior. The Attach API is a critical tool for developers and operations teams because it allows them to monitor and control running applications without the need for application restarts or code changes.

## Why Use the Attach API?

The Attach API is especially useful in production environments where downtime is not an option. It allows developers to investigate and troubleshoot production issues without interrupting users or causing application downtime. By attaching to a running JVM, developers can dynamically instrument an application's code to gather data and metrics.

The Attach API also enables developers to perform real-time debugging and profiling without affecting performance. By monitoring an application's behavior in real-time, developers can uncover performance bottlenecks and prevent crashes before they occur.

## How to Use the Attach API

The Attach API consists of two main components: the attaching process and the agent process. The attaching process is responsible for connecting to a running JVM and loading the agent process. The agent process is responsible for injecting instrumentation code into the JVM.

### Attaching to a Running JVM

To attach to a running JVM, you need to know the process ID (PID) of the JVM. You can find the PID of a running JVM using the `jps` command-line tool. Once you have the PID, you can connect to the JVM using the `VirtualMachine` class and its `attach` method.

```java
import com.sun.tools.attach.VirtualMachine;

VirtualMachine vm = VirtualMachine.attach("12345");
```

The `attach` method returns a `VirtualMachine` object that represents the attached JVM.

### Loading an Agent

Once you have attached to the JVM, you can load an agent using the `loadAgent` method of the `VirtualMachine` class. The `loadAgent` method takes the path to the agent JAR file as its argument.

```java
vm.loadAgent("/path/to/agent.jar");
```

The agent JAR file must contain a class that extends the `java.lang.instrument.Instrumentation` class. This class is responsible for defining the instrumentation code that will be injected into the JVM.

### Implementing an Agent

The `Instrumentation` class provides several methods for defining instrumentation code, including the `addTransformer` method, which is used to define a `ClassFileTransformer` object. The `ClassFileTransformer` object is responsible for transforming the bytecode of loaded classes.

Here's an example of an agent that uses the `addTransformer` method to intercept method calls:

```java
import java.lang.instrument.ClassFileTransformer;
import java.lang.instrument.Instrumentation;
import java.security.ProtectionDomain;

public class MyAgent {
  public static void premain(String agentArgs, Instrumentation inst) {
    inst.addTransformer(new MyClassTransformer());
  }

  static class MyClassTransformer implements ClassFileTransformer {
    public byte[] transform(ClassLoader loader, String className, Class<?> classBeingRedefined,
        ProtectionDomain protectionDomain, byte[] classfileBuffer) {
      // Transform the bytecode of the loaded class
      return null;
    }
  }
}
```

The `premain` method is the entry point for the agent and is invoked when the agent is loaded. It takes two arguments: `agentArgs`, which is a string containing any command-line arguments passed to the agent, and `inst`, which is the `Instrumentation` object.

The `MyClassTransformer` class is a `ClassFileTransformer` implementation that intercepts method calls. The `transform` method is called by the JVM whenever a new class is loaded. The method takes the bytecode of the loaded class as its argument and returns the transformed bytecode.

### Deploying an Agent

To deploy an agent to a running JVM, you need to package the agent code into a JAR file and include a manifest file that specifies the `Premain-Class` attribute. The `Premain-Class` attribute specifies the name of the class that contains the `premain` method.

Here's an example manifest file:

```
Manifest-Version: 1.0
Premain-Class: com.example.MyAgent
```

To deploy the agent, you can use the `java` command-line tool with the `-javaagent` option:

```bash
java -javaagent:/path/to/agent.jar -jar myapp.jar
```

## Conclusion

Java's Attach API is a powerful tool for dynamically instrumenting running applications. By attaching to a running JVM, developers can inject instrumentation code to monitor performance, gather data, and troubleshoot production issues. The Attach API is a critical tool for developers and operations teams because it allows them to gain insight into running applications without the need for application restarts or code changes.

## References

- [Java SE Attach API](https://docs.oracle.com/en/java/javase/14/docs/api/java.attach/module-summary.html)
- [Dynamic Instrumentation with the Java Virtual Machine](https://www.oracle.com/technical-resources/articles/java/instrumentation.html)
- [Java Instrumentation](https://www.baeldung.com/java-instrumentation)