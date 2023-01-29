---
title: Kafka로 비동기 메시징 처리
description: 
published: true
date: 2023-01-29T21:33:51.976Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:33:51.976Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Handling Asynchronous Messaging with Kafka***English** version of this document is available*](/en/Knowledge-base/Backend/handling-asynchronous-messaging-with-kafka)
{.links-list}


Kafka는 JMS 및 AMQP와 같은 기존 메시지 브로커 대신 자주 사용되는 처리량이 많은 분산 메시징 시스템입니다. Kafka는 분산 커밋 로그로 설계되어 대용량 메시지 데이터를 처리할 수 있습니다. 또한 Kafka는 여러 메시지 소비자 및 메시지 파티션을 기본적으로 지원하므로 수평으로 확장할 수 있습니다.

다중 메시지 소비자에 대한 Kafka의 지원은 비동기 메시지를 처리하는 데 사용할 수 있음을 의미합니다. 따라서 Kafka는 센서 또는 소셜 미디어 피드와 같은 외부 소스의 메시지 데이터를 처리하는 데 이상적인 선택입니다. 또한 Kafka의 수평적 확장성은 성능에 미치는 영향을 최소화하면서 대량의 메시지 데이터를 처리할 수 있음을 의미합니다.

Kafka를 비동기 메시징에 사용하려면 Kafka 생산자 및 소비자를 설정해야 합니다. Kafka 생산자는 Kafka에 메시지를 보내는 책임이 있고 Kafka 소비자는 Kafka에서 메시지를 읽는 책임이 있습니다.

다음은 비동기 메시지를 처리하도록 Kafka 생산자와 소비자를 설정하는 간단한 예입니다.

import kafka.producer.KeyedMessage; import kafka.producer.ProducerConfig; import java.util.Properties; import java.util.*;

public class AsyncKafkaExample { public static void main(String[] args) { Properties props = new Properties(); props.put("metadata.broker.list", "localhost:9092"); props.put("serializer.class", "kafka.serializer.StringEncoder"); ProducerConfig 구성 = 새 ProducerConfig(props); kafka.javaapi.producer.Producer<String, String> 프로듀서 = new kafka.javaapi.producer.Producer<String, String>(config);

문자열 주제 = "테스트"; 문자열 메시지 = "안녕하세요, 카프카!"; KeyedMessage<String, String> data = new KeyedMessage<String, String>(주제, 메시지); 생산자.보내기(데이터);

생산자.닫기(); } }

import kafka.consumer.ConsumerConfig; import kafka.consumer.ConsumerIterator; import kafka.consumer.KafkaStream; import kafka.javaapi.consumer.ConsumerConnector;

import java.util.HashMap; import java.util.List; import java.util.Map; import java.util.Properties;

public class AsyncKafkaExample { public static void main(String[] args) { Properties props = new Properties(); props.put("zookeeper.connect", "localhost:2181"); props.put("group.id", "테스트 그룹"); props.put("zookeeper.session.timeout.ms", "1000"); props.put("zookeeper.sync.time.ms", "200"); props.put("auto.commit.interval.ms", "1000");

ConsumerConfig 구성 = new ConsumerConfig(props); ConsumerConnector 커넥터 = kafka.consumer.Consumer.createJavaConsumerConnector(config);

문자열 주제 = "테스트"; Map<String, Integer> topicCountMap = new HashMap<String, Integer>(); topicCountMap.put(topic, new Integer(1));

Map<String, List<KafkaStream<byte[], byte[]>>> consumerMap = connector.createMessageStreams(topicCountMap); List<KafkaStream<byte[], byte[]>> streams = consumerMap.get(topic);

for (최종 KafkaStream 스트림: 스트림) { ConsumerIterator<byte[], byte[]> it = stream.iterator();

while (it.hasNext()) { System.out.println("받은 메시지: " + new String(it.next().message())); } }

커넥터.종료(); } }