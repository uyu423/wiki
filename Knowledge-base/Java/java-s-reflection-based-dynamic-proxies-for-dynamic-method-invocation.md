---
title: 동적 메서드 호출을 위한 Java의 리플렉션 기반 동적 프록시
description: 
published: true
date: 2023-03-02T04:32:20.873Z
tags: 
editor: markdown
dateCreated: 2023-03-02T04:32:19.533Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's Reflection-based Dynamic Proxies for Dynamic Method Invocation***English** document is available*](/en/Knowledge-base/Java/java-s-reflection-based-dynamic-proxies-for-dynamic-method-invocation)
{.links-list}


Java의 리플렉션 API는 개체에서 동적으로 메서드를 호출하는 메커니즘을 제공합니다. 이는 대상 개체를 래핑하는 프록시 개체를 생성하여 수행됩니다. 프록시 개체는 모든 메서드 호출을 가로채 대상 개체로 전달합니다.

Java의 리플렉션 API는 매우 강력하지만 사용하기 어려울 수 있습니다. 주요 문제는 개체에서 어떤 메서드를 사용할 수 있는지 알기 어렵고 올바른 인수를 사용하여 메서드를 호출하는 방법을 알기 어렵다는 것입니다.

동적 프록시는 이러한 문제를 해결하는 데 도움이 될 수 있습니다. 동적 프록시는 다른 개체를 래핑하고 모든 메서드 호출을 가로채는 개체입니다. 그런 다음 프록시는 해당 메서드의 자체 구현을 제공하거나 래핑된 개체에 메서드 호출을 전달할 수 있습니다.

동적 프록시는 Proxy.newProxyInstance() 메서드를 호출하여 생성됩니다. 이 메서드는 세 가지 인수를 사용합니다.

- 사용할 ClassLoader. 이것은 일반적으로 대상 객체의 ClassLoader입니다.
- 구현할 인터페이스의 배열입니다. 이것은 일반적으로 대상 객체가 구현하는 인터페이스입니다.
- InvocationHandler. 이것은 프록시에서 메소드가 호출될 때 실행될 코드를 포함하는 객체입니다.

InvocationHandler 객체는 invoke() 메서드를 구현해야 합니다. 이 메서드는 세 가지 인수를 사용합니다.

- 프록시 객체.
- 호출된 메서드의 이름입니다.
- 인수의 배열입니다.

invoke() 메서드는 원하는 모든 작업을 수행할 수 있습니다. 값을 반환하거나 예외를 발생시키거나 메서드 호출을 래핑된 개체로 전달할 수 있습니다.

다음은 동적 프록시의 간단한 예입니다.

```java
public class MyInvocationHandler implements InvocationHandler {
    private Object target;

    public MyInvocationHandler(Object target) {
        this.target = target;
    }

    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("Before method " + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("After method " + method.getName());
        return result;
    }
}
```

이 InvocationHandler는 각 메서드가 호출되기 전과 후에 메시지를 인쇄합니다. 어떻게 사용할 수 있는지 봅시다:

```java
public class Foo {
    public void doSomething() {
        System.out.println("Doing something");
    }
}
```

```java
Foo foo = new Foo();
InvocationHandler handler = new MyInvocationHandler(foo);
Class<?> proxyClass = Proxy.getProxyClass(Foo.class.getClassLoader(), new Class[] { Foo.class });
Foo proxy = (Foo) proxyClass.getConstructor(new Class[] { InvocationHandler.class }).newInstance(new Object[] { handler });
proxy.doSomething();
```

이 코드는 Foo 클래스에 대한 프록시를 만듭니다. 프록시는 각 메서드가 호출되기 전과 후에 메시지를 인쇄합니다. 이 코드의 출력은 다음과 같습니다.

메소드 doSomething 이전
뭔가를하고
메소드 doSomething 이후

보시다시피 프록시는 원래 객체처럼 사용할 수 있습니다. invoke() 메서드는 원하는 모든 작업을 수행할 수 있으므로 필요한 모든 동작을 구현할 수 있습니다.

동적 프록시에는 몇 가지 제한 사항이 있습니다. 인터페이스를 구현하는 개체에만 사용할 수 있습니다. 다른 클래스를 확장하는 클래스와 함께 사용할 수 없습니다. 그리고 그들은 최종 클래스와 함께 사용할 수 없습니다.

이러한 제한에도 불구하고 동적 프록시는 매우 강력한 도구입니다. 모든 종류의 흥미로운 동작을 구현하는 데 사용할 수 있습니다.

추가 정보:

- https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Proxy.html
- https://docs.oracle.com/javase/tutorial/reflect/proxy.html