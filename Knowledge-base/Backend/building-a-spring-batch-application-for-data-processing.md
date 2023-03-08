---
title: 데이터 처리를 위한 Spring Batch 애플리케이션 구축
description: 
published: true
date: 2023-02-18T12:07:50.192Z
tags: 
editor: markdown
dateCreated: 2023-02-18T12:07:43.342Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building a Spring Batch Application for Data Processing***English** document is available*](/en/Knowledge-base/Backend/building-a-spring-batch-application-for-data-processing)
{.links-list}


# 데이터 처리를 위한 Spring Batch 애플리케이션 구축

## 소개

Spring Batch는 엔터프라이즈 시스템을 위한 강력한 처리 프레임워크입니다. 그것은
대량의 고성능 일괄 처리 작업을 처리하도록 설계되었습니다.

이 기사에서는 Spring Batch 애플리케이션을 개발하는 방법을 보여줍니다.
CSV 파일에서 데이터를 읽고 XML 파일에 씁니다. 우리는 Maven을 사용하여
프로젝트 종속성을 관리합니다.


## 스프링 배치란?

Spring Batch는 다음을 개발하기 위한 경량의 엔터프라이즈급 프레임워크입니다.
강력한 배치 응용 프로그램. Spring Batch는 재사용 가능한 기능을 제공합니다.
로깅/추적을 포함하여 대량의 기록을 처리하는 데 필수적인
트랜잭션 관리, 작업 처리 통계, 작업 재시작, 건너뛰기 및
자원 관리.

Spring Batch는 Spring의 POJO 기반 개발 접근 방식을 기반으로 합니다.
모든 Java 개발 환경에서 쉽게 사용할 수 있는 프레임워크입니다. 열쇠
Spring Framework의 장점은 레이어 케이크 아키텍처입니다.
경량을 사용하여 엔터프라이즈급 애플리케이션을 개발할 수 있습니다.
하부 구조.

Spring Batch Framework의 주요 목표는 강력한
배치 애플리케이션을 위한 실행 프레임워크. 또한 다음을 위한 기반을 제공합니다.
사용자 지정 배치 작업 구현.

## 시스템 요구 사항

이 예에서는 다음 시스템 요구 사항을 사용합니다.

- JDK 1.8
- 메이븐 3.0+

## 프로젝트 구조

우리 프로젝트의 구조는 다음과 같습니다.

```
├── pom.xml
├── src
│   └── main
│       └── java
│           └── com
│               └── javacodegeeks
│                   └── spring
│                       └── batch
│                           └── App.java
└── src
    └── main
        └── resources
            ├── input
            │   └── input.csv
            └── spring
                └── batch
                    └── jobs
                        └── job-config.xml
```

## 메이븐 종속성

프로젝트에 다음 Maven 종속성을 사용합니다.

- `spring-boot-starter-batch`: Spring Batch 사용을 위한 스타터
- `org.springframework.batch:spring-batch-infrastructure`: 코어 포함
프레임워크의 기능
- `org.codehaus.jackson:jackson-mapper-asl`:
개체에 대한 CSV 파일
- `org.hsqldb:hsqldb`: 처리된 레코드를 저장하기 위한 인메모리 데이터베이스

우리의 `pom.xml`은 다음과 같을 것입니다:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.javacodegeeks.spring.batch</groupId>
    <artifactId>spring-batch-example</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>spring-batch-example</name>
    <description>Spring Batch Example</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-batch</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.batch</groupId>
            <artifactId>spring-batch-infrastructure</artifactId>
            <version>3.0.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.codehaus.jackson</groupId>
            <artifactId>jackson-mapper-asl</artifactId>
            <version>1.9.13</version>
        </dependency>
        <dependency>
            <groupId>org.hsqldb</groupId>
            <artifactId>hsqldb</artifactId>
            <version>2.4.0</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

## 스프링 배치 작업

Spring Batch의 작업은 독립적인 객체를 캡슐화하는 엔터티입니다.
응집력있는 작업 단위. 작업은 하나 이상의 단계로 구성되며 각 단계는
단계는 작업의 독립적이고 순차적인 단계입니다. 각 단계에는
잠재적으로 복잡한 알고리즘, 계산 및
비즈니스 규칙.

