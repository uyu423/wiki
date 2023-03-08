---
title: The Proxy Pattern in Spring Boot Development
description: 
published: true
date: 2023-02-17T18:15:16.404Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:57:26.203Z
---

- [Spring Boot 개발의 프록시 패턴***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/the-proxy-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot 開発におけるプロキシ パターン***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/the-proxy-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的代理模式***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/the-proxy-pattern-in-spring-boot-development)
{.links-list}


# The Proxy Pattern in Spring Boot Development

The Proxy pattern is a software design pattern that enables an object to act on behalf of another object. In Spring Boot, the Proxy design pattern can be used to enable communication between two beans, or to provide extra functionality not found in the original bean. Proxies can be defined in either XML or Java code.

When using the Proxy design pattern in Spring Boot, there are two main types of proxies that can be used:

- **BeanNameAutoProxyCreator**
- **DefaultAdvisorAutoProxyCreator**

## BeanNameAutoProxyCreator

BeanNameAutoProxyCreator is a proxy creator that autodetects beans that need to be proxied and creates proxies for them. This proxy creator works by looking at the bean name and applying the proxy if the bean name matches the name of the bean that is being proxied. For example, if we have a bean named "myService", and we want to proxy this bean, we would use the following XML configuration:

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

In the above configuration, we have defined a BeanNameAutoProxyCreator bean, and specified that we want to proxy the "myService" bean. We have also specified that we want to use the "myInterceptor" bean as the interceptor for this proxy.

## DefaultAdvisorAutoProxyCreator

DefaultAdvisorAutoProxyCreator is a proxy creator that autodetects beans that need to be proxied and creates proxies for them. This proxy creator works by looking at the beans that have been annotated with the "@EnableAspectJAutoProxy" annotation and creates proxies for them. For example, if we have a bean named "myService", and we want to proxy this bean, we would use the following XML configuration:

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

In the above configuration, we have defined a DefaultAdvisorAutoProxyCreator bean, and specified that we want to use the "myInterceptor" bean as the interceptor for this proxy. We have not explicitly defined which beans we want to proxy, but since we have annotated the "myService" bean with "@EnableAspectJAutoProxy", this bean will be proxied by the DefaultAdvisorAutoProxyCreator.

## Conclusion

The Proxy design pattern is a useful pattern that can be used in Spring Boot to enable communication between two beans, or to provide extra functionality not found in the original bean. Proxies can be defined in either XML or Java code, and there are two main types of proxies that can be used in Spring Boot: BeanNameAutoProxyCreator and DefaultAdvisorAutoProxyCreator.