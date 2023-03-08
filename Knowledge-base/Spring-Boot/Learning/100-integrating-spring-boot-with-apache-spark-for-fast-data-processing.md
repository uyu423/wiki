---
title: 100: 빠른 데이터 처리를 위해 Apache Spark와 Spring Boot 통합
description: 
published: true
date: 2023-02-06T04:32:30.387Z
tags: 
editor: markdown
dateCreated: 2023-02-06T04:32:28.731Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [100: Integrating Spring Boot with Apache Spark for Fast Data Processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/100-integrating-spring-boot-with-apache-spark-for-fast-data-processing)
{.links-list}


## 100: 빠른 데이터 처리를 위해 Apache Spark와 Spring Boot 통합

이 게시물에서는 빠른 데이터 처리를 위해 Spring Boot를 Apache Spark와 통합하는 방법을 보여줍니다.

Spark는 대용량 데이터 세트를 처리하기 위한 강력한 도구이며 빅 데이터 커뮤니티에서 점점 인기를 얻고 있습니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 인기 있는 Java 프레임워크입니다.

이 두 가지 프레임워크를 통합하면 데이터를 빠르고 효율적으로 처리할 수 있습니다. 이번 포스트에서는 그 방법을 알려드리겠습니다.

Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. 그런 다음 Spark에 필요한 종속성을 추가합니다. 마지막으로 간단한 Spark 작업을 작성하고 로컬 개발 환경에서 실행합니다.

### 스프링 부트 애플리케이션 만들기

먼저 Spring Boot 애플리케이션을 만듭니다. Spring Initializr를 사용하여 프로젝트를 생성합니다.

Spring Initializr 웹 사이트(https://start.spring.io/)로 이동합니다.

다음 값으로 양식을 작성하십시오.

* 그룹: com.example
* 아티팩트: 데모
* 이름: 데모
* 설명: Spring Boot 및 Apache Spark용 데모 프로젝트
* 패키지 이름: com.example.demo
* 유형: 메이븐 프로젝트
* 포장: 항아리
* 자바 버전: 8
* "Spring Boot Starters" 섹션에서 "Web" 체크박스를 선택합니다.

"프로젝트 생성"을 클릭합니다.

이제 프로젝트 구조가 포함된 zip 파일이 있어야 합니다. 파일의 압축을 풀고 원하는 IDE에서 엽니다.

### 필요한 의존성 추가하기

다음으로 Spark에 필요한 종속성을 추가합니다. 다음 종속성이 필요합니다.

* 스파크 코어
* 스파크-SQL

pom.xml 파일에 다음을 추가하여 프로젝트에 이러한 종속성을 추가할 수 있습니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.apache.spark</groupId>
        <artifactId>spark-core_2.11</artifactId>
        <version>2.4.4</version>
    </dependency>
    <dependency>
        <groupId>org.apache.spark</groupId>
        <artifactId>spark-sql_2.11</artifactId>
        <version>2.4.4</version>
    </dependency>
</dependencies>
```

### Spark 작업 작성

이제 프로젝트가 설정되었으므로 간단한 Spark 작업을 작성할 수 있습니다. SparkJob.java라는 새 Java 클래스를 만드는 것으로 시작하겠습니다.

SparkJob 클래스에서 먼저 SparkSession을 만듭니다. SparkSession은 Spark SQL의 진입점입니다. 이를 통해 다양한 데이터 소스에서 데이터를 읽고 SQL 쿼리를 수행할 수 있습니다.

다음으로 데이터 세트를 읽습니다. 항공사 비행 데이터의 샘플 데이터 세트를 사용합니다. 데이터 세트는 CSV 형식이며 http://stat-computing.org/dataexpo/2009/2008.csv.bz2에서 사용할 수 있습니다.

데이터 세트가 있으면 테이블로 등록합니다. 이를 통해 SQL 쿼리를 실행할 수 있습니다.

마지막으로 간단한 SQL 쿼리를 실행하여 각 항공사의 항공편 수를 계산합니다.

SparkJob 클래스의 전체 코드는 다음과 같습니다.

```java
package com.example.demo;

import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class SparkJob {

    public static void main(String[] args) {
        SparkSession spark = SparkSession
                .builder()
                .appName("Spark Demo")
                .getOrCreate();

        String dataFile = "data/2008.csv.bz2";
        Dataset<Row> df = spark.read().format("csv")
                .option("header", "true")
                .option("inferSchema", "true")
                .load(dataFile);

        df.createOrReplaceTempView("flights");

        Dataset<Row> airlines = spark.sql("SELECT DISTINCT Carrier FROM flights");

        for (Row row : airlines.collectAsList()) {
            String airline = row.getString(0);
            Dataset<Row> flights = spark.sql("SELECT * FROM flights WHERE Carrier = '" + airline + "'");
            long numFlights = flights.count();
            System.out.println(airline + ": " + numFlights);
        }

        spark.stop();
    }

}
```

### 스파크 작업 실행

이제 Spark 작업이 작성되었으므로 로컬 개발 환경에서 실행할 수 있습니다.

이렇게 하려면 먼저 로컬 Spark 인스턴스를 시작해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
$SPARK_HOME/bin/spark-shell --master local[*]
```

Spark가 실행되면 Spark 작업을 제출할 수 있습니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
spark-submit --class com.example.demo.SparkJob --master local[*] target/demo-0.0.1-SNAPSHOT.jar
```

모든 것이 잘 진행되면 다음과 유사한 출력이 표시됩니다.

```
American: 12359
Continental: 7261
Delta: 20216
United: 13721
US Airways: 10429
```

그리고 그게 다야! 이제 Apache Spark와 Spring Boot를 성공적으로 통합했습니다.