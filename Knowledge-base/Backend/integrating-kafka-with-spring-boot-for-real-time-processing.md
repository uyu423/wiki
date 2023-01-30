---
title: 실시간 처리를 위해 Kafka와 Spring Boot 통합
description: 
published: true
date: 2023-01-30T05:54:31.696Z
tags: 
editor: markdown
dateCreated: 2023-01-30T05:54:31.696Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Integrating Kafka with Spring Boot for Real-time Processing***English** version of this document is available*](/en/Knowledge-base/Backend/integrating-kafka-with-spring-boot-for-real-time-processing)
{.links-list}




Kafka는 실시간 데이터 처리를 위한 강력한 도구이며 Spring Boot는 Java 애플리케이션 개발에 널리 사용되는 프레임워크입니다. 이 기사에서는 더 빠르고 쉬운 실시간 데이터 처리를 위해 Kafka를 Spring Boot와 통합하는 방법을 살펴봅니다.

먼저 Kafka와 Spring Boot를 소개한 다음 Spring Boot로 간단한 생산자 및 소비자 예제를 만드는 방법을 살펴보겠습니다. 또한 Kafka를 Spring Boot와 함께 사용하기 위한 몇 가지 팁과 모범 사례를 살펴보겠습니다.

Kafka는 실시간 데이터 처리에 널리 사용되는 도구입니다. 빠르고 확장 가능하며 내구성이 뛰어난 메시지 대기열 시스템입니다. Kafka는 데이터 파이프라인, 스트리밍 데이터 애플리케이션 및 메시지 브로커를 비롯한 다양한 애플리케이션에서 사용됩니다.

Spring Boot는 Java 애플리케이션 개발에 널리 사용되는 프레임워크입니다. 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. Spring Boot는 또한 마이크로서비스를 쉽게 만들 수 있게 해줍니다.

Kafka와 Spring Boot를 통합하는 것은 두 도구가 함께 잘 작동하도록 설계되었기 때문에 자연스럽게 맞습니다. Spring Boot는 Spring 기반 애플리케이션을 쉽게 개발하고 배포할 수 있도록 하는 여러 기능을 제공합니다. Kafka는 빠르고 확장 가능하며 내구성 있는 메시지 대기열 시스템을 제공합니다.

이 기사에서는 Spring Boot를 사용하여 간단한 생산자 및 소비자 예제를 만드는 방법을 살펴보겠습니다. 또한 Kafka를 Spring Boot와 함께 사용하기 위한 몇 가지 팁과 모범 사례를 살펴보겠습니다.

생산자 만들기

생산자를 만들기 위해서는 Spring Boot 애플리케이션을 만들어야 합니다. Spring Boot Initializr를 사용하여 이를 수행할 수 있습니다. Web, Actuator, Aop 및 Lombok 종속성을 선택합니다. Lombok은 일반적인 Java 개발 작업을 위한 상용구 코드를 제공하는 라이브러리입니다.

프로젝트가 생성되면 선호하는 IDE로 가져올 수 있습니다. IntelliJ IDEA를 사용하겠습니다.

프로젝트를 가져오면 KafkaProducerApplication 이라는 새 클래스를 만듭니다. 이 클래스는 Spring Boot 애플리케이션의 진입점이 될 것입니다.

@SpringBootApplication public class KafkaProducerApplication { public static void main(String [] args) { SpringApplication. run ( KafkaProducerApplication . class , args ); } }

다음으로 application.properties 라는 구성 파일을 만듭니다. 이 파일에서 Kafka 부트스트랩 서버 주소 및 주제 이름을 포함한 몇 가지 속성을 구성합니다.

spring.kafka.bootstrap-servers=localhost:9092 spring.kafka.topic.name=테스트

이제 Spring Boot 애플리케이션이 설정되었으므로 생산자를 만들 수 있습니다. KafkaProducer 라는 새 클래스를 만듭니다.

@Component 공개 클래스 KafkaProducer { 비공개 정적 최종 로거 로거 = LoggerFactory . getLogger(카프카프로듀서.클래스); @Autowired private KafkaTemplate < String , String > kafkaTemplate ; 공공 무효 sendMessage (문자열 주제, 문자열 메시지) { 로거. info ( "{}에 메시지 보내기: {}" , 주제 , 메시지 ); 카프카템플릿 . 보내기( 주제 , 메시지 ); } }

이 클래스에서는 KafkaTemplate 을 주입했습니다. KafkaTemplate은 Kafka Producer API를 둘러싼 Spring 래퍼입니다. 메시지 생성을 위한 편리한 방법을 제공합니다.

sendMessage() 메서드도 만들었습니다. 이 메서드는 주제와 메시지를 입력으로 사용합니다. 그런 다음 KafkaTemplate을 사용하여 지정된 주제로 메시지를 보냅니다.

생산자를 설정했으므로 이제 소비자를 생성해 보겠습니다.

소비자 만들기

KafkaConsumer 라는 새 클래스를 만드는 것으로 시작하겠습니다.

@Component 공개 클래스 KafkaConsumer { 비공개 정적 최종 로거 로거 = LoggerFactory . getLogger(카프카소비자.클래스); @KafkaListener ( 주제 = " 테스트 " ) public void receiveMessage ( 문자열 메시지 ) { 로거 . info ( "수신된 메시지: {}" , 메시지 ); } }

이 클래스에서는 @KafkaListener 로 receiveMessage() 메서드에 주석을 달았습니다. 이 주석은 Spring이 메서드를 Kafka 주제에 바인딩하도록 지시합니다. 이 경우 메서드를 테스트 항목에 바인딩하도록 주석을 구성했습니다.

receiveMessage() 메서드는 문자열을 입력으로 사용합니다. 이 문자열에는 Kafka 주제에서 받은 메시지가 포함되어 있습니다.

이제 애플리케이션을 실행하고 Kafka 주제로 메시지를 보낼 수 있습니다. 메시지는 KafkaConsumer에서 수신하고 콘솔에 인쇄됩니다.

팁 및 모범 사례

다음은 Kafka를 Spring Boot와 함께 사용하기 위한 몇 가지 팁과 모범 사례입니다.

1. Spring Kafka 테스트 지원 라이브러리 사용

Spring Kafka 테스트 지원 라이브러리는 Kafka 기반 애플리케이션을 테스트하기 위한 유틸리티를 제공합니다. 여기에는 Kafka 생산자와 소비자를 조롱하는 유틸리티가 포함되어 있습니다.

2. Producer Factory로 Kafka 템플릿 구성

Kafka 템플릿은 Producer Factory로 구성할 수 있습니다. Producer Factory는 Kafka Producer를 구성하는 데 사용할 수 있습니다.

3. Kafka 소비자 오프셋 검사

Kafka 소비자 오프셋을 모니터링하는 것이 중요합니다. 소비자 오프셋은 Kafka 명령줄 도구를 사용하여 검사할 수 있습니다.

4. 스프링 재시도 라이브러리 사용

Spring Retry Library는 실패한 Kafka 작업을 자동으로 재시도하는 데 사용할 수 있습니다.

5. Spring Kafka 배치 리스너 사용

Spring Kafka Batch Listener는 Kafka 주제의 메시지를 일괄적으로 사용하는 데 사용할 수 있습니다.

결론

이 기사에서는 더 빠르고 쉬운 실시간 데이터 처리를 위해 Kafka를 Spring Boot와 통합하는 방법을 살펴보았습니다. 또한 Kafka를 Spring Boot와 함께 사용하기 위한 몇 가지 팁과 모범 사례도 확인했습니다.