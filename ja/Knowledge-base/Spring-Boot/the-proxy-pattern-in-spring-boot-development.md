---
title: Spring Boot 開発におけるプロキシ パターン
description: 
published: true
date: 2023-02-17T18:15:19.069Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:57:26.204Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [The Proxy Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-proxy-pattern-in-spring-boot-development)
{.links-list}


#Spring Boot Developmentのプロキシパターン

プロキシパターンは、オブジェクトが他のオブジェクトに代わって機能できるようにするソフトウェアデザインパターンです。 Spring Bootでは、プロキシデザインパターンを使用して2つのBean間の通信を有効にしたり、元のBeanで見つからなかった追加機能を提供したりできます。プロキシはXMLまたはJavaコードで定義できます。

Spring Bootでプロキシデザインパターンを使用するときに使用できる2つの主な種類のプロキシがあります。

- **BeanNameAutoProxyCreator**
- **DefaultAdvisorAutoProxyCreator**

## BeanNameAutoProxyCreator

BeanNameAutoProxyCreator は、プロキシが必要な Bean を自動検出してプロキシを生成するプロキシ作成者です。このプロキシ作成者は、Bean名を表示し、Bean名がプロキシされているBeanの名前と一致する場合は、プロキシを適用して機能します。たとえば、「myService」というBeanがあり、このBeanをプロキシする場合は、次のXML構成を使用します。

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

上記の構成では、BeanNameAutoProxyCreator Beanを定義し、「myService」Beanをプロキシするように指定しました。また、このプロキシへのインターセプタとして "myInterceptor" Beanを使用するように指定しました。

## DefaultAdvisorAutoProxyCreator

DefaultAdvisorAutoProxyCreator は、プロキシが必要な Bean を自動検出してプロキシを生成するプロキシ作成者です。このプロキシ作成者は、「@EnableAspectJAutoProxy」アノテーションでコメント付きのBeanを調べて、そのプロキシを生成します。たとえば、「myService」というBeanがあり、このBeanをプロキシする場合は、次のXML構成を使用します。

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

上記の設定では、DefaultAdvisorAutoProxyCreator Beanを定義し、「myInterceptor」Beanをこのプロキシのインターセプタとして使用するように指定しました。プロキシする Bean を明示的に定義していませんが、「@EnableAspectJAutoProxy」で「myService」 Bean に注釈を付けたため、この Bean は DefaultAdvisorAutoProxyCreator によってプロキシされます。

##結論

プロキシデザインパターンは、Spring Bootで2つのBean間の通信を可能にしたり、元のBeanで見つからなかった追加機能を提供するために使用できる便利なパターンです。プロキシはXMLまたはJavaコードで定義でき、Spring Bootで使用できる2つの主要なプロキシタイプ、BeanNameAutoProxyCreatorとDefaultAdvisorAutoProxyCreatorがあります。