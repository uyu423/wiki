---
title: Spring Boot 개발의 프록시 패턴
description: 
published: true
date: 2023-02-17T18:15:17.756Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:57:26.204Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [The Proxy Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-proxy-pattern-in-spring-boot-development)
{.links-list}


# 스프링 부트 개발의 프록시 패턴

프록시 패턴은 개체가 다른 개체를 대신하여 작동할 수 있도록 하는 소프트웨어 디자인 패턴입니다. Spring Boot에서 프록시 디자인 패턴을 사용하여 두 빈 간의 통신을 활성화하거나 원래 빈에서 찾을 수 없는 추가 기능을 제공할 수 있습니다. 프록시는 XML 또는 Java 코드로 정의할 수 있습니다.

Spring Boot에서 프록시 디자인 패턴을 사용할 때 사용할 수 있는 두 가지 주요 유형의 프록시가 있습니다.

- **BeanNameAutoProxyCreator**
- **DefaultAdvisorAutoProxyCreator**

## BeanNameAutoProxyCreator

BeanNameAutoProxyCreator는 프록시가 필요한 빈을 자동 감지하고 프록시를 생성하는 프록시 작성자입니다. 이 프록시 작성자는 bean 이름을 보고 bean 이름이 프록시 중인 bean의 이름과 일치하는 경우 프록시를 적용하여 작동합니다. 예를 들어 "myService"라는 빈이 있고 이 빈을 프록시하려는 경우 다음 XML 구성을 사용합니다.

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

위의 구성에서 BeanNameAutoProxyCreator 빈을 정의하고 "myService" 빈을 프록시하도록 지정했습니다. 또한 이 프록시에 대한 인터셉터로 "myInterceptor" 빈을 사용하도록 지정했습니다.

## DefaultAdvisorAutoProxyCreator

DefaultAdvisorAutoProxyCreator는 프록시가 필요한 빈을 자동 감지하고 프록시를 생성하는 프록시 작성자입니다. 이 프록시 작성자는 "@EnableAspectJAutoProxy" 주석으로 주석이 달린 빈을 살펴보고 이에 대한 프록시를 생성합니다. 예를 들어 "myService"라는 빈이 있고 이 빈을 프록시하려는 경우 다음 XML 구성을 사용합니다.

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

위의 구성에서 우리는 DefaultAdvisorAutoProxyCreator 빈을 정의했고 "myInterceptor" 빈을 이 프록시의 인터셉터로 사용하도록 지정했습니다. 프록시할 빈을 명시적으로 정의하지 않았지만 "@EnableAspectJAutoProxy"로 "myService" 빈에 주석을 달았으므로 이 빈은 DefaultAdvisorAutoProxyCreator에 의해 프록시됩니다.

## 결론

프록시 디자인 패턴은 Spring Boot에서 두 빈 간의 통신을 가능하게 하거나 원래 빈에서 찾을 수 없는 추가 기능을 제공하는 데 사용할 수 있는 유용한 패턴입니다. 프록시는 XML 또는 Java 코드로 정의할 수 있으며 Spring Boot에서 사용할 수 있는 두 가지 주요 프록시 유형인 BeanNameAutoProxyCreator 및 DefaultAdvisorAutoProxyCreator가 있습니다.