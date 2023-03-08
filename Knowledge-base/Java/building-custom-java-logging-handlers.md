---
title: 사용자 지정 Java 로깅 처리기 빌드
description: 
published: true
date: 2023-02-07T05:17:59.099Z
tags: 
editor: markdown
dateCreated: 2023-02-07T05:17:57.424Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Custom Java Logging Handlers***English** document is available*](/en/Knowledge-base/Java/building-custom-java-logging-handlers)
{.links-list}


# 커스텀 자바 로깅 핸들러 만들기

Java 플랫폼은 시스템 전체 이벤트의 로깅 및 기록을 위한 내장 지원을 제공합니다. 즉시 사용할 수 있는 많은 옵션 외에도 Java 개발자는 자체 사용자 정의 로깅 처리기를 만들 수도 있습니다.

로깅 핸들러는 로거에서 로그 레코드를 수신하고 파일, 콘솔 또는 원격 서버와 같은 대상으로 내보내는 역할을 하는 개체입니다.

이 기사에서는 Java에서 사용자 정의 로깅 핸들러를 빌드하는 방법을 살펴보겠습니다. 또한 로깅 처리기를 만들고 사용하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

## 사용자 지정 로깅 처리기 만들기

Java에서 사용자 지정 로깅 핸들러를 만드는 것은 2단계 프로세스입니다. 먼저 java.util.logging.Handler 클래스를 확장하는 클래스를 만들어야 합니다. 이 클래스는 사용자 지정 처리기의 동작을 정의합니다.

다음으로 핸들러를 java.util.logging.LogManager에 등록해야 합니다. 이는 프로그래밍 방식으로 또는 구성 파일을 사용하여 수행할 수 있습니다.

각 접근 방식의 예를 살펴보겠습니다.

### 프로그래밍 방식 등록

프로그래밍 방식 등록은 사용자 지정 로깅 핸들러를 등록하는 가장 간단한 방법입니다. LogManager.addHandler() 메서드를 호출하여 이를 수행할 수 있습니다. 이 메서드는 사용자 지정 Handler 클래스의 인스턴스를 매개 변수로 허용합니다.

예를 들면 다음과 같습니다.

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

위의 예에서 먼저 사용자 지정 Handler 클래스의 인스턴스를 만듭니다. 다음으로 LogManager에서 루트 로거를 가져옵니다. 마지막으로 핸들러를 루트 로거에 추가합니다.

### 구성 파일 등록

구성 파일 등록은 프로그래밍 방식 등록보다 약간 더 복잡하지만 더 많은 유연성을 제공합니다.

구성 파일 등록을 사용하여 Java 애플리케이션의 "conf" 디렉토리에 "logging.properties"라는 파일을 생성해야 합니다. 이 파일에는 Java 로깅 시스템을 구성하는 여러 속성이 포함되어 있습니다.

다음은 logging.properties 파일의 예입니다.

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

위의 예에서 사용자 지정 처리기에 대한 여러 속성을 정의했습니다. 첫 번째 속성인 "level"은 핸들러의 로깅 수준을 지정합니다. 두 번째 속성인 "포맷터"는 핸들러에서 사용할 포맷터를 지정합니다. 세 번째 속성인 "encoding"은 핸들러에서 사용할 문자 인코딩을 지정합니다.

## 사용자 지정 로깅 핸들러 생성을 위한 모범 사례

이제 Java에서 사용자 지정 로깅 핸들러를 만드는 방법을 살펴보았으므로 로깅 핸들러를 만들고 사용하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

### 간단하게 유지

사용자 지정 로깅 핸들러를 만들 때 디자인을 단순하게 유지하는 것이 중요합니다. 좋은 경험 법칙은 꼭 필요한 메서드만 재정의하는 것입니다.

예를 들어 java.util.logging.Handler 클래스는 로그 레코드를 처리하기 위한 여러 메서드를 정의합니다. 그러나 publish() 메서드만 재정의하면 됩니다. 다른 메서드는 그대로 둘 수 있습니다.

### 기존 핸들러를 시작점으로 사용

사용자 지정 로깅 핸들러를 만들 때 기존 핸들러를 시작점으로 사용하는 것이 유용한 경우가 많습니다. 예를 들어 java.util.logging.ConsoleHandler 클래스는 로그 레코드를 콘솔에 쓰는 간단한 핸들러입니다.

로그 레코드를 파일에 쓰는 핸들러를 만드는 경우 java.util.logging.FileHandler 클래스를 시작점으로 사용할 수 있습니다. 이 클래스는 로그 레코드를 파일에 쓰는 데 필요한 모든 메서드를 정의합니다.

### 로거의 스레드를 차단하지 마십시오.

