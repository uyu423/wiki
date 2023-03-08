---
title: 모니터링을 위해 Java의 추적 가능 및 계측 클래스 사용
description: 
published: true
date: 2023-02-05T12:17:30.138Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:17:28.487Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using Java's Traceable and Instrumented Classes for Monitoring***English** document is available*](/en/Knowledge-base/Java/using-java-s-traceable-and-instrumented-classes-for-monitoring)
{.links-list}


# 모니터링을 위해 Java의 추적 가능하고 계측된 클래스 사용

계측 코드는 Java 애플리케이션의 성능을 모니터링하기 위한 강력한 기술입니다. 개발자는 Java의 Traceable 및 Instrumented 클래스를 사용하여 코드 실행 방법에 대한 자세한 정보를 수집하고 잠재적인 병목 현상을 식별할 수 있습니다.

계측은 메모리 사용, 가비지 수집 활동 및 스레드 실행을 포함하여 애플리케이션 성능의 여러 측면을 모니터링하는 데 사용할 수 있습니다. 이 문서에서는 계측을 사용하여 메서드 실행 시간을 모니터링하는 데 중점을 둘 것입니다.

## 계측을 사용하는 이유는 무엇입니까?

계측을 통해 개발자는 코드를 수정하지 않고도 성능 데이터를 수집할 수 있습니다. 이는 코드 변경 사항을 배포하기 어려울 수 있는 프로덕션 시스템을 모니터링하는 데 특히 유용합니다.

계측은 타사 라이브러리와 같이 개발자가 제어할 수 없는 코드를 모니터링하는 데에도 사용할 수 있습니다. 이 경우 계측을 사용하여 라이브러리가 어떻게 사용되고 있는지에 대한 데이터를 수집하고 잠재적인 성능 문제를 식별할 수 있습니다.

## Java의 추적 가능하고 계측된 클래스 사용

Java의 Traceable 및 Instrumented 클래스는 코드를 계측하고 성능 데이터를 수집하는 간단한 방법을 제공합니다. 이러한 클래스는 java.lang.instrument 패키지의 일부이며 Java 5 이상에서 사용할 수 있습니다.

Traceable 및 Instrumented 클래스를 사용하려면 개발자는 java.lang.instrument.Instrumentation의 하위 클래스를 만들고 premain() 메서드를 재정의해야 합니다. 이 메서드는 애플리케이션의 main() 메서드가 실행되기 전에 호출됩니다.

premain() 메서드에서 개발자는 Traceable 또는 Instrumented 하위 클래스의 인스턴스를 만들고 JVM(Java Virtual Machine)에 등록해야 합니다. 그런 다음 호출되는 메서드와 같은 특정 이벤트가 발생할 때 JVM은 Traceable 또는 Instrumented 하위 클래스의 메서드를 호출합니다.

다음은 메서드 호출 시간을 추적하는 Traceable 하위 클래스의 간단한 예입니다.

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

위의 예에서 traceMethodInvocation() 메서드는 메서드가 호출될 때마다 호출됩니다. methodInfo 매개 변수에는 메서드 이름 및 실행에 걸린 시간을 포함하여 메서드에 대한 정보가 포함됩니다.

traceMethodInvocation() 메서드는 메서드 호출 시간을 맵에 저장합니다. getMethodTimes() 메서드를 사용하여 지도를 검색할 수 있습니다.

MyTraceable 클래스를 JVM에 등록하려면 premain() 메서드를 사용할 수 있습니다.

```java
public static void premain(String args, Instrumentation instrumentation) {

instrumentation.addTransformer(new MyTraceable());

}
```

premain() 메서드에서 MyTraceable 클래스는 계측 개체에 등록됩니다. instrumentation 개체는 클래스 변환기를 JVM에 추가하는 데 사용됩니다. 클래스 변환기는 클래스가 JVM에 의해 로드되기 전에 클래스의 바이트코드를 수정하는 코드 조각입니다.

MyTraceable 클래스는 메서드가 호출될 때마다 traceMethodInvocation() 메서드가 호출되도록 클래스 변환기로 등록됩니다.

MyTraceable 클래스가 등록되면 애플리케이션을 평소처럼 실행할 수 있습니다. traceMethodInvocation() 메서드는 메서드가 호출될 때마다 호출되며 메서드 호출 시간은 MyTraceable 개체에서 추적됩니다.

## 데이터 분석

MyTraceable 클래스에서 수집한 데이터는 애플리케이션의 잠재적인 병목 현상을 식별하는 데 사용할 수 있습니다. 이를 위해 각 방법에 소요된 시간을 기준으로 데이터를 정렬할 수 있습니다.

실행하는 데 가장 오랜 시간이 걸리는 방법은 잠재적인 병목 현상입니다. 이러한 방법을 추가로 분석하여 최적화할 수 있는지 확인할 수 있습니다.

## 결론

계측은 Java 애플리케이션의 성능을 모니터링하기 위한 강력한 기술입니다. 개발자는 Java의 Traceable 및 Instrumented 클래스를 사용하여 코드 실행 방법에 대한 자세한 정보를 수집하고 잠재적인 병목 현상을 식별할 수 있습니다.