---
title: Java's Reflection-based Dynamic Proxies for Dynamic Method Invocation
description: 
published: true
date: 2023-03-02T04:32:26.635Z
tags: 
editor: markdown
dateCreated: 2023-03-02T04:32:19.535Z
---

- [동적 메서드 호출을 위한 Java의 리플렉션 기반 동적 프록시***Korean** document is available*](/ko/Knowledge-base/Java/java-s-reflection-based-dynamic-proxies-for-dynamic-method-invocation)
{.links-list}


Java's reflection API provides a mechanism for dynamically invoking methods on objects. This is done by creating a proxy object that wraps the target object. The proxy object intercepts all method calls and forwards them to the target object.

Java's reflection API is very powerful, but it can be difficult to use. The main problems are that it is hard to know which methods are available on an object, and it is hard to know how to invoke a method with the correct arguments.

Dynamic proxies can help to solve these problems. A dynamic proxy is an object that wraps another object and intercepts all method calls. The proxy can then provide its own implementation of those methods, or it can forward the method call to the wrapped object.

Dynamic proxies are created by calling the Proxy.newProxyInstance() method. This method takes three arguments:

- The ClassLoader to use. This is typically the ClassLoader of the target object.
- An array of interfaces to implement. This is typically the interfaces that the target object implements.
- An InvocationHandler. This is an object that contains the code that will be executed when a method is called on the proxy.

The InvocationHandler object must implement the invoke() method. This method takes three arguments:

- The proxy object.
- The name of the method that was called.
- An array of arguments.

The invoke() method can do whatever it wants. It can return a value, throw an exception, or forward the method call to the wrapped object.

Here is a simple example of a dynamic proxy:

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

This InvocationHandler just prints a message before and after each method is called. Let's see how it can be used:

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

This code creates a proxy for the Foo class. The proxy will print a message before and after each method is called. The output of this code is:

Before method doSomething
Doing something
After method doSomething

As you can see, the proxy can be used just like the original object. The invoke() method can do whatever it wants, so it can implement any behavior that you need.

There are some limitations to dynamic proxies. They can only be used with objects that implement interfaces. They can't be used with classes that extend other classes. And they can't be used with final classes.

Despite these limitations, dynamic proxies are a very powerful tool. They can be used to implement all sorts of interesting behaviors.

Further reading:

- https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Proxy.html
- https://docs.oracle.com/javase/tutorial/reflect/proxy.html