사용자 지정 로깅 핸들러를 만들 때 로거의 스레드를 차단하지 않는 것이 중요합니다. 차단 핸들러로 인해 로거가 로그 레코드 처리를 중지할 수 있습니다.

로거의 스레드 차단을 피하는 한 가지 방법은 로그 레코드 내보내기에 별도의 스레드를 사용하는 것입니다. 예를 들어 java.util.logging.AsyncHandler 클래스는 로그 레코드를 내보내기 위해 별도의 스레드를 사용합니다.

로거의 스레드 차단을 피하는 또 다른 방법은 대기열을 사용하는 것입니다. java.util.logging.QueueHandler 클래스는 대기열을 사용하여 로그 레코드를 저장합니다. 그런 다음 별도의 스레드에서 레코드를 내보냅니다.

### 포맷터 사용

사용자 지정 로깅 핸들러를 만들 때 포맷터를 사용하는 것이 중요합니다. 포맷터는 로그 레코드를 문자열로 변환하는 역할을 하는 개체입니다.

java.util.logging.Handler 클래스는 핸들러의 포맷터를 설정하는 데 사용할 수 있는 setFormatter() 메소드를 정의합니다. 기본적으로 이 메서드는 핸들러가 생성될 때 호출됩니다.

사용자 지정 포맷터를 사용하는 경우 포맷터가 스레드로부터 안전한지 확인해야 합니다. 포맷터가 여러 스레드에서 호출될 수 있기 때문입니다.

포맷터가 스레드로부터 안전한지 확인하는 한 가지 방법은 java.util.logging.ThreadLocalFormatter 클래스를 사용하는 것입니다. 이 클래스는 현재 스레드에 고유한 포맷터를 정의합니다.

포맷터가 스레드로부터 안전한지 확인하는 또 다른 방법은 java.util.logging.SynchronizedFormatter 클래스를 사용하는 것입니다. 이 클래스는 기존 포맷터를 래핑하고 모든 포맷터의 메서드를 동기화합니다.

### 필터 사용

사용자 정의 로깅 핸들러를 생성할 때 필터를 사용하는 것이 종종 도움이 됩니다. 필터는 처리기가 내보내야 하는 로그 레코드를 결정하는 개체입니다.

java.util.logging.Handler 클래스는 핸들러에 대한 필터를 설정하는 데 사용할 수 있는 setFilter() 메소드를 정의합니다. 기본적으로 이 메서드는 핸들러가 생성될 때 호출됩니다.

사용자 지정 필터를 사용하는 경우 필터가 스레드로부터 안전한지 확인해야 합니다. 이는 필터가 여러 스레드에서 호출될 수 있기 때문입니다.

필터가 스레드로부터 안전한지 확인하는 한 가지 방법은 java.util.logging.SynchronizedFilter 클래스를 사용하는 것입니다. 이 클래스는 기존 필터를 래핑하고 필터의 모든 메서드를 동기화합니다.

필터가 스레드로부터 안전한지 확인하는 또 다른 방법은 java.util.logging.ThreadLocalFilter 클래스를 사용하는 것입니다. 이 클래스는 현재 스레드에 특정한 필터를 정의합니다.

### 잠금 사용

사용자 지정 로깅 핸들러를 만들 때 잠금을 사용하는 것이 도움이 되는 경우가 많습니다. 잠금은 리소스에 대한 액세스를 동기화하는 데 사용되는 개체입니다.

java.util.logging.Handler 클래스는 핸들러에 대한 잠금을 설정하는 데 사용할 수 있는 setLock() 메소드를 정의합니다. 기본적으로 이 메서드는 핸들러가 생성될 때 호출됩니다.

사용자 지정 잠금을 사용하는 경우 잠금이 스레드로부터 안전한지 확인해야 합니다. 여러 스레드에서 잠금에 액세스할 수 있기 때문입니다.

잠금이 스레드로부터 안전한지 확인하는 한 가지 방법은 java.util.concurrent.locks.ReentrantLock 클래스를 사용하는 것입니다. 이 클래스는 여러 스레드에서 사용할 수 있는 잠금을 정의합니다.

잠금이 스레드로부터 안전한지 확인하는 또 다른 방법은 java.util.concurrent.locks.Lock 클래스를 사용하는 것입니다. 이 클래스는 기존 잠금을 래핑하고 잠금의 모든 메서드를 동기화합니다.

## 결론

이 기사에서는 Java에서 사용자 정의 로깅 핸들러를 작성하는 방법을 살펴보았습니다. 또한 핸들러를 java.util.logging.LogManager에 등록하는 방법도 살펴보았습니다. 마지막으로 로깅 처리기를 만들고 사용하기 위한 몇 가지 모범 사례를 살펴보았습니다.