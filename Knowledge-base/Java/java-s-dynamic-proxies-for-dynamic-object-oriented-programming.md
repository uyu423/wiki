---
title: 동적 객체 지향 프로그래밍을 위한 Java의 동적 프록시
description: 
published: true
date: 2023-02-03T06:23:35.225Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:23:33.657Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's Dynamic Proxies for Dynamic Object Oriented Programming***English** document is available*](/en/Knowledge-base/Java/java-s-dynamic-proxies-for-dynamic-object-oriented-programming)
{.links-list}



# 동적 객체 지향 프로그래밍을 위한 Java의 동적 프록시

Java의 동적 프록시를 사용하면 유형이 안전한 객체 지향 방식으로 동적 코드를 생성할 수 있습니다. 이 기사에서는 동적 프록시를 사용하여 동적 코드를 생성하는 방법과 이를 실제 애플리케이션에서 사용할 수 있는 방법을 살펴봅니다.

## 동적 프록시란 무엇입니까?

동적 프록시는 런타임에 지정된 인터페이스 목록을 구현하는 클래스입니다. 메서드가 동적 프록시 인스턴스에서 호출되면 메서드 호출이 Proxy 클래스의 invoke() 메서드로 전달되어 호출을 적절한 메서드 핸들러로 디스패치합니다.

동적 프록시는 원래 코드를 수정하지 않고 개체에 기능을 추가하는 데 사용할 수 있는 개체 주위에 "래퍼"를 만드는 데 사용할 수 있습니다. 예를 들어 동적 프록시를 사용하여 개체의 모든 메서드 호출에 로깅을 추가하거나 메서드 호출을 허용하기 전에 보안 검사를 추가할 수 있습니다.

## 동적 프록시 생성

동적 프록시 생성은 비교적 간단합니다. 먼저 Proxy 클래스의 인스턴스를 만들고 프록시하려는 클래스의 ClassLoader와 프록시가 구현해야 하는 인터페이스 배열을 전달해야 합니다. 예를 들어:

```java
ClassLoader classLoader = MyObject.class.getClassLoader();
Class[] interfaces = new Class[] { MyObject.class };

MyObject myObject = (MyObject) Proxy.newProxyInstance(classLoader, interfaces, new MyObjectInvocationHandler(myObject));
```

위의 예에서는 Proxy 클래스를 사용하여 MyObject 클래스에 대한 동적 프록시를 만듭니다. MyObject 클래스는 지정된 ClassLoader에 의해 로드 가능해야 하며 MyObject 인터페이스를 구현해야 합니다. Proxy.newProxyInstance() 메서드의 세 번째 인수는 프록시에서 메서드 호출 처리를 담당하는 InvocationHandler의 인스턴스입니다.

위의 예에서 메서드 호출을 원래 개체로 전달하는 간단한 InvocationHandler를 만들었습니다. 그러나 메서드 호출 로깅 또는 보안 검사 추가와 같은 고유한 논리를 InvocationHandler에 쉽게 추가할 수 있습니다.

## 동적 프록시 사용

동적 프록시를 생성하면 다른 개체와 마찬가지로 사용할 수 있습니다. 예를 들어 MyObject 클래스에 대한 동적 프록시가 있는 경우 원본 객체에서와 마찬가지로 프록시에서 메서드를 호출할 수 있습니다.

```java
myObject.doSomething();
```

## 동적 프록시를 사용하는 이유는 무엇입니까?

동적 프록시는 동적 코드를 생성하기 위한 강력한 도구입니다. 원본 코드를 수정하지 않고 개체에 기능을 추가하는 데 사용할 수 있습니다. 이는 소스 코드에 액세스할 수 없는 상황에서 매우 유용할 수 있습니다.

동적 프록시는 개체의 인터페이스를 변경하지 않고 개체에 기능을 추가하는 데 사용할 수 있는 "래퍼" 개체를 만드는 데 사용할 수도 있습니다. 예를 들어 동적 프록시를 사용하여 개체의 인터페이스를 변경하지 않고 개체에 대한 모든 메서드 호출에 로깅을 추가하는 개체 주위에 래퍼를 만들 수 있습니다.

## 동적 프록시를 사용하는 경우

동적 프록시는 원래 코드를 수정하지 않고 개체에 기능을 추가해야 하는 상황에서 매우 유용할 수 있습니다. 또한 개체의 인터페이스를 변경하지 않고 개체에 기능을 추가하는 데 사용할 수 있는 "래퍼" 개체를 만드는 데 사용할 수 있습니다.

## 동적 프록시를 사용하지 않는 경우

동적 프록시는 성능에 영향을 줄 수 있는 간접 레이어를 추가하므로 성능이 중요한 상황에서는 사용하면 안 됩니다. Proxy 클래스는 기본적으로 JVM에서 지원하지 않으므로 기본 객체를 기본 메서드로 전달해야 하는 상황에서도 사용해서는 안 됩니다.

## 결론

동적 프록시는 동적 코드를 생성하기 위한 강력한 도구입니다. 원본 코드를 수정하지 않고 개체에 기능을 추가하는 데 사용할 수 있습니다. 이는 소스 코드에 액세스할 수 없는 상황에서 매우 유용할 수 있습니다. 동적 프록시는 개체의 인터페이스를 변경하지 않고 개체에 기능을 추가하는 데 사용할 수 있는 "래퍼" 개체를 만드는 데 사용할 수도 있습니다.