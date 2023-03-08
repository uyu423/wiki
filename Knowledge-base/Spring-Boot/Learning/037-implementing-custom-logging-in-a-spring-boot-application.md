---
title: 037: Spring Boot 애플리케이션에서 사용자 정의 로깅 구현
description: 
published: true
date: 2023-02-04T05:32:25.740Z
tags: 
editor: markdown
dateCreated: 2023-02-04T05:32:24.120Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [037: Implementing custom logging in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/037-implementing-custom-logging-in-a-spring-boot-application)
{.links-list}


# Spring Boot 애플리케이션에서 사용자 정의 로깅 구현

이 게시물에서는 Spring Boot 애플리케이션에서 사용자 지정 로깅을 구현하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* Spring Boot 애플리케이션을 위한 Log4j2 구성
* 커스텀 Log4j2 어펜더 만들기
* 사용자 지정 어펜더를 사용하여 데이터베이스에 이벤트 로깅

## Spring Boot 애플리케이션을 위한 Log4j2 구성

Log4j2는 Java 애플리케이션용으로 널리 사용되는 로깅 라이브러리입니다. Spring Boot는 Log4j2를 기본적으로 지원합니다. Spring Boot 애플리케이션에 대해 Log4j2를 구성하려면 클래스 경로에 Log4j2 구성 파일을 추가해야 합니다. Log4j2 구성 파일의 이름은 log4j2.xml 또는 log4j2.yaml이어야 합니다.

다음은 모든 메시지를 콘솔에 기록하는 간단한 Log4j2 구성 파일입니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
  </Appenders>
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
    </Root>
  </Loggers>
</Configuration>
```

Log4j2 구성 파일에서 사용할 appender를 지정해야 합니다. 이 예에서는 모든 메시지를 콘솔에 기록하는 콘솔 어펜더를 사용하고 있습니다. 또한 사용할 로거를 지정해야 합니다. 이 예에서 우리는 루트 로거를 사용하고 있으며 이전에 정의한 콘솔 어펜더를 참조하고 있습니다.

## 커스텀 Log4j2 어펜더 만들기

데이터베이스에 이벤트를 기록하려면 사용자 지정 Log4j2 어펜더를 생성해야 합니다. Log4j2 appender는 로그를 기록할 위치를 지정할 수 있는 플러그인입니다. 우리의 경우 데이터베이스에 로그를 기록하려고 합니다.

사용자 정의 appender는 다음 인터페이스를 구현해야 합니다.

```java
public interface Appender {
 
    void start();
 
    void stop();
 
    boolean isStarted();
 
    void append(LogEvent event);
 
    Layout getLayout();
 
    void setLayout(Layout layout);
 
    ErrorHandler getErrorHandler();
 
    void setErrorHandler(ErrorHandler errorHandler);
 
    Name getName();
 
    boolean ignoresThrowable();
}
```

사용자 지정 appender의 스켈레톤 구현을 생성하여 시작할 수 있습니다.

```java
public class DatabaseAppender implements Appender {
 
    @Override
    public void start() {
 
    }
 
    @Override
    public void stop() {
 
    }
 
    @Override
    public boolean isStarted() {
        return false;
    }
 
    @Override
    public void append(LogEvent event) {
 
    }
 
    @Override
    public Layout getLayout() {
        return null;
    }
 
    @Override
    public void setLayout(Layout layout) {
 
    }
 
    @Override
    public ErrorHandler getErrorHandler() {
        return null;
    }
 
    @Override
    public void setErrorHandler(ErrorHandler errorHandler) {
 
    }
 
    @Override
    public Name getName() {
        return null;
    }
 
    @Override
    public boolean ignoresThrowable() {
        return false;
    }
}
```

start() 메서드에서 데이터베이스 연결을 초기화해야 합니다. stop() 메서드에서 데이터베이스 연결을 닫아야 합니다. append() 메서드에서 로그 이벤트를 데이터베이스에 삽입해야 합니다.

## 사용자 정의 어펜더를 사용하여 데이터베이스에 이벤트 로깅

이제 사용자 지정 appender가 있으므로 이를 사용하도록 Log4j2를 구성해야 합니다. Log4j2 구성 파일에 다음을 추가하여 이를 수행할 수 있습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
 
    <DatabaseAppender name="DatabaseAppender">
      <ConnectionString>jdbc:mysql://localhost:3306/test</ConnectionString>
      <DriverClassName>com.mysql.jdbc.Driver</DriverClassName>
      <UserName>root</UserName>
      <Password>root</Password>
    </DatabaseAppender>
  </Appenders>
 
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
      <AppenderRef ref="DatabaseAppender"/>
    </Root>
  </Loggers>
</Configuration>
```

Log4j2 구성 파일에 <DatabaseAppender> 요소를 추가했습니다. 이 요소에는 설정해야 하는 몇 가지 속성이 있습니다.

* ConnectionString: 데이터베이스에 대한 JDBC 연결 문자열
* DriverClassName: JDBC 드라이버 클래스 이름
* UserName: 데이터베이스 사용자 이름
* 비밀번호: 데이터베이스 비밀번호

또한 루트 로거에 <AppenderRef> 요소를 추가했습니다. 이 요소는 DatabaseAppender를 참조합니다.

이제 사용자 지정 appender를 구성했으므로 이를 사용하여 데이터베이스에 이벤트를 기록할 수 있습니다.