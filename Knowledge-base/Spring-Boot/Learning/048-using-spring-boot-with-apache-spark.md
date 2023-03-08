---
title: 048: 아파치 스파크와 함께 스프링 부트 사용하기
description: 
published: true
date: 2023-02-04T14:32:59.188Z
tags: 
editor: markdown
dateCreated: 2023-02-04T14:32:57.533Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [048: Using Spring Boot with Apache Spark***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/048-using-spring-boot-with-apache-spark)
{.links-list}




# Apache Spark와 함께 Spring Boot 사용

Spark는 속도, 사용 편의성 및 정교한 분석을 중심으로 구축된 강력한 오픈 소스 처리 엔진입니다. Spark와 Spring Boot의 조합이 데이터 집약적인 애플리케이션을 구축하는 데 널리 사용되는 것은 놀라운 일이 아닙니다.

이 게시물에서는 Spark 및 Spring Boot를 사용하여 시작하는 방법을 보여줍니다. Spark 애플리케이션을 만들고 실행하는 방법을 포함하여 Spark 작업의 기본 사항을 다룹니다. 또한 Spring Boot를 사용하여 Spark 작업을 더욱 쉽게 만드는 방법도 보여줍니다.

## 스파크란?

Spark는 대규모 데이터 처리를 위한 빠르고 일반적인 엔진입니다. 원래 UC Berkeley의 AMPLab에서 개발되었으며 현재 많은 회사와 개인의 기여로 Apache 프로젝트가 되었습니다.

Spark는 간단한 데이터 ETL에서 복잡한 기계 학습 및 그래프 처리에 이르기까지 광범위한 애플리케이션에서 사용하도록 설계되었습니다. Spark는 반복 계산, 대화형 쿼리 또는 스트리밍 데이터와 관련된 사용 사례에 특히 적합합니다.

Spark는 SQL, DataFrames, Datasets 및 다양한 기계 학습 알고리즘에 대한 지원을 포함하여 풍부한 기능 세트를 제공합니다. 또한 Spark는 Hadoop, Cassandra 및 Kafka와 같은 다른 인기 있는 빅 데이터 도구와 함께 사용할 수 있습니다.

## 스파크 시작하기

Spark는 독립 실행형 애플리케이션, 스크립트 또는 다른 프로그래밍 언어용 라이브러리를 포함하여 다양한 방식으로 사용할 수 있습니다. 이 섹션에서는 Scala에서 간단한 Spark 애플리케이션을 만들고 실행하는 방법을 보여줍니다.

### 스파크 애플리케이션 만들기

Spark 애플리케이션 생성의 첫 번째 단계는 SparkConf 클래스를 확장하는 클래스를 정의하는 것입니다. SparkConf 클래스를 사용하면 Spark 마스터의 위치 및 Spark 애플리케이션에 사용할 메모리 양과 같은 Spark 설정을 구성할 수 있습니다.



클래스 MySparkConf 확장 SparkConf {
   재정의 def getAll: Map[String, String] = {
     지도(
       "spark.master" -> "로컬[*]",
       "spark.executor.memory" -> "1g"
     )
   }
}

다음으로 SparkContext 클래스의 인스턴스를 만들어야 합니다. SparkContext 클래스는 Spark 애플리케이션의 기본 진입점입니다. Spark 클러스터에 대한 연결을 나타내며 RDD, DataFrame 및 Dataset을 생성하는 데 사용됩니다.



val sc = new SparkContext(new MySparkConf())

이제 SparkContext가 있으므로 Spark 애플리케이션 생성을 시작할 수 있습니다. 이 예제에서는 텍스트 파일의 단어 수를 세는 간단한 응용 프로그램을 만듭니다.

먼저 SparkContext.textFile 메서드를 사용하여 텍스트 파일을 읽어야 합니다. 이 메서드는 문자열의 RDD를 반환하며 각 문자열은 텍스트 파일의 한 줄입니다.



val textFile = sc.textFile("/path/to/file.txt")

다음으로 RDD.flatMap 메서드를 사용하여 각 줄을 단어로 분할할 수 있습니다. flatMap 메서드는 원래 RDD의 각 요소에 함수를 적용한 결과를 포함하는 새 RDD를 반환합니다. 이 경우 함수는 각 줄을 단어로 나눕니다.



val words = textFile.flatMap(line => line.split(" "))

마지막으로 RDD.count 메서드를 사용하여 RDD의 단어 수를 계산할 수 있습니다.



값 개수 = words.count()

### 스파크 애플리케이션 실행

Spark 애플리케이션은 spark-submit 스크립트를 사용하여 실행할 수 있습니다. spark-submit 스크립트는 Spark 애플리케이션의 위치 및 사용할 메모리 양을 포함하여 여러 인수를 사용합니다.

위의 예제 애플리케이션을 실행하려면 다음 명령을 사용합니다.

spark-submit --class MySparkApp --master local[*] --executor-memory 1g /path/to/jar/file.jar

## 스파크와 함께 스프링 부트 사용하기

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 인기 있는 Java 프레임워크입니다. Spring Boot는 특히 마이크로서비스 생성에 적합합니다.

독립 실행형 Spring 애플리케이션을 만드는 프로세스를 단순화하는 것 외에도 Spring Boot를 사용하면 Spark를 비롯한 다양한 데이터 소스를 쉽게 사용할 수 있습니다.

