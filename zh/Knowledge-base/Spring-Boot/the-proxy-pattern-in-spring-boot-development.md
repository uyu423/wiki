---
title: Spring Boot开发中的代理模式
description: 
published: true
date: 2023-02-17T18:15:20.411Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:57:26.243Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [The Proxy Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-proxy-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot 开发中的代理模式

代理模式是一种软件设计模式，它使一个对象能够代表另一个对象进行操作。在 Spring Boot 中，代理设计模式可用于启用两个 bean 之间的通信，或者提供原始 bean 中没有的额外功能。代理可以用 XML 或 Java 代码定义。

在 Spring Boot 中使用代理设计模式时，可以使用两种主要类型的代理：

- **BeanNameAutoProxyCreator**
- **DefaultAdvisorAutoProxyCreator**

## BeanNameAutoProxyCreator

BeanNameAutoProxyCreator 是一个代理创建器，它自动检测需要代理的 beans 并为它们创建代理。这个代理创建者通过查看 bean 名称并在 bean 名称与被代理的 bean 名称匹配时应用代理来工作。例如，如果我们有一个名为“myService”的 bean，并且我们想要代理这个 bean，我们将使用以下 XML 配置：

```xml
<beans>
    <bean class="org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator">
        <property name="beanNames">
            <list>
                <value>myService</value>
            </list>
        </property>
        <property name="interceptorNames">
            <list>
                <value>myInterceptor</value>
            </list>
        </property>
    </bean>

    <bean id="myService" class="com.example.MyService">
        <!-- service implementations -->
    </bean>

    <bean id="myInterceptor" class="com.example.MyInterceptor">
        <!-- interceptor implementations -->
    </bean>
</beans>
```

在上面的配置中，我们定义了一个 BeanNameAutoProxyCreator bean，并指定我们要代理“myService”bean。我们还指定要使用“myInterceptor”bean 作为此代理的拦截器。

## DefaultAdvisorAutoProxyCreator

DefaultAdvisorAutoProxyCreator 是一个代理创建器，它自动检测需要代理的 bean 并为它们创建代理。这个代理创建者通过查看用“@EnableAspectJAutoProxy”注释注释的 beans 来工作，并为它们创建代理。例如，如果我们有一个名为“myService”的 bean，并且我们想要代理这个 bean，我们将使用以下 XML 配置：

```xml
<beans>
    <bean class="org.springframework.aop.framework.autoproxy.DefaultAdvisorAutoProxyCreator">
        <property name="interceptorNames">
            <list>
                <value>myInterceptor</value>
            </list>
        </property>
    </bean>

    <bean id="myService" class="com.example.MyService">
        <!-- service implementations -->
    </bean>

    <bean id="myInterceptor" class="com.example.MyInterceptor">
        <!-- interceptor implementations -->
    </bean>
</beans>
```

在上面的配置中，我们定义了一个 DefaultAdvisorAutoProxyCreator bean，并指定我们要使用“myInterceptor”bean 作为此代理的拦截器。我们没有明确定义要代理哪些 bean，但是由于我们已经用“@EnableAspectJAutoProxy”注释了“myService”bean，所以这个 bean 将由 DefaultAdvisorAutoProxyCreator 代理。

## 结论

代理设计模式是一种有用的模式，可以在 Spring Boot 中使用它来启用两个 bean 之间的通信，或者提供原始 bean 中没有的额外功能。代理可以在 XML 或 Java 代码中定义，Spring Boot 中可以使用两种主要类型的代理：BeanNameAutoProxyCreator 和 DefaultAdvisorAutoProxyCreator。