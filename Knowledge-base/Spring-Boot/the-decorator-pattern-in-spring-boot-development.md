---
title: 스프링 부트 개발의 데코레이터 패턴
description: 
published: true
date: 2023-02-08T16:32:25.925Z
tags: 
editor: markdown
dateCreated: 2023-02-08T16:32:24.338Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Decorator Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-decorator-pattern-in-spring-boot-development)
{.links-list}


# 스프링 부트 개발의 데코레이터 패턴

데코레이터 패턴은 핵심 기능을 변경하지 않고 기존 개체를 수정할 수 있는 소프트웨어 디자인 패턴입니다. 이는 원하는 기능을 포함하는 데코레이터 개체로 원래 개체를 래핑하여 수행됩니다.

Spring Boot에서 Decorator 패턴을 사용하여 코드를 변경하지 않고 기존 빈에 새로운 기능을 동적으로 추가할 수 있습니다. 이는 원하는 기능을 포함하는 데코레이터 빈으로 원래 빈을 래핑하여 수행됩니다.

예를 들어 메시지를 포함하는 간단한 bean이 있다고 가정해 보겠습니다.

```java
public class MessageBean {
  
  private String message;
  
  public MessageBean(String message) {
    this.message = message;
  }
  
  public String getMessage() {
    return message;
  }
}
```

Decorator 패턴을 사용하여 코드를 변경하지 않고 이 빈에 새로운 기능을 동적으로 추가할 수 있습니다. 예를 들어 메시지에 타임스탬프를 추가하는 데코레이터 빈을 만들 수 있습니다.

```java
public class TimestampDecorator implements MessageBean {
  
  private MessageBean messageBean;
  
  public TimestampDecorator(MessageBean messageBean) {
    this.messageBean = messageBean;
  }
  
  @Override
  public String getMessage() {
    return messageBean.getMessage() + " - " + new Date();
  }
}
```

이제 MessageBean을 코드에 삽입할 때 TimestampDecorator를 사용하도록 지정할 수 있습니다.

```java
@Autowired
@Qualifier("timestampDecorator")
private MessageBean messageBean;
```

이렇게 하면 getMessage() 메서드를 호출할 때 메시지에 현재 타임스탬프가 추가됩니다.

```java
messageBean.getMessage(); // "Hello World! - Thu Jan 01 00:00:00 EST 1970"
```

데코레이터 패턴은 코드를 변경하지 않고 기존 빈에 새로운 기능을 동적으로 추가하는 유용한 방법입니다. 타임스탬프, 로깅, 보안 또는 기타 원하는 기능을 추가하는 데 사용할 수 있습니다.