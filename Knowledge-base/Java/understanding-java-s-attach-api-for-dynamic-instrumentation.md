---
title: 동적 계측을 위한 Java의 Attach API 이해
description: 
published: true
date: 2023-03-06T04:32:43.042Z
tags: 
editor: markdown
dateCreated: 2023-03-06T04:32:35.825Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Understanding Java's Attach API for Dynamic Instrumentation***English** document is available*](/en/Knowledge-base/Java/understanding-java-s-attach-api-for-dynamic-instrumentation)
{.links-list}



동적 계측을 위한 Java의 Attach API 이해

Java의 Attach API는 실행 중인 JVM(Java Virtual Machine)에 연결하고 여기에 계측 에이전트를 주입하기 위한 강력한 메커니즘입니다. 동적 계측은 실행 중인 애플리케이션에 코드를 삽입하여 메서드 호출을 가로채고 성능을 모니터링하며 애플리케이션 동작에 대한 데이터를 수집하는 프로세스입니다. Attach API는 애플리케이션을 다시 시작하거나 코드를 변경할 필요 없이 실행 중인 애플리케이션을 모니터링하고 제어할 수 있기 때문에 개발자와 운영 팀에게 중요한 도구입니다.

## Attach API를 사용하는 이유는 무엇입니까?

Attach API는 다운타임이 허용되지 않는 프로덕션 환경에서 특히 유용합니다. 이를 통해 개발자는 사용자를 방해하거나 애플리케이션 다운타임을 유발하지 않고 프로덕션 문제를 조사하고 해결할 수 있습니다. 실행 중인 JVM에 연결함으로써 개발자는 애플리케이션의 코드를 동적으로 계측하여 데이터 및 메트릭을 수집할 수 있습니다.

또한 Attach API를 사용하면 개발자가 성능에 영향을 주지 않고 실시간 디버깅 및 프로파일링을 수행할 수 있습니다. 애플리케이션의 동작을 실시간으로 모니터링함으로써 개발자는 성능 병목 현상을 발견하고 충돌이 발생하기 전에 방지할 수 있습니다.

## Attach API 사용 방법

Attach API는 첨부 프로세스와 에이전트 프로세스의 두 가지 주요 구성 요소로 구성됩니다. 연결 프로세스는 실행 중인 JVM에 연결하고 에이전트 프로세스를 로드하는 역할을 합니다. 에이전트 프로세스는 계측 코드를 JVM에 삽입하는 역할을 합니다.

### 실행 중인 JVM에 연결

실행 중인 JVM에 연결하려면 JVM의 프로세스 ID(PID)를 알아야 합니다. `jps` 명령줄 도구를 사용하여 실행 중인 JVM의 PID를 찾을 수 있습니다. PID가 있으면 `VirtualMachine` 클래스와 해당 `attach` 메서드를 사용하여 JVM에 연결할 수 있습니다.

```java
import com.sun.tools.attach.VirtualMachine;

VirtualMachine vm = VirtualMachine.attach("12345");
```

`attach` 메서드는 연결된 JVM을 나타내는 `VirtualMachine` 개체를 반환합니다.

### 에이전트 로드

JVM에 연결되면 `VirtualMachine` 클래스의 `loadAgent` 메소드를 사용하여 에이전트를 로드할 수 있습니다. `loadAgent` 메소드는 에이전트 JAR 파일의 경로를 인수로 사용합니다.

```java
vm.loadAgent("/path/to/agent.jar");
```

에이전트 JAR 파일은 `java.lang.instrument.Instrumentation` 클래스를 확장하는 클래스를 포함해야 합니다. 이 클래스는 JVM에 삽입될 계측 코드 정의를 담당합니다.

### 에이전트 구현

'Instrumentation' 클래스는 'ClassFileTransformer' 개체를 정의하는 데 사용되는 'addTransformer' 메서드를 포함하여 계측 코드를 정의하기 위한 여러 메서드를 제공합니다. `ClassFileTransformer` 개체는 로드된 클래스의 바이트코드 변환을 담당합니다.

다음은 메서드 호출을 가로채기 위해 `addTransformer` 메서드를 사용하는 에이전트의 예입니다.

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

`premain` 메소드는 에이전트의 진입점이며 에이전트가 로드될 때 호출됩니다. 에이전트에 전달된 명령줄 인수를 포함하는 문자열인 `agentArgs`와 `Instrumentation` 개체인 `inst`의 두 가지 인수를 사용합니다.

`MyClassTransformer` 클래스는 메서드 호출을 가로채는 `ClassFileTransformer` 구현입니다. `transform` 메소드는 새 클래스가 로드될 때마다 JVM에 의해 호출됩니다. 이 메서드는 로드된 클래스의 바이트 코드를 인수로 사용하고 변환된 바이트 코드를 반환합니다.

### 에이전트 배포

실행 중인 JVM에 에이전트를 배포하려면 에이전트 코드를 JAR 파일로 패키징하고 `Premain-Class` 특성을 지정하는 매니페스트 파일을 포함해야 합니다. `Premain-Class` 속성은 `premain` 메서드를 포함하는 클래스의 이름을 지정합니다.

다음은 매니페스트 파일의 예입니다.

```
Manifest-Version: 1.0
Premain-Class: com.example.MyAgent
```

에이전트를 배포하려면 `-javaagent` 옵션과 함께 `java` 명령줄 도구를 사용할 수 있습니다.

```bash
java -javaagent:/path/to/agent.jar -jar myapp.jar
```

## 결론

Java의 Attach API는 실행 중인 애플리케이션을 동적으로 계측하기 위한 강력한 도구입니다. 실행 중인 JVM에 연결함으로써 개발자는 계측 코드를 삽입하여 성능을 모니터링하고 데이터를 수집하며 생산 문제를 해결할 수 있습니다. Attach API는 애플리케이션을 다시 시작하거나 코드를 변경할 필요 없이 실행 중인 애플리케이션에 대한 통찰력을 얻을 수 있기 때문에 개발자와 운영 팀에게 중요한 도구입니다.

## 참조

- [Java SE 연결 API](https://docs.oracle.com/en/java/javase/14/docs/api/java.attach/module-summary.html)
- [자바 가상 머신을 사용한 동적 계측](https://www.oracle.com/technical-resources/articles/java/instrumentation.html)
- [자바 계측](https://www.baeldung.com/java-instrumentation)