다음은 두 가지로 구성된 Spring Batch 작업의 간단한 예입니다.
단계. 첫 번째 단계는 CSV 파일에서 데이터를 읽고
XML 파일에 씁니다. 두 번째 단계는 데이터를 읽는 Tasklet입니다.
XML 파일을 인메모리 데이터베이스에 기록합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="http://www.springframework.org/schema/batch"
    xmlns:beans="http://www.springframework.org/schema/beans" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/batch
        http://www.springframework.org/schema/batch/spring-batch.xsd">

    <beans:import resource="../config/context.xml"/>

    <beans:bean id="jobRepository" class="org.springframework.batch.core.repository.support.MapJobRepositoryFactoryBean">
        <beans:property name="transactionManager" ref="transactionManager"/>
    </beans:bean>

    <beans:bean id="transactionManager" class="org.springframework.batch.support.transaction.ResourcelessTransactionManager"/>

    <job-repository id="jobRepository" data-source="dataSource"/>

    <beans:bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
        <beans:property name="driverClassName" value="org.hsqldb.jdbcDriver"/>
        <beans:property name="url" value="jdbc:hsqldb:mem:testdb"/>
        <beans:property name="username" value="sa"/>
        <beans:property name="password" value=""/>
    </beans:bean>

    <beans:bean id="jobLauncher" class="org.springframework.batch.core.launch.support.SimpleJobLauncher">
        <beans:property name="jobRepository" ref="jobRepository"/>
    </beans:bean>

    <beans:bean id="csvFile" class="org.springframework.core.io.FileSystemResource" scope="step">
        <beans:constructor-arg value="#{jobParameters[csvFile]}"/>
    </beans:bean>

    <beans:bean id="xmlFile" class="org.springframework.core.io.FileSystemResource" scope="step">
        <beans:constructor-arg value="#{jobParameters[xmlFile]}"/>
    </beans:bean>

    <job id="job1" xmlns="http://www.springframework.org/schema/batch">
        <step id="step1">
            <tasklet>
                <chunk reader="csvFileItemReader" writer="xmlFileItemWriter" commit-interval="10"/>
            </tasklet>
        </step>
        <step id="step2">
            <tasklet>
                <chunk reader="xmlFileItemReader" writer="dbItemWriter" commit-interval="10"/>
            </tasklet>
        </step>
    </job>

    <beans:bean id="csvFileItemReader" class="org.springframework.batch.item.file.FlatFileItemReader">
        <beans:property name="resource" ref="csvFile"/>
        <beans:property name="lineMapper">
            <beans:bean class="org.springframework.batch.item.file.mapping.DefaultLineMapper">
                <beans:property name="lineTokenizer">
                    <beans:bean class="org.springframework.batch.item.file.transform.DelimitedLineTokenizer">
                        <beans:property name="names" value="id,name,dept,salary"/>
                    </beans:bean>
                </beans:property>
                <beans:property name="fieldSetMapper">
                    <beans:bean class="org.springframework.batch.item.file.mapping.BeanWrapperFieldSetMapper">
                        <beans:property name="targetType" value="com.javacodegeeks.spring.batch.Employee"/>
                    </beans:bean>
                </beans:property>
            </beans:bean>
        </beans:property>
    </beans:bean>

    <beans:bean id="xmlFileItemWriter" class="org.springframework.batch.item.xml.StaxEventItemWriter">
        <beans:property name="resource" ref="xmlFile"/>
        <beans:property name="marshaller" ref="employeeMarshaller"/>
        <beans:property name="rootTagName" value="employees"/>
    </beans:bean>

    <beans:bean id="employeeMarshaller" class="org.springframework.oxm.jaxb.Jaxb2Marshaller">
        <beans:property name="classesToBeBound">
            <beans:list>
                <beans:value>com.javacodegeeks.spring.batch.Employee</beans:value>
            </beans:list>
        </beans:property>
    </beans:bean>

    <beans:bean id="dbItemWriter" class="org.springframework.batch.item.database.JdbcBatchItemWriter">
        <beans:property name="dataSource" ref="dataSource"/>
        <beans:property name="sql" value="INSERT INTO EMPLOYEE (ID, NAME, DEPT, SALARY) VALUES (:id, :name, :dept, :salary)"/>
        <beans:property name="itemSqlParameterSourceProvider">
            <beans:bean class="org.springframework.batch.item.database.BeanPropertyItemSqlParameterSourceProvider"/>
        </beans:property>
    </beans:bean>

    <beans:bean id="xmlFileItemReader" class="org.springframework.batch.item.xml.StaxEventItemReader">
        <beans:property name="resource" ref="xmlFile"/>
        <beans:property name="fragmentRootElementName" value="employee"/>
        <beans:property name="unmarshaller" ref="employeeMarshaller"/>
    </beans:bean>