이 섹션에서는 Spring Boot를 사용하여 Spark 애플리케이션을 만드는 방법을 보여줍니다. 이전 섹션의 동일한 예제 애플리케이션을 사용하지만 Spring Boot를 사용하여 애플리케이션 생성 및 실행 프로세스를 단순화합니다.

### 스프링 부트 애플리케이션 만들기

Spring Boot 애플리케이션을 만드는 첫 번째 단계는 새 Maven 프로젝트를 만드는 것입니다. Maven 호환 IDE를 사용하여 이를 수행할 수 있습니다.

프로젝트의 pom.xml 파일에서 다음 종속성을 추가해야 합니다.

스프링 부트 스타터 부모
스프링 부트 스타터 웹
스프링 부트 스타터 데이터 스파크

spring-boot-starter-parent 종속성은 모든 Spring Boot 종속성의 상위 POM입니다. spring-boot-starter-web 종속성은 Spring MVC에 대한 지원을 추가하는 데 사용됩니다. spring-boot-starter-data-spark 종속성은 Spark에 대한 지원을 추가하는 데 사용됩니다.

다음으로 @SpringBootApplication 주석이 달린 새 클래스를 만들어야 합니다. 이 클래스에는 애플리케이션의 기본 메서드가 포함됩니다.



@SpringBootApplication
공개 클래스 MyApplication {

   공개 정적 무효 메인(문자열[] 인수) {
      SpringApplication.run(MyApplication.class, args);
   }
}

@SpringBootApplication 주석은 애플리케이션에 다음 주석을 모두 추가하는 데 사용되는 편리한 주석입니다.

@Configuration: 이 주석은 클래스에 Spring 애플리케이션에 대한 구성 정보가 포함되어 있음을 나타내는 데 사용됩니다.

@EnableAutoConfiguration: 이 주석은 Spring 애플리케이션의 자동 구성을 활성화하는 데 사용됩니다.

@ComponentScan: 이 주석은 Spring 애플리케이션의 구성 요소 스캔을 활성화하는 데 사용됩니다.

### 스파크 작업 생성

Spark 작업을 생성하려면 @Configuration 및 @EnableSpark 주석이 달린 새 클래스를 생성해야 합니다. @Configuration 주석은 클래스에 Spring 애플리케이션에 대한 구성 정보가 포함되어 있음을 나타내는 데 사용됩니다. @EnableSpark 주석은 Spring 애플리케이션에서 Spark를 활성화하는 데 사용됩니다.



@구성
@EnableSpark
공개 클래스 MySparkJob {

   @Autowired
   개인 SparkContext sparkContext;

   @Autowired
   개인 SparkConf sparkConf;

   @콩
   공개 SparkJob sparkJob() {
      // ... SparkJob 생성 및 반환
   }
}

@Autowired 주석은 SparkContext 및 SparkConf를 Spark 작업에 주입하는 데 사용됩니다. @Bean 주석은 메서드가 Spring 빈을 생성함을 나타내는 데 사용됩니다.

sparkJob 메서드에서 SparkJob을 생성하고 반환해야 합니다. SparkJob은 Spark 애플리케이션을 나타내는 Spring 관리 구성 요소입니다.



@구성
@EnableSpark
공개 클래스 MySparkJob {

   @Autowired
   개인 SparkContext sparkContext;

   @Autowired
   개인 SparkConf sparkConf;

   @콩
   공개 SparkJob sparkJob() {
      새 SparkJob() 반환 {
         @우세하다
         공공 무효 실행() {
            // ... 스파크 작업 실행
         }
      };
   }
}

run 메서드에서 애플리케이션에 대한 Spark 코드를 추가할 수 있습니다. 이 예제에서는 이전 섹션과 동일한 코드를 사용합니다.



@구성
@EnableSpark
공개 클래스 MySparkJob {

   @Autowired
   개인 SparkContext sparkContext;

   @Autowired
   개인 SparkConf sparkConf;

   @콩
   공개 SparkJob sparkJob() {
      새 SparkJob() 반환 {
         @우세하다
         공공 무효 실행() {
            val textFile = sparkContext.textFile("/path/to/file.txt")
            val words = textFile.flatMap(line => line.split(" "))
            값 개수 = words.count()
         }
      };
   }
}

### 스프링 부트 애플리케이션 실행

Spring Boot 애플리케이션은 spring-boot-run 목표를 사용하여 실행할 수 있습니다. 이 목표는 Maven 플러그인 또는 Spring Boot 명령줄 도구를 사용하여 실행할 수 있습니다.

위의 예제 애플리케이션을 실행하려면 다음 명령을 사용합니다.

mvn spring-boot:실행

## 결론

이 게시물에서는 Spark 및 Spring Boot를 사용하여 시작하는 방법을 보여 주었습니다. Spark 애플리케이션을 만들고 실행하는 방법을 포함하여 Spark 작업의 기본 사항을 다루었습니다. 또한 Spring Boot를 사용하여 Spark 작업을 훨씬 더 쉽게 만드는 방법도 보여 주었습니다.

Spark 및 Spring Boot에 대해 자세히 알아보려면 사용할 수 있는 훌륭한 리소스가 많이 있습니다. 특히 다음을 권장합니다.

- Spark 빠른 시작 가이드: https://spark.apache.org/docs/latest/quick-start.html
- 스프링 부트 문서: https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/
- The Spark with Spring Boot 가이드: https://spring.io/guides/gs/spark-on-spring-boot/