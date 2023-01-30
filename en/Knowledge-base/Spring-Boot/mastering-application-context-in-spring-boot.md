---
title: Mastering Application Context in Spring Boot
description: 
published: true
date: 2023-01-30T00:58:30.825Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:58:30.825Z
---

- [Spring Boot에서 애플리케이션 컨텍스트 마스터하기***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/mastering-application-context-in-spring-boot)
{.links-list}


ApplicationContext is the central interface in the Spring framework for providing configuration information to an application. Bootstrap context and standalone XML application contexts are also available for certain special use cases.

ApplicationContext provides:

BeanFactoryPostProcessor-instances to post-process the application context itself.

ApplicationListener-instances to receive events from the context (such as ContextRefreshedEvent).

MessageSource for resolving messages, such as for I18N.

Hierarchical context structure with parent and child contexts.

PropertyResourceConfigurer delegates to allow for pluggable property sources.

Ability to resolve environment property sources such as system properties and environment variables through ConfigurableEnvironment.

ClassPathXmlApplicationContext and FileSystemXmlApplicationContext, the latter also supporting XmlWebApplicationContext for use in a Web environment.

AnnotationConfigApplicationContext, for supporting annotated beans classes in JavaConfig.

JndiObjectFactoryBean for accessing remote resources through JNDI.

 CORBA naming context.


WebApplicationContext, the context interface for a Web environment.

ConfigurableWebApplicationContext, the subinterface of WebApplicationContext that allows for programmatic registration and configuration of message sources, theme sources, and other.

The default ApplicationContext implementations are:

AnnotationConfigApplicationContext
ClassPathXmlApplicationContext
FileSystemXmlApplicationContext

TheApplicationContext can be used to access any object in the Spring IoC container. The getBean() method is overloaded with several signatures to achieve different goals:

Return an instance of the specified bean name.
Return an instance of the specified bean name, creating it if it does not exist.
Return an instance of the specified bean name, with the specified type.
Return an instance of the specified bean name, with the specified type, creating it if it does not exist.

Note that getBean() is a generic method and can be used with any type. However, the other overloaded methods are more type-safe. If a bean does not exist, and the "create" flag is false, getBean() will return null. If the "create" flag is true, getBean() will create the bean before returning it.

The other overloaded methods will throw an exception if the bean does not exist and the "create" flag is false. If the "create" flag is true, these methods will create the bean before returning it. These overloaded methods are more type-safe than the generic getBean() method and should be used whenever possible.

The ApplicationContext is also capable of resolve environment property sources such as system properties and environment variables through the ConfigurableEnvironment interface.

To get started with using the ApplicationContext, refer to the following code snippet.


import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext();
        ctx.register(AppConfig.class);
        ctx.refresh();
        MyService myService = ctx.getBean(MyService.class);
        myService.doStuff();
    }
}
In the above code snippet, we:

Create an AnnotationConfigApplicationContext.
Register the configuration class, AppConfig.
Refresh the application context.
Retrieve the MyService bean from the application context.
Invoke the doStuff() method on the MyService bean.

The ApplicationContext is a central interface in the Spring framework and provides many features and services. In this post, we've looked at some of the basics of using the ApplicationContext.