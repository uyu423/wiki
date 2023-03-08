---
title: 비동기 작업 관리를 위한 Java의 java.util.concurrent.CompletionService
description: 
published: true
date: 2023-02-03T22:55:16.447Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:55:11.466Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's java.util.concurrent.CompletionService for Asynchronous Task Management***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-completionservice-for-asynchronous-task-management)
{.links-list}


# 비동기 작업 관리를 위한 Java의 java.util.concurrent.CompletionService

Java의 `java.util.concurrent.CompletionService`는 비동기 작업을 관리하기 위한 강력한 도구입니다. 작업을 제출하고 진행 상황을 추적하고, 작업이 완료되면 알림을 받고, 필요한 경우 작업을 취소할 수도 있습니다.

다음은 `CompletionService`를 사용하여 작업을 제출하고 진행 상황을 추적하는 간단한 예입니다.

```java
// Create a CompletionService
CompletionService<String> service = new ExecutorCompletionService<>(executor);

// Submit a task
Future<String> future = service.submit(new Callable<String>() {
    @Override
    public String call() throws Exception {
        // Do some work
        return "Result";
    }
});

// Track the task's progress
while (!future.isDone()) {
    // Do something else
}

// Get the task's result
String result = future.get();
```

보시다시피 `CompletionService`를 사용하면 비동기 작업의 진행 상황을 쉽게 제출하고 추적할 수 있습니다. 또한 작업 완료 시 알림을 받고 필요한 경우 작업을 취소하는 편리한 방법을 제공합니다.

외부 리소스:

- [CompletionService용 JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletionService.html)
- [자바 동시성 튜토리얼: CompletionService](https://www.baeldung.com/java-completion-service)
- [Java Tip 67: Java CompletionService 사용](https://www.javaworld.com/article/2077322/java-tip-67--use-the-java-completion-service.html)