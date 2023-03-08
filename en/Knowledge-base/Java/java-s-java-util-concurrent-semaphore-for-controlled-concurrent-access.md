---
title: Java's java.util.concurrent.Semaphore for Controlled Concurrent Access
description: 
published: true
date: 2023-02-02T01:23:28.895Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:23:24.787Z
---

- [java.util.concurrent.Semaphore de Java para acceso concurrente controlado***Spanish** document is available*](/es/Knowledge-base/Java/java-s-java-util-concurrent-semaphore-for-controlled-concurrent-access)
{.links-list}
- [用于受控并发访问的 Java java.util.concurrent.Semaphore***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/java-s-java-util-concurrent-semaphore-for-controlled-concurrent-access)
{.links-list}
- [제어된 동시 액세스를 위한 Java의 java.util.concurrent.Semaphore***Korean** document is available*](/ko/Knowledge-base/Java/java-s-java-util-concurrent-semaphore-for-controlled-concurrent-access)
{.links-list}


# Java's java.util.concurrent.Semaphore for Controlled Concurrent Access

In multi-threaded programming, it is often necessary to limit the number of threads that can access a resource or block of code at any given time. This is known as concurrency control.

One way to achieve concurrency control in Java is to use the `java.util.concurrent.Semaphore` class.

A semaphore is a token that allows a thread to enter a critical section, which is a block of code that can only be executed by one thread at a time. When the thread exits the critical section, it returns the semaphore to the pool.

A semaphore can be used to control access to any resource, not just code. For example, a semaphore can be used to control access to a printer or database.

## Creating a Semaphore

A semaphore is created by specifying the number of permits. This is the number of threads that can access the critical section at the same time. For example, to create a semaphore with 10 permits:

```java
Semaphore semaphore = new Semaphore(10);
```

## Requesting a Permit

A thread requests a permit by calling the `acquire()` method. This method blocks the thread until a permit is available. For example:

```java
semaphore.acquire();
```

## Releasing a Permit

When a thread exits the critical section, it calls the `release()` method to return the permit to the semaphore. For example:

```java
semaphore.release();
```

## Example

The following example shows how to use a semaphore to control access to a printer.

```java
import java.util.concurrent.Semaphore;

public class Printer {
    private Semaphore semaphore;

    public Printer(int numPermits) {
        semaphore = new Semaphore(numPermits);
    }

    public void print(String document) {
        try {
            semaphore.acquire();
            // print the document
        } catch (InterruptedException e) {
            // handle error
        } finally {
            semaphore.release();
        }
    }
}
```

In this example, the `print()` method acquires a permit before printing the document. If no permits are available, the `acquire()` method blocks the thread until one is available. After printing the document, the `release()` method returns the permit to the semaphore.

## Differences Between Semaphores and Locks

Semaphores and locks are both mechanisms for concurrency control. However, there are some key differences between them.

- A semaphore can have multiple permits, while a lock can only have one.
- A semaphore can be released by a thread that did not acquire it, while a lock can only be released by the thread that acquired it.
- A semaphore does not have a concept of ownership, while a lock does.

## Conclusion

Java's `java.util.concurrent.Semaphore` class provides a mechanism for concurrency control. Semaphores can be used to control access to any resource, not just code. When using semaphores, it is important to remember the differences between semaphores and locks.