</beans:beans>
```

## 1단계: CSV 파일에서 읽기

작업의 첫 번째 단계에서는 CSV 파일에서 데이터를 읽고 씁니다.
XML 파일로. FlatFileItemReader를 사용하여 CSV에서 데이터를 읽습니다.
파일.

FlatFileItemReader는 플랫 파일에서 데이터를 읽고 각 줄을
물체. 이 예제에서는 각 줄을 Employee 개체에 매핑합니다.

DelimitedLineTokenizer를 사용하여 CSV 파일의 각 줄을 토큰화합니다.
DelimitedLineTokenizer는 추상의 하위 클래스입니다.
LineTokenizer 클래스. 라인을 필드로 분할하여 라인을 토큰화합니다.

BeanWrapperFieldSetMapper를 사용하여 토큰을 Employee에 매핑합니다.
개체 속성. BeanWrapperFieldSetMapper는 BeanWrapperFieldSetMapper의 하위 클래스입니다.
추상 FieldSetMapper 클래스. FieldSet의 데이터를 다음으로 매핑합니다.
JavaBean의 속성.

## 2단계: XML 파일에 쓰기

작업의 두 번째 단계에서는 XML 파일에서 데이터를 읽고 작성합니다.
메모리 내 데이터베이스에 저장합니다. StaxEventItemWriter를 사용하여 작성합니다.
데이터를 XML 파일로.

StaxEventItemWriter는 추상의 하위 클래스입니다.
AbstractStaxEventItemWriter 클래스. 다음을 사용하여 XML 파일에 항목을 씁니다.
StAX(XML용 스트리밍 API).

Jaxb2Marshaller를 사용하여 Employee 개체를 XML로 마샬링합니다. 그만큼
Jaxb2Marshaller는 추상의 하위 클래스입니다.
마샬러 클래스. XML과 Java 객체를 마샬링합니다.

## 3단계: 데이터베이스에 쓰기

작업의 세 번째 단계에서는 XML 파일에서 데이터를 읽고 작성합니다.
메모리 내 데이터베이스에 저장합니다. JdbcBatchItemWriter를 사용하여 작성합니다.
데이터를 데이터베이스로.

JdbcBatchItemWriter는 추상의 하위 클래스입니다.
JdbcItemWriter 클래스. JDBC를 사용하여 데이터베이스에 데이터를 씁니다.

제공하기 위해 BeanPropertyItemSqlParameterSourceProvider를 사용합니다.
Employee 객체의 SQL 매개변수. 그만큼
BeanPropertyItemSqlParameterSourceProvider는
추상 ItemSqlParameterSourceProvider 클래스. 그것은 제공합니다
JavaBean 속성의 SQL 매개변수.

## 작업 구성

`job-config.xml` 파일에서 작업을 구성합니다. 그만큼
`job-config.xml` 파일에는 작업에 대한 구성이 포함되어 있습니다.

## 작업 실행

다음 명령을 사용하여 작업을 실행합니다.

```
java -jar target/spring-batch-example-0.0.1-SNAPSHOT.jar --job.name=job1 --csvFile=./input/input.csv --xmlFile=./output/output.xml
```

## 결론

이 기사에서는 Spring Batch 애플리케이션을 개발하는 방법을 설명했습니다.
CSV 파일에서 데이터를 읽고 XML 파일에 씁니다. 방법도 보여드렸습니다.
XML 파일에서 데이터를 읽고 메모리 내 데이터베이스에 씁